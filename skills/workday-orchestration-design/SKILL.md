---
name: workday-orchestration-design
description: Design and plan Workday Orchestrate orchestrations and integration apps end to end — choosing between Extend and integration apps, picking the template (Synchronous, Asynchronous, Business Process, Home Card, Integration System, suborchestration), wiring triggers in the tenant (integration system attributes and launch parameters, business process Orchestration Service steps, launch on Cancel/Rescind/Correct/Deny, launching from Extend pages), processes and checkpoints, runtime and data limits, security and ISU, app attributes, lifecycle and promotion, and ready-made recipes for common integrations. Use when the user describes a requirement to automate, asks how to architect or start an orchestration, asks about limits or timeouts, or needs the tenant-side setup.
---

# Designing Workday orchestrations

## Reference files in this skill

- `references/platform.txt` — templates and start/end steps, processes and checkpoints, every
  documented limit, trigger wiring in the tenant, lifecycle and promotion, app attributes,
  security, regional endpoints and IP allowlists, comparison with other integration tools.
- `references/recipes.txt` — 13 worked patterns (outbound file integration, large reports,
  pagination, joins, retries, polling, chaining integrations, business process hooks, Extend page
  calls, PDF generation, error notification, cancellable jobs).

## Procedure

**Step 1 — Clarify the requirement.** Ask only what changes the design, one question at a time:
- What starts it: a schedule or manual launch, a business process step or status change, an
  Extend page, an external caller?
- What data in and out, and how much (rows, file size)?
- Which systems: Workday APIs (REST, SOAP, RaaS, WQL, Graph) and/or external APIs?
- Is someone waiting for the answer (synchronous) or not?
- Extend app or integration app (licence)?

**Step 2 — Pick the template** with the table in `references/platform.txt` §2:
- someone waiting, short work → Synchronous (5 min; 25 s if a page waits);
- long work or awaiting other events → Asynchronous (48 h) or Integration System (48 h);
- reacting to a business process → Business Process;
- scheduled or launched integration with launch parameters, messages and output files →
  Integration System;
- repeated logic → suborchestration.
Integration apps can only use Business Process and Integration System.

**Step 3 — Check limits early** (`platform.txt` §4): process 60/45 min with checkpoints, memory
200 MB, disk 2 GB, response 500 MB, launch 20 MB, 300 steps, 150 orchestrations per app.
Design batching (Batch Loop, paged calls, RaaS) before building.

**Step 4 — Sketch the flow** as a numbered list of components with their Reference Names, using
a matching recipe from `references/recipes.txt` as the starting point. Include for every API
step: credential, failure detection (retry policy with success range or status test), local error
handler with logging. Add a global error handler.

**Step 5 — Describe the tenant wiring** for the chosen trigger (`platform.txt` §5) and the
security setup (credentials, ISU, domains) the run needs.

**Step 6 — Plan delivery**: Save to App Hub → deploy to development/implementation → test with
the debugger and Run Logs → promote Implementation → Sandbox → Production → install and configure
in App Manager (attributes per environment).

## Output format

- Start with a one-paragraph summary of the design and the chosen template, with the reason.
- Then a numbered component list: `n. <Component> "<ReferenceName>" — purpose; key settings`.
- Then "Tenant setup" and "Risks and limits" as short bullet lists.
- Use exact Orchestration Builder labels in **bold** and expressions in code blocks.
- Mark anything not confirmed by the reference files as an assumption.

## Boundaries

- This agent explains and designs; it can't open Orchestration Builder or the tenant. Give the
  user click paths to perform.
- Don't propose hand-editing exported `.orchestration` files; changes are made in Orchestration
  Builder.
- Never ask for or repeat secrets, tokens or passwords.
