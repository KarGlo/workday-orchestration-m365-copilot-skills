---
name: workday-orchestration-errors-debugging
description: Handle errors and troubleshoot Workday Orchestrate orchestrations — local and global error handlers, Propagate Error vs Conditional Outputs and isSuccess, processingError, making HTTP failures actually fail, retries and polling timeouts, Validate vs Continue on Conditions, Log / Add Integration Message / Log to File, the step debugger, Build and Run Logs and their fields, Orchestration Activity statuses, cancel vs kill, verbose logging and summary reports. Use when an orchestration fails, times out, hangs in AWAITING_CALLBACK, silently does nothing, produces no output file, returns 403/500, or when the user asks how to add error handling, logging or monitoring.
---

# Error handling and troubleshooting

## Reference files

These `.txt` files are packaged next to this skill (in its `references` folder) or, when the skill was
uploaded as a single `SKILL.md`, attached to the agent's knowledge under the same file names.
Look them up by file name in whichever place is available.

- `errors-debugging.txt` — handler semantics, what counts as a failure, logging
  components, step debugger and its limits, Build/Run Log fields, Orchestration Activity statuses,
  verbose logging API, summary report fields, and a symptom → cause table.

## Procedure: troubleshooting a failing or misbehaving run

1. **Collect evidence first.** Ask for, in this order: template (Sync/Async/BP/IS), the run's
   status in Orchestration Activity, the failing step name (wd_orch_step_name) and the message
   from Run Logs or the integration event's Messages tab. Ask the user to remove personal data
   and tokens from anything they paste.
2. **Match the symptom** against the table in §9 of the reference file. State the most likely
   cause first, with the check that confirms it.
3. **Reproduce with the step debugger** when possible (§4): name the step to start from and the
   inputs to supply. Say when debugging isn't available (Trigger steps, polling) or needs a prior
   deployed run (IS template, lp/intsys in suborchestrations).
4. **Fix and harden.** Give the exact change in Orchestration Builder terms (component, tab,
   field, value or expression).
5. **Prevent recurrence.** Recommend the missing safety net from the checklist below.

## Procedure: adding error handling to an orchestration

1. **Global error handler**: lightning-bolt button. Inside: Log, and in Integration System
   orchestrations also Add Integration Message (severity ERROR) with
   `processingError.locationPath()` and `processingError.message()`.
2. **Every API step** (Send Workday API Request, Send HTTP Request, paged calls): attach a retry
   policy with a success range (e.g. 200-299) or test `responseStatusCode`; add a local error
   handler with a Log (and Add Integration Message in IS).
3. **Choose the handler mode deliberately:**
   - Propagate Error when the run must fail after logging (default for writes).
   - Conditional Outputs when the run can continue: follow it with Branch on Conditions on
     `isSuccess`, and read the protected step's outputs only in the true branch. Not allowed on
     the last step of the orchestration or of a group.
4. **Guard data access** with default-capable accessors where a missing value is acceptable, and
   with Continue on Conditions where it isn't.
5. **Gate debug logging** with a Condition on a launch parameter or app attribute; keep personal
   data and secrets out of log messages.
6. **Long processes**: confirm checkpoints split work under 60/45 minutes; use polling's Error On
   Timeout when a stuck external job must fail the run.

## Rules

- Don't base logic on the text of `processingError.message()` or `rawMessage()`; Workday says they
  are for logging only. Use `isSuccess`, status codes or explicit checks instead.
- Validate never stops a run; Continue on Conditions does.
- Prefer Cancel over Kill; Kill only for stuck runs, and say that it can leave systems
  inconsistent.
- Verbose logging needs a Developer Site bearer token: tell the user it is a secret, not to share
  it, and to limit the duration.

For step configuration see `workday-orchestration-steps`; for expressions see
`workday-orchestration-expressions`.
