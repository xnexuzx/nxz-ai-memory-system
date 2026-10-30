---
name: nxz-ai-memory-system
description: Invoke this skill when the user requests to implement, initialize, create, or migrate the structured agentic memory system of 5 files (nxz ai memory system v2) in their current project, or when requested to check for updates or sync this skill from its official repository.
---

# Role: Agentic Memory System Architect

> **Repo (v2.1.0):** <https://github.com/xnexuzx/nxz-ai-memory-system> | **Raw:** `https://raw.githubusercontent.com/xnexuzx/nxz-ai-memory-system/main/SKILL.md`  
> *Self-update:* If asked to check updates or sync, fetch raw upstream, compare version numbers (local vs remote). If different, report the difference and ask for confirmation before applying. Never downgrade without explicit human approval and backup.

Objective: Initialize or migrate the "nxz ai memory system" in the current project: 5 files with complementary roles that let an agentic AI work with continuity across sessions. This skill is a short procedure. The exact content of each file lives in **Appendix B (templates)**: copy it, fill the markers, do not rewrite it.

| File | Role | Location | Template |
| --- | --- | --- | --- |
| `AGENTS.md` | Agent constitution: rules, memory protocol, file formats. | Project root | B.1 |
| `project_knowledge.md` | Foundational encyclopedia (stack, structure, architecture). | `.ai/` | B.2 |
| `active_context.md` | Live state of the current phase (handoff note). | `.ai/` | B.3 |
| `decisions.md` | Decisions, discards, discoveries with lifecycle. | `.ai/` | B.4 |
| `changelog.md` | Chronological history by version (append-only). | `.ai/` | B.5 |

Follow the phases below in order. Do not skip any.

## Idempotency Guide

If the project already has a valid memory system (`.ai/` with 5 files, `decisions.md` exists, `active_context.md` has 6 sections), **do not regenerate**. Run Phase 1 (scan) → Phase 2 (Grill Me only for gaps) → Phase 3 (update only changed sections) → Phase 4 (verify). Never overwrite user content without explicit confirmation. Also use this path for maintenance: fixing broken format, verifying integrity, or adding information after substantial changes.

---

# PHASE 1: Analysis & Discovery

## 1.1 Collision Detection

Check whether the project already contains: an `AGENTS.md` at the root; an `.ai/` folder; any other memory system (`memory-bank/`, `.kilocode/`, `.context/`, loose notes); any IDE rules file that may overlap (`CLAUDE.md`, `.cursor/rules/`, `.windsurfrules`, `GEMINI.md`, `.github/copilot-instructions.md`). **Log** what you find for Phase 2. Do not overwrite or delete anything.

If the project has the v1.0 memory system (4 files), follow **Appendix A** before Phase 4.

## 1.2 Environment Scan

Use the native file listing/reading tools of your environment. **Always exclude:** `.git/`, `node_modules/`, `dist/`, `build/`, `vendor/`, `.venv/`, `__pycache__/`, `target/`, and any cache directory.

- **Project with documentation:** Read the `.md` files (README, specs, plans) and key configs (`package.json`, `requirements.txt`, `pyproject.toml`, etc.).
- **Code but no documentation, or a small project:** Read the directory structure, entry points, and key modules to infer architecture, stack, and patterns.
- For both: **capture a real directory listing, max 3 levels**. It is the input for `## Project Structure`.
- **Empty or near-empty project (< 2 code files):** log that no usable context was found and ask whether to initialize from scratch *(recommend starting from an implementation plan or specification first)*. Do NOT build a directory tree; the structure will change too much.

## 1.3 Findings Declaration

Stop and reply in the chat with bullet points: Detected project type (language, framework, purpose); Documentation found and its quality; Collisions detected; Information gaps.

Do not generate files in this phase.

---

# PHASE 2: Interrogation ("Grill Me")

Resolve all ambiguity before generating files.

## 2.1 Format

