# Workday Orchestration & WDCLI skills for Microsoft 365 Copilot

**English** · [Polski](README.pl.md)

Skills and instructions for a **Microsoft 365 Copilot agent** (Agent Builder) that helps you
design, build, review and troubleshoot **Workday orchestrations** (Orchestration Builder, Extend
apps and integration apps) and use the **Workday Developer CLI (`wdcli`)**.

This repository contains **text only** — Markdown and `.txt` files. No scripts, no executables.
The ready-to-upload `.zip` packages on the Releases page contain the same text files.

> Unofficial. Not affiliated with, endorsed by or supported by Workday, Inc. or Microsoft.
> "Workday" is a trademark of Workday, Inc.

## What's inside

```
agent/
├── agent-profile.md                 name, description, starter prompts, recommended settings
├── instructions-with-skills.md      agent instructions for variant A (4,958 of 8,000 characters)
└── instructions-without-skills.md   agent instructions for variant B (5,235 of 8,000 characters)
skills/
├── workday-orchestration-design/            templates, triggers, tenant wiring, limits, lifecycle, 13 recipes
├── workday-orchestration-steps/             every component, its tabs and availability; credentials, retries, polling
├── workday-orchestration-expressions/       expression syntax + catalogue of all 926 documented functions
├── workday-orchestration-errors-debugging/  error handlers, logging, debugger, logs, statuses, troubleshooting
├── workday-orchestration-review/            review checklist and how to read exported .orchestration files
└── workday-wdcli/                           wdcli install, login, commands, proxy, CI, legacy wcpcli
LICENSE · NOTICE.md · licenses/
```

Each skill folder has a `SKILL.md` (instructions, under the 20,000-character limit) and a
`references/` folder with `.txt` files the skill reads when it needs them.

## Choose a variant

| | Variant A — custom skills | Variant B — knowledge files |
| --- | --- | --- |
| Requires | Microsoft 365 Copilot licence (or pay-as-you-go) and your organisation in the **Microsoft Frontier Program**; not available with Purview Information Barriers | Microsoft 365 Copilot licence |
| You upload | 6 skill `.zip` packages | 12 `.txt` files |
| Instructions | `agent/instructions-with-skills.md` | `agent/instructions-without-skills.md` |
| Quality | Better: detailed procedures load only when needed | Good: procedures condensed into the instructions |
| Limits | 8 skills per agent, 50 MB per `.zip`, 25 MB per file, 350 files, depth 3 | 20 embedded files per agent |

Custom skills are a preview feature, and an agent can't yet combine skills with uploaded files —
pick one variant per agent.

## Set up variant A (skills)

1. **Get the packages.** Download the six `.zip` files from the latest
   [release](../../releases). Or build them yourself: open a skill folder, select **its contents**
   (`SKILL.md` and `references`), and compress them (Windows: right-click > **Compress to ZIP
   file** / **Send to > Compressed (zipped) folder**). `SKILL.md` must be at the root of the zip —
   don't zip the folder itself. On macOS, Finder may add a hidden `__MACOSX` folder; prefer the
   release packages there.
2. In Microsoft 365 Copilot (<https://m365.cloud.microsoft>) select **Agents & Skills** >
   **New agent**, then **Skip to configure**.
3. **Name** and **Description**: copy from `agent/agent-profile.md`.
4. **Instructions**: paste the whole of `agent/instructions-with-skills.md`.
5. **Skills** > **Add**: upload each `.zip`, then review its name, description, instructions and
   files.
6. **Starter prompts**: add the six from `agent/agent-profile.md`.
7. Optional **Knowledge**: the public website `https://developer.workday.com/documentation`.
8. **Try it**: run the starter prompts, then create and share the agent.

## Set up variant B (knowledge files)

1. Download the repository (**Code > Download ZIP**) and extract it.
2. **New agent** > **Skip to configure**; Name and Description from `agent/agent-profile.md`.
3. **Instructions**: paste `agent/instructions-without-skills.md`.
4. **Knowledge** > upload these 12 files from `skills/*/references/`:
   `platform.txt`, `recipes.txt`, `steps.txt`, `settings.txt`, `syntax.txt`,
   `functions-global.txt`, `functions-strings-text.txt`, `functions-structured-data.txt`,
   `functions-numbers-dates-collections.txt`, `errors-debugging.txt`, `review.txt`, `wdcli.txt`.
5. Turn on **Only use specified sources**.
6. Add the starter prompts and test with **Try it**.

Microsoft treats uploaded knowledge as reference data, not as instructions, so in variant B all
behavioural rules are in the instructions and the files hold facts.

## How the content was made

The skills were written from Workday's developer documentation (336 pages of the Integration Apps,
Orchestrations, Expression Language and CLI sections, retrieved 2026-10-02) and checked against 163
real orchestration files from Workday's
[WorkdayDeveloperProgram](https://github.com/Workday/WorkdayDeveloperProgram) repository. The
function catalogue was generated from the documentation's reference tables (926 functions); two
helpers used by Workday's samples but missing from the reference (`chars.space()`,
`chars.newline()`) are listed separately and marked unverified. Where Workday's documentation contradicts itself (for example `wdcli auth login`
vs `wdcli auth:login`), the skills say so instead of picking one silently.

## Keeping it current

Re-check against the documentation when Workday ships a release: limits
(`workday-orchestration-design/references/platform.txt`), components
(`workday-orchestration-steps/references/steps.txt`), functions
(`workday-orchestration-expressions/references/functions-*.txt`) and commands
(`workday-wdcli/references/wdcli.txt`). After editing a skill, rebuild its `.zip`.

## License

[Apache License 2.0](LICENSE). Third-party sources and their licences: [NOTICE.md](NOTICE.md).
