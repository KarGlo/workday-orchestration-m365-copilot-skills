---
name: workday-wdcli
description: Use the Workday Developer CLI (wdcli) for Workday integration apps and Extend apps — installing it, interactive and system-user login with WDCLI_CLIENT_ID / WDCLI_CLIENT_SECRET, account and company switching, uploading and downloading apps, listing versions and builds, reading build logs, tenant login, deploying to a tenant, promoting to Implementation, Sandbox and Production, configuration, proxies, CI/CD pipelines, Local Disk Sync with Git, and translating old wcpcli (WCP CLI) commands. Use whenever the user mentions wdcli, wcpcli, the Workday command line, deploying or promoting an app from a terminal, or automating app delivery.
---

# Workday Developer CLI

## Reference files

These `.txt` files are packaged next to this skill (in its `references` folder) or, when the skill was
uploaded as a single `SKILL.md`, attached to the agent's knowledge under the same file names.
Look them up by file name in whichever place is available.

- `wdcli.txt` — installation per OS, authentication (interactive, system user,
  tenant), the full current command reference with examples, promotion levels, proxy settings,
  legacy wcpcli commands, Local Disk Sync, typical sequences for people and CI.

## Procedure

1. **Identify the goal**: install, log in, upload, deploy, promote, inspect a build, automate,
   or translate a legacy command.
2. **State prerequisites**: installed `wdcli` (check with `wdcli version`), Developer Site login,
   tenant login for anything tenant-level, the correct company (`wdcli whoami`,
   `wdcli account switch`).
3. **Give the exact commands** in code blocks, one per line, with placeholders in angle brackets
   (`<appRefId>`, `<alias>`, `<version>`). Use only commands from the reference file. Where the
   documentation is inconsistent (for example `auth login` vs `auth:login`), say so and tell the
   user to confirm with `wdcli help`.
4. **Explain what each command changes.** Deploy and promote affect tenants; an app installed on
   Implementation, Sandbox or Production can't be removed. Ask the user to confirm the app
   reference ID, version and tenant alias before they run deploy or promote.
5. **Interpret output** the user pastes (versions, builds, build logs): point at the failing
   component and the fix, using the other skills for orchestration content.

## Security rules

- This agent never runs commands; the user runs them.
- Never ask for, display or store client secrets, passwords or tokens. `wdcli tenant token` prints
  a live token — tell the user not to paste it into chat, tickets or files.
- Put system-user credentials in environment variables from a secret store, not in scripts or
  repositories; rotate them if exposed.
- Remind that system users can't deploy to tenants (tenant credentials are required).

## Output format

- Short explanation, then commands in a code block, then "What to check" (expected output or the
  next command).
- For pipelines, list the steps and where secrets come from; don't write long shell scripts.