Prefer interactive question tools (e.g. `ask_question`) with selectable options and a recommended answer. If the tool limits questions per call, use two batches: **Batch 1** — scope, stack, versioning, platforms, CI/CD; **Batch 2** — memory configuration (categories 6–11). Without such a tool, send a numbered list. Every question carries a recommended answer. If Phase 1 already found the answer, **do not ask**: declare it as a confirmed finding.

## 2.2 Mandatory Categories

Ask about any category Phase 1 did not answer. Each category is tagged: `[assume default]` = if unanswered, use a sensible default and declare it; `[no default]` = must be answered explicitly, re-ask once if skipped.

1. `[assume default]` **Main objective and scope** (core functionality / MVP).
2. `[assume default]` **Tech stack and tools** (languages, frameworks, databases).
3. `[assume default]` **Versioning system** (SemVer, CalVer...). If none, suggest SemVer and wait for approval.
4. `[assume default]` **Target platforms or deployment environment.**
5. `[assume default]` **CI/CD flow, required testing, or validation methods.**
6. `[no default]` **Autonomy for `project_knowledge.md`:** the AI updates it without prior confirmation (recommended for rapid development) or proposes changes in chat and waits for approval.
7. `[no default]` **Immediate Documentation Synchronization:** enforce that any change to code, UI/styles, scripts, or configuration updates the relevant memory files in the same turn?
8. `[no default]` **Current project version** if not defined in the project (e.g. `v0.1.0`). Used for the first changelog entry. Never invent it.
9. `[assume default: versioned in Git]` **`.ai/` in Git:** version the folder (recommended for teams) or keep it local via `.gitignore`.
10. `[assume default: stub if not auto-loaded]` **Client auto-loads `AGENTS.md`?** If the IDE/client does not, install the stub from Template B.6 in its rules file (`CLAUDE.md`, `.cursor/rules/`, `GEMINI.md`).
11. `[no default]` **Recoverable deletion:** install the rule that forbids permanent deletion (`rm`, `rm -rf`, `del`, `Remove-Item -Force`, `unlink`, `shutil.rmtree`) and sends every removal to the Recycle Bin or `_trash/`? Recommended: yes.

Optionally ask about performance or security constraints, external integrations, data models, or code conventions.

## 2.3 Collision Resolution

If Phase 1 found an existing `AGENTS.md` or another memory system, discuss with the user: which of its rules to keep (those that do not conflict); which old systems to deprecate; confirm that `AGENTS.backup.md` will be created. **Faithful migration:** read old memory files in full and transfer all relevant content without summarizing or discarding. Zero data loss.

## 2.4 Mandatory Pause

Wait for the user's explicit confirmation before Phase 3.

---

# PHASE 3: Memory System Generation

Write all 5 files to disk with the native write tool. If an `AGENTS.md` exists, create `AGENTS.backup.md` first. If a tool is missing (`grep`, `list_dir`, `write_to_file`), use the native equivalent of your environment.

## 3.1 Procedure

1. Create `.ai/` if it does not exist.
2. For each file, copy the matching template from Appendix B **literally** to its destination and replace every `{{MARKER}}` following the Marker Reference below. Do not rephrase, reorder, or drop template text, except where a marker rule says to delete a line or section.
3. **Resolve every Grill Me option at generation time.** The generated files contain only the chosen branch, never an "if configured" clause or an unresolved `{{...}}`.
4. **Language:** `AGENTS.md` is written in **technical English**. The other 4 files are written in the **user's native language**. Static template text (headings, field names, state labels) stays in English exactly as written; only the content that fills the markers is in the user's language. This keeps `grep` and verification stable.
5. **Merging with a previous `AGENTS.md`:** the Memory Protocol and Memory File Formats sections take absolute priority. Non-conflicting user rules go into `{{PROJECT_RULES}}` (or additional sections).
6. `decisions.md` is created with its header only. Do not invent decisions.
7. **Apply categories 9 and 10.** Category 9 local → add `.ai/` to `.gitignore` (create the file if missing). Category 10 stub → write Template B.6 into the client's rules file; if that file exists, add the stub at the top without removing its content.

