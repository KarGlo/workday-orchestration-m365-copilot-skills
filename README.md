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
├── instructions-with-skills.md      agent instructions for variant A (5,163 of 8,000 characters)
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

## Set up by copy and paste (no downloads)

Every file below can be copied as text in the browser — nothing is saved to the computer.
For each file, either open the **raw text** link and copy everything (**Ctrl+A**, **Ctrl+C**), or
open the file name and use the **Copy raw file** button (two-squares icon) above its content.
Use this list for the setup in "Set up variant A when Skills accepts `.md` files" below.

- **Instructions** and **Skills**: paste straight into Agent Builder if it offers a text field.
  If Skills only accepts a file, paste into Notepad and save as `SKILL.md` with
  **Save as type: All files** (otherwise Notepad adds `.txt`); keep each skill in its own folder.
- **Attachments**: paste each file into Notepad and save it under **exactly** the name shown — the
  skills look the files up by name.
- `functions-structured-data.txt` is about 54 KB; after pasting, check that the end of the file
  arrived too.

| # | File | Where it goes | Text |
| --- | --- | --- | --- |
| 1 | [`instructions-with-skills.md`](agent/instructions-with-skills.md) | **Instructions** — paste the text | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/agent/instructions-with-skills.md) |
| 2 | [`workday-orchestration-design / SKILL.md`](skills/workday-orchestration-design/SKILL.md) | **Skills > Add** — paste, or save as `SKILL.md` and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-design/SKILL.md) |
| 3 | [`workday-orchestration-steps / SKILL.md`](skills/workday-orchestration-steps/SKILL.md) | **Skills > Add** — paste, or save as `SKILL.md` and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-steps/SKILL.md) |
| 4 | [`workday-orchestration-expressions / SKILL.md`](skills/workday-orchestration-expressions/SKILL.md) | **Skills > Add** — paste, or save as `SKILL.md` and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/SKILL.md) |
| 5 | [`workday-orchestration-errors-debugging / SKILL.md`](skills/workday-orchestration-errors-debugging/SKILL.md) | **Skills > Add** — paste, or save as `SKILL.md` and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-errors-debugging/SKILL.md) |
| 6 | [`workday-orchestration-review / SKILL.md`](skills/workday-orchestration-review/SKILL.md) | **Skills > Add** — paste, or save as `SKILL.md` and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-review/SKILL.md) |
| 7 | [`workday-wdcli / SKILL.md`](skills/workday-wdcli/SKILL.md) | **Skills > Add** — paste, or save as `SKILL.md` and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-wdcli/SKILL.md) |
| 8 | [`platform.txt`](skills/workday-orchestration-design/references/platform.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-design/references/platform.txt) |
| 9 | [`recipes.txt`](skills/workday-orchestration-design/references/recipes.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-design/references/recipes.txt) |
| 10 | [`steps.txt`](skills/workday-orchestration-steps/references/steps.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-steps/references/steps.txt) |
| 11 | [`settings.txt`](skills/workday-orchestration-steps/references/settings.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-steps/references/settings.txt) |
| 12 | [`syntax.txt`](skills/workday-orchestration-expressions/references/syntax.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/references/syntax.txt) |
| 13 | [`functions-global.txt`](skills/workday-orchestration-expressions/references/functions-global.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/references/functions-global.txt) |
| 14 | [`functions-strings-text.txt`](skills/workday-orchestration-expressions/references/functions-strings-text.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/references/functions-strings-text.txt) |
| 15 | [`functions-structured-data.txt`](skills/workday-orchestration-expressions/references/functions-structured-data.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/references/functions-structured-data.txt) |
| 16 | [`functions-numbers-dates-collections.txt`](skills/workday-orchestration-expressions/references/functions-numbers-dates-collections.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/references/functions-numbers-dates-collections.txt) |
| 17 | [`errors-debugging.txt`](skills/workday-orchestration-errors-debugging/references/errors-debugging.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-errors-debugging/references/errors-debugging.txt) |
| 18 | [`review.txt`](skills/workday-orchestration-review/references/review.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-review/references/review.txt) |
| 19 | [`wdcli.txt`](skills/workday-wdcli/references/wdcli.txt) | **Knowledge > Attachments** — save under this exact name and upload | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-wdcli/references/wdcli.txt) |
| 20 | [`agent-profile.md`](agent/agent-profile.md) | Name, Description, Starter prompts — retype | [raw text](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/agent/agent-profile.md) |

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

## Set up variant A when Skills accepts `.md` files

Some Agent Builder versions take a single Markdown file under **Skills > Add** instead of a
`.zip`. Then:

1. Download `upload-files.zip` from the latest [release](../../releases) and extract it. It holds
   `skills/<skill-name>/SKILL.md` (6 files) and `knowledge/` (the 12 `.txt` reference files).
2. **New agent** > **Skip to configure**; Name and Description from `agent/agent-profile.md`.
3. **Instructions**: paste `agent/instructions-with-skills.md`.
4. **Skills** > **Add**: upload each of the six `SKILL.md` files.
5. **Knowledge** > **Attachments**: upload all 12 files from `knowledge/` — the skills look them up
   there by file name.
6. Add the starter prompts and test with **Try it**, for example "Which functions extract a value
   from a JSON response?" — the answer should quote signatures from `functions-structured-data.txt`.

Microsoft lists "agents with both skills and embedded files" as a known preview limitation. If the
agent won't save or ignores the attachments, put the 12 `.txt` files in a OneDrive or SharePoint
folder and add that folder through **Add knowledge** instead, or use variant B.

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
