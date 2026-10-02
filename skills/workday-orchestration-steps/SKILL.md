---
name: workday-orchestration-steps
description: Choose and configure Workday Orchestration Builder components (steps) — Send Workday API Request, Send HTTP Request, paged REST/SOAP/HTTP calls, Send Workday RaaS Request, Trigger Business Process, Trigger Integration, Trigger PDF Generation, Create Values, Create JSON, Create Text Template, Validate, Store/Find/Retrieve Document, Loop, Batch Loop, Join Loop, Branch on Conditions, Continue on Conditions, Log, Log to File, Add Integration Message, Call Suborchestration, Home Card and AWS steps — plus orchestration Settings such as credentials, ISU, OAuth, HTTP retry policies, HTTP polling, CSV formats and aggregations. Use when the user asks which step to use, how to configure a step's tabs, which template supports a step, how to paginate, authenticate, retry, poll, store files or aggregate loop results.
---

# Orchestration Builder steps and settings

## Reference files in this skill

- `references/steps.txt` — availability matrix by template, every component's properties,
  outputs, limits and gotchas, and the internal node name used in exported files.
- `references/settings.txt` — credentials (API Key, Basic, OAuth, ISU, AWS SigV4) and ISU setup,
  HTTP retry policies, HTTP polling, CSV formats, aggregations, async cancellation, OpenAPI
  export.

## Procedure

1. **Identify the template** (Sync, Async, Business Process, Home Card, Integration System, or a
   suborchestration) and whether the app is an Extend app or an integration app. Integration apps
   only have Business Process and Integration System templates.
2. **Check availability** in the matrix before recommending a step. State restrictions plainly:
   RaaS, Trigger Business Process, Trigger Integration and Trigger PDF Generation can't run in a
   join loop; RaaS and Trigger Business Process can't be added to suborchestrations; Log to File,
   Add Integration Message, Trigger Integration and Trigger PDF Generation are Integration System
   only; AWS steps are Extend Pro only.
3. **Configure tab by tab** in the order the user sees them (General/Auth, Body, Headers, Query
   Parameters, Pagination, Launch Parameters, Document, Settings). Give field names exactly as
   Orchestration Builder labels them.
4. **Name the outputs** the next steps will use (`response`, `responseStatusCode`, `message`,
   `data`, `item`, `itemNumber`, `entryId`, `isSuccess`, ...) and show the reference syntax
   `data.StepName.output`.
5. **Flag long-running and checkpoint behaviour**: RaaS (up to 1 h), Trigger Business Process
   (must finish within 90 days), Trigger Integration (waits for the child's callback), Trigger PDF
   Generation, polling — each starts a new process; synchronous orchestrations must stay inside
   5 minutes and 25 seconds when a page waits on them.

## Decisions to get right

- **Workday API vs HTTP**: always Send Workday API Request (or the paged Workday steps) for
  Workday; Send HTTP Request only for external systems.
- **Failure on HTTP errors**: an unsuccessful HTTP response does not fail the run unless a custom
  retry policy with a success range is attached or the status is tested. Recommend one of the two
  on every API step.
- **Pagination**: Workday REST → Send Paged Workday REST Call (limit/offset); WWS → Send Paged
  Workday SOAP Call (don't add the SOAP envelope); external → Send Paged HTTP Request (offset or
  one of the cursor variants).
- **Large reads**: RaaS report or paged calls feeding a Loop/Batch Loop; Join Loop for matching
  two datasets by key instead of nested loops.
- **Writing files**: Create Text Template or a CSV/Text/JSON Fold aggregation → Store Document
  with "Attach document to integration event" = boolean true in IS orchestrations.
- **Logging**: Log everywhere; in IS orchestrations add Add Integration Message so messages reach
  the integration event; Log to File for CSV logs attached to the event.
- **Reuse**: Call Suborchestration for repeated logic and to keep Branch on Conditions nesting at
  3 levels or fewer.
- **Credentials**: prefer the initiating user's access token or an ISU configured on the
  integration system / business process step; use OAuth Cred Store Reference (not a pasted
  token) in production.

## Security rules for answers

- Never ask the user for passwords, client secrets, tokens or API keys, and never put real ones in
  examples — use placeholders such as `<client-secret>`.
- Explain where a secret is stored (Cred Store, Settings > Credentials) instead of what it is.

For expressions inside step fields, use the `workday-orchestration-expressions` skill; for error
handlers and debugging, `workday-orchestration-errors-debugging`.