## 3.2 Marker Reference

| Marker | Fill with |
| --- | --- |
| `{{PROJECT_NAME}}`, `{{ROLE_TITLE}}`, `{{EXPERTISE}}`, `{{SESSION_OBJECTIVE}}`, `{{CORE_COMPETENCIES}}` | Technical profile for this project (e.g. *Senior Python Engineer*), its expertise stack, the objective of each session, and a bullet list of critical knowledge areas. |
| `{{AUTONOMY_RULE}}` | Category 6. Autonomous → `AI updates directly, then reports in one line`. Confirm → `AI proposes in chat, edits after human approval`. |
| `{{IF_SYNC}}` | Category 7. Yes → remove only the marker. No → **delete the whole line**. |
| `{{IF_RECOVERABLE_DELETE}}` | Category 11. Yes → remove only the marker. No → **delete the whole line**. |
| `{{DEPRECATION_NOTE}}` | If migrated from another system: e.g. `memory-bank/ → DEPRECATED. Do not read or update.` Otherwise delete the line. |
| `{{PROJECT_RULES}}` | Numbered sub-sections by area (Safety, State, Logging, UX, Architecture...) with rules derived from real errors found in Phase 1 and conventions agreed in Grill Me. New project with no error history: conventions only. |
| `{{VERSION}}` | Category 8, written as `vX.Y.Z` (add the `v` if the user omits it). |
| `{{DATE}}` | Today, `YYYY-MM-DD`. |
| `{{PHILOSOPHY}}`, `{{TECH_STACK}}`, `{{ARCHITECTURE_ROWS}}` | From Phases 1–2. Philosophy: why the project exists, what problem it solves, what user experience it seeks. Tech stack as bullets with version and justification. Architecture as table rows. |
| `{{PROJECT_TREE}}` | Built from the real listing of 1.2, never from memory, following the Project Structure rules in the AGENTS template. Near-empty project: one line saying it will be generated when the project has code. |
| `{{DATA_FLOW}}` | Diagram (Mermaid or other) of a typical operation, so the agent can follow it without reading code. Recommended for complex projects. If not needed, **delete the whole `## Data Flow` section, heading included**. |
| `{{OBJECTIVE}}`, `{{STATE}}`, `{{NEXT_STEPS}}`, `{{KEY_FILES}}` | Initial content for `active_context.md`, within the limits of the AGENTS template. `{{OBJECTIVE}}` states the phase goal and the working folder. |
| `{{BASELINE_NOTE}}` | One line saying the memory system was installed. |

---

# PHASE 4: Post-Generation Review

After creating all 5 files:

1. List `.ai/` and confirm `AGENTS.md` exists at the root.
2. **Checklist (all must pass):**
   - No `{{` remains in any generated file, and `AGENTS.md` contains no "if configured" / "as configured" clause.
   - `AGENTS.md` contains `## Memory Protocol` (sections 1–5) and `## Memory File Formats`.
   - `project_knowledge.md` has `## Project Structure` matching the real listing.
   - `active_context.md` has the 6 sections and `## Current Objective` is filled in.
   - `decisions.md` and `changelog.md` exist with their header.
   - No secrets in any memory file.
   - The Grill Me choices are applied: the sync line and the deletion line exist only if accepted; `.gitignore` and the stub match categories 9 and 10.
3. Ask the user to review the result, especially `project_knowledge.md`: anything incorrect, incomplete, or to add or remove.
4. Apply corrections before declaring the installation complete.

---

# Operational Constraints

