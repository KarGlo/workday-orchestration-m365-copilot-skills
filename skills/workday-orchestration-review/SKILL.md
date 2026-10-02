---
name: workday-orchestration-review
description: Review, audit or explain an existing Workday orchestration or suborchestration — from a description, screenshots, or an exported .orchestration / .suborchestration file (single-line JSON from Download Source). Checks error handlers, HTTP failure detection, security domains, safe accessors, step placement and template restrictions, limits, credentials and logging against a documented checklist, and maps export node names to Orchestration Builder components. Use when the user asks to review, audit, check quality, explain what an orchestration does, prepare for production or promotion, or pastes or attaches an orchestration file.
---

# Reviewing orchestrations

## Reference file in this skill

- `references/review.txt` — how to get the export, the JSON structure, UI ↔ export node names,
  the review checklist with severities, observations about Workday samples, and the report
  format.

## Procedure

1. **Get the input.**
   - Exported file: ask the user to attach the `.orchestration` / `.suborchestration` file from
     Download Source (rename to `.txt` or `.json` if the chat rejects the extension), or paste
     it. Ask them to remove credentials, usernames of real people and tenant data first.
   - No file: ask for the template, the list of steps in order, and screenshots of the
     relevant property panels.
2. **Orient.** From the export, report: name, flow type (template), start/end types, number of
   nodes, global error handler present or not, security domains, credentials defined, retry
   configurations. Translate node types to UI names with the table in §3.
3. **Explain the flow** in plain language: trigger → each step (Reference Name, component,
   purpose) → outputs. Quote expressions from `source` fields when they matter.
4. **Apply the checklist** in §4 item by item. For each issue record severity, rule, location
   and fix. Don't invent issues: if a check can't be performed from the input, list it under
   "Not verifiable".
5. **Write the report** in the format of §6: ACTION findings first, then ADVICE, then
   "Checked" and "Not verifiable".
6. **Offer next steps** (for example: the fix order, or help writing the corrected expressions
   with the `workday-orchestration-expressions` skill).

## Rules

- Fixes are made in Orchestration Builder. Never suggest editing the exported JSON by hand.
- Workday's sample orchestrations are not a quality benchmark; judge against the checklist.
- If the file contains secrets or personal data, tell the user to rotate/remove them, and don't
  repeat them in the answer.
- Be explicit about severity: ACTION blocks production readiness, ADVICE improves quality.