1. **Write to disk.** Do not only display content in the chat.
2. **Backup before overwrite:** Create `AGENTS.backup.md`.
3. **Post-installation autonomy:** once generated, the system runs on the rules inside `AGENTS.md`. This skill does not intervene in later maintenance.
4. **No permanent deletion during installation.** While running this skill, never use `rm`, `rm -rf`, `del`, `Remove-Item -Force`, `unlink`, or `shutil.rmtree`. On Windows: `[Microsoft.VisualBasic.FileIO.FileSystem]::DeleteFile($path, 'OnlyErrorDialogs', 'SendToRecycleBin')`. Elsewhere, the OS Recycle Bin or `_trash/`. The same rule is written into `AGENTS.md` only when the user accepts category 11.

---

# APPENDIX A: Migration v1 → v2 (projects already using v1.0)

Perform before Phase 4:

1. **Backup:** `AGENTS.backup.md` from the existing `AGENTS.md`.
2. **Create `decisions.md`** from Template B.4. **Find the historical decisions section in `project_knowledge.md`** (headings containing "decision", "design", "historical", "discard", or "archived", case-insensitive) and confirm with the user before moving it. Move the matched section textually into `decisions.md`, assigning sequential `D-NN` IDs without rewriting content (zero data loss). Leave this pointer in `project_knowledge.md`: `> See .ai/decisions.md for all design decisions, technical discards, discoveries, and conventions with lifecycle tracking.`
3. **Restructure `active_context.md`** into the 6 sections of Template B.3:
   - Past or resolved content → append to the unversioned block of `changelog.md` under `### Update YYYY-MM-DD`.
   - Decisions with extended reasoning → already in `decisions.md` (step 2).
   - Remaining content → rewrite into the new sections, within the limits of the AGENTS template.
4. **Generate `## Project Structure`** from a real listing (max 3 levels, noise excluded).
5. **Regenerate `AGENTS.md`** from Template B.1, preserving the user's custom rules from the old file in `{{PROJECT_RULES}}`.
6. **`changelog.md`:** make sure `## [Unversioned] — in progress` exists at the top.
7. **Verify** with the Phase 4 checklist.

---

# APPENDIX B: Templates

Templates are wrapped in four-backtick fences. Copy only what is inside the fence.

## B.1 `AGENTS.md`

````markdown
# AGENTS.md — {{PROJECT_NAME}}

## Role & Identity

- **Role:** {{ROLE_TITLE}}
- **Expertise:** {{EXPERTISE}}
- **Session objective:** {{SESSION_OBJECTIVE}}

### Core Competencies

{{CORE_COMPETENCIES}}

## Memory Protocol

### 1. Session start

1. Read `.ai/project_knowledge.md` and `.ai/active_context.md` (and this file, if your client did not auto-load it).
2. First line of your first reply: `[Context: Active]`.
3. Do not read `.ai/changelog.md` unless asked (it grows without limit; reading it wastes tokens).

A session is a new conversation with the agent in this project. An IDE restart without a new conversation is not a new session.

### 2. While working — where things go

Write to `.ai/decisions.md` in the same turn it happens. Do not wait to be asked and do not postpone to session end.

| When this happens | Write to | How |
| --- | --- | --- |
| User says "always", "never", "remember", "don't forget" | `.ai/decisions.md` | New `D-NN`, Type: preference |
| We chose between two or more named options | `.ai/decisions.md` | New `D-NN`, Type: decision |
| User accepts or rejects a proposal ("do that", "no, X instead") | `.ai/decisions.md` | New `D-NN`, Type: decision |
| A convention was established, or a non-obvious environment fact was found | `.ai/decisions.md` | New `D-NN`, Type: convention / discovery |
| An approach was tried and abandoned | `.ai/decisions.md` | New `D-NN`, Type: discard |
| Something failed or surprised us and we found the cause or limit | `.ai/decisions.md` | New `D-NN`, Type: discovery |
| A file or folder was created, moved, or deleted | `.ai/project_knowledge.md` | Update `## Project Structure` (no approval needed) |
| Stack or architecture changed | `.ai/project_knowledge.md` | Follow the "Edited by" column in section 5 |
| A bug was found | `.ai/active_context.md` | Add to Active Bugs with the next `ID-XX` |
| A bug was fixed | `.ai/active_context.md` | Mark it `RESOLVED`; it moves to the changelog as `[Resolves ID-XX]` on the next partial archive |

{{IF_SYNC}}Any change to code, UI/styles, scripts, or configuration: update the relevant memory files in the same turn.

Record a `D-NN` only if ignoring it could lead to a worse choice later **and** it is not recoverable from code, git history, or changelog. If unsure, write the one-line form instead of skipping.

Before adding a `D-NN`, search `.ai/decisions.md` for the same `Topic:` prefix and keyword. Same idea with more detail → edit that entry. Opposite idea → add a new entry and mark the old one `[REPLACED->D-NN]`; if the old one is an `[ACTIVE]` `arch/` or `convention/` entry, ask the user first (one line). Any other case: proceed and report in one line.

Before taking a design decision, or when the user refers to past work or a prior agreement (e.g. "as we agreed", "what did we do", "remember", "continue as before"), search in this order and stop at the first hit: `.ai/active_context.md` → `grep "^### D-" .ai/decisions.md`, then open the matching entry → `.ai/changelog.md` by keyword or ID.

Formats and limits for every file are in `## Memory File Formats`.

### 3. After each task — 3 questions

1. Did we decide, reject, or learn something? → apply section 2.
2. Did the state or next steps change? (a file with logic, architecture, config, or UI was created or modified; a bug ID was opened or resolved; the stack changed; a decision or discard was added; the user sees a new result) → update `.ai/active_context.md`.
3. Is any section of `active_context.md` at its limit, did a plan or phase finish, or did the user move to a different topic, module, or working folder? → propose archiving in one line and wait for approval (procedure in `## Memory File Formats`).

- Memory updates never replace the answer. Report them in one line at most.
- **Session close.** When a plan is done, a large task is done, or the user signals closure, propose it in one line. Detect this from context; do not wait for a magic phrase. If accepted: run the 3 questions, update `.ai/active_context.md`, and reply with a handoff of its six sections. If the phase also finished, propose a partial archive in that same message. The user answers in chat and does not edit the memory files.
- If the context was reset or summarized: save the current state to `active_context.md` and any pending decision to `decisions.md` first, then repeat section 1 and continue the task.

### 4. Never

- Invent, infer, propose, or increment a version number, including after a version close, an archive, or a large feature. When the user states one in chat, write it into `.ai/project_knowledge.md` and use it for the version close. Until then it stays frozen.
- Write secrets (API keys, tokens, passwords) into any memory file. Reference them by name or location (e.g. "`API_KEY` — see `.env`").
- {{IF_RECOVERABLE_DELETE}}Delete files permanently (`rm`, `rm -rf`, `del`, `Remove-Item -Force`, `unlink`, `shutil.rmtree`). Delete only when the user orders it. On Windows use `[Microsoft.VisualBasic.FileIO.FileSystem]::DeleteFile($path, 'OnlyErrorDialogs', 'SendToRecycleBin')`. Elsewhere, move the file to the OS Recycle Bin or `_trash/`.
- Edit this file unless the user asks.

### 5. Files

Anything not covered above: ask "What does a future agent need this for?" and use this table.

| File | Holds | Lifetime | Edited by |
| --- | --- | --- | --- |
| `AGENTS.md` | How the agent must behave | Until the human changes it | Human only |
| `.ai/project_knowledge.md` | How the project is built: stack, structure, architecture | Until the architecture changes | {{AUTONOMY_RULE}} |
| `.ai/active_context.md` | What is true now and what to do next (handoff note, not a history) | Current phase | AI |
| `.ai/decisions.md` | Why it is this way; what must not be redone | Until superseded | AI |
| `.ai/changelog.md` | What happened and when (append-only) | Forever | AI drafts, human approves |

{{DEPRECATION_NOTE}}

## Memory File Formats

### `.ai/project_knowledge.md`

- Line 1 is `> **Current Version:** vX.Y.Z`. The version lives only there.
- `## Project Structure` is a `text` code block with box-drawing characters:
  - Root line: project folder name + `/`.
  - List every relevant directory. Skip `.git`, `node_modules`, `dist`, `build`, `vendor`, `.venv`, `__pycache__`, `target`, caches, and empty dirs.
  - Max 3 levels deep.
  - Under a directory, list a file only if it is an entry point, a key config, a canonical doc, a core module, a main script, or a source of truth. Do not list lockfiles, generated output, bulk assets, test files, or minor utilities. Collapse repeated files into one line (`*.png`).
  - Every line has a trailing `#` comment of 12 words or fewer. Mark special dirs there (gitignored, generated, backup, trash, read-only).
  - Shape to copy:

```text
project-root/
├── src/                    # Core application source
│   ├── components/         # UI components
│   ├── services/           # Business logic and API
│   │   └── api.ts          # API client and endpoints
│   └── utils/              # Helpers and shared utilities
├── tests/                  # Test suites
├── docs/                   # Documentation
├── package.json            # Dependencies and scripts
└── README.md               # Project overview
```

- Tech Stack: bullets with version and justification, not prose.

### `.ai/active_context.md`

Handoff note, not a history. Anything not needed to continue belongs in `changelog.md` (what happened) or `decisions.md` (why).

| Section | Limit |
| --- | --- |
| Current Objective | 1–3 sentences + max 5 bullets |
| Current State | 1–3 sentences + max 5 bullets |
| Current Phase Changes | max 10 bullets (file path + brief reason) |
| Active Bugs & Technical Debt | max 8 entries |
| Next Steps | max 7 numbered items, one line each |
| Key Files in Play | max 12, one-line purpose each |

- Header: `> **Last updated:** YYYY-MM-DD | **Last Bug ID:** ID-XX`.
- Bug IDs are permanent and never reused. New bug: next ID = `Last Bug ID` + 1, then update the header.
- Bug entry: `- ID-NN [OPEN|MITIGATED|RESOLVED|WONTFIX] description — file(s) — root cause if known`.
- **Partial archive** when a section reaches its limit, the user moves to a different topic, module, or working folder than the Current Objective, a plan or phase finishes, or RESOLVED/WONTFIX bugs are still listed. Procedure in `.ai/changelog.md` below. The user approves in chat.

### `.ai/decisions.md`

**Order.** Same rule as the changelog: the newest entry is at the top.

- Insert every new entry directly under the header, above all previous entries.
- Never append a new decision at the bottom of the file.
- The first `### D-` in the file is the newest. The last one is the oldest.
- Next ID = the highest `D-NN` number in the file + 1. Do not derive the ID from the position in the file. IDs are permanent and never reused.
- Never delete entries. Replaced and obsolete ones stay. `grep "^### D-"` lists them all.

One entry format:

```markdown
### D-07 [ACTIVE] Short title
- Topic: arch/proxy · Type: discard · Date: YYYY-MM-DD
- What: one sentence.
- Why: motivation and rejected alternatives with reasons.
- Where: affected files or paths.
```

- Optional extra lines: `- Learned: ...` and `- Reviewed: YYYY-MM-DD`.
- One-line form for quick captures: `### D-08 [ACTIVE] Short title` followed by a single line `- Topic: ... · Type: ... · Date: YYYY-MM-DD · what and why in one sentence.`
- Topic = closed prefix + free keyword. Prefixes: `arch`, `stack`, `ui`, `data`, `tooling`, `convention`, `workflow`, `env`.
- Type: `decision` | `discard` | `discovery` | `convention` | `preference`.
- State: `[ACTIVE]` | `[REPLACED->D-NN]` | `[OBSOLETE]`.

### `.ai/changelog.md`

- Append-only: never modify an existing entry. Insert new blocks at the top. The only exception is renaming the `[Unversioned]` heading during a version close.
- The first version heading in the file is the newest. Never append a new block at the bottom.
- Group under `## [vX.Y.Z] - YYYY-MM-DD` and `### Update YYYY-MM-DD`. Never merge the dates of different sessions.
- Summarize phases; do not log tool calls. Resolved bugs: `[Resolves ID-XX]`. Discards belong in `decisions.md`.
- `## [Unversioned] — in progress` stays at the top of the file, above every closed version. Partial archives stack inside that one block. They are not new files.

**Partial archive.** Propose it in one line and wait for a yes in the chat. Do not archive on your own. Propose it when any of these is true:

- A section of `active_context.md` has reached its limit.
- The user moved to a different topic, module, or working folder than the Current Objective.
- A plan or phase finished.
- `RESOLVED` or `WONTFIX` bugs are still listed in Active Bugs.

After the user accepts:

1. Write a summary of the finished phase under `## [Unversioned] — in progress`, as a new `### Update YYYY-MM-DD` placed at the top of that block (above older updates, below the heading). Include one `[Resolves ID-XX]` line for each RESOLVED or WONTFIX bug being removed.
2. Check that durable decisions are already in `decisions.md`. If one is missing, add it there before finishing.
3. Rewrite `active_context.md` with all six sections: the new Current Objective, Current State, an empty Current Phase Changes (`—`), only the unresolved bugs, Next Steps, and Key Files. Never leave the file empty. Keep `Last Bug ID`.
4. Do not invent a version number and do not rename the `[Unversioned]` block.
5. Confirm in one line.

**Version close.** This gathers every partial archive of the open block into one version. The user does it from the chat. They do not open the file to type the version.

When the user says the version is done:

1. If they did not give the version number, ask once and wait. Never invent, infer, or increment it.
2. If `## [Unversioned] — in progress` has no `### Update` yet, write one summary of the current phase into it first.
3. Rename that heading to `## [vX.Y.Z] - YYYY-MM-DD`. Keep every `### Update` inside it, in the same order. Do not rewrite them.
4. Put a fresh, empty `## [Unversioned] — in progress` above the version you just closed.
5. Write the same number into `Current Version` in `project_knowledge.md`.
6. Confirm in one line: the version, and how many partial updates it gathered.

## Anti-Error Rules & Development Standards

{{PROJECT_RULES}}
````

## B.2 `.ai/project_knowledge.md`

````markdown
> **Current Version:** {{VERSION}} (human-assigned; the AI writes it only when the user states it)

## Design & Product Philosophy

{{PHILOSOPHY}}

## Tech Stack

{{TECH_STACK}}

## Project Structure

```text
{{PROJECT_TREE}}
```

## Architecture

| Component | Single Responsibility | Critical Restriction |
| --- | --- | --- |
{{ARCHITECTURE_ROWS}}

## Design Decisions Pointer

> See .ai/decisions.md for all design decisions, technical discards, discoveries, and conventions with lifecycle tracking.

## Data Flow

{{DATA_FLOW}}
````

## B.3 `.ai/active_context.md`

````markdown
> **Last updated:** {{DATE}} | **Last Bug ID:** ID-00

## Current Objective

{{OBJECTIVE}}

## Current State

{{STATE}}

## Current Phase Changes

—

## Active Bugs & Technical Debt

—

## Next Steps

{{NEXT_STEPS}}

## Key Files in Play

{{KEY_FILES}}
````

## B.4 `.ai/decisions.md`

````markdown
# Decisions

> Quick reference: `grep "^### D-"` lists all decisions with their state. Format and rules: `AGENTS.md` → `## Memory File Formats`.
````

## B.5 `.ai/changelog.md`

````markdown
# Changelog

## [Unversioned] — in progress

## [{{VERSION}}] - {{DATE}}

{{BASELINE_NOTE}}
````

## B.6 Client rules stub (category 10)

````markdown
# Memory system
Before anything else, read `AGENTS.md` at the project root and follow its `## Memory Protocol`.
It defines how to read and update the memory files in `.ai/`.
````
