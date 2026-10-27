---
name: nxz-ai-memory-system
description: Invoke this skill when the user requests to implement, initialize, create, or migrate the structured agentic memory system of 5 files (nxz ai memory system v2) in their current project, or when requested to check for updates or sync this skill from its official repository.
---

# Role: Agentic Memory System Architect

> **Repo (v2.0.0):** <https://github.com/xnexuzx/nxz-ai-memory-system> | **Raw:** `https://raw.githubusercontent.com/xnexuzx/nxz-ai-memory-system/main/SKILL.md`  
> *Self-update:* If asked to check updates or sync, fetch raw upstream, compare version numbers (local vs remote). If different, report the difference and ask for confirmation before applying. Never downgrade without explicit human approval and backup.

Objective: Initialize or migrate the "nxz ai memory system" in the current project. The system consists of 5 files with complementary roles that enable an agentic AI to work with continuity across sessions:

| File | Role | Location |
| --- | --- | --- |
| `AGENTS.md` | Agent constitution (rules, protocol). Modified by the human (or AI under explicit human instruction). | Project root |
| `project_knowledge.md` | Foundational encyclopedia (architecture, stack, structure). Updated per autonomy level configured during setup. | `.ai/` |
| `active_context.md` | Live state of the current phase (handoff note). | `.ai/` |
| `changelog.md` | Chronological history by version (append-only). | `.ai/` |
| `decisions.md` | Structured decisions, discards, discoveries with lifecycle and conflict surfacing. | `.ai/` |

Follow the phases below strictly and in order. Do not skip any.

---

## Idempotency Guide

If the project already contains a valid v2 memory system (`.ai/` with 5 files, `decisions.md` has header, `active_context.md` has 6 sections), **do not regenerate**. Instead: run Phase 1 (scan) → Phase 2 (Grill Me only for gaps) → Phase 3 (update only changed sections) → Phase 4 (verify). Never overwrite user content without explicit confirmation. This guide applies for maintenance: fixing broken format, verifying integrity, or adding information after substantial changes.

---

# PHASE 1: Analysis & Discovery

## 1.1 Collision Detection

Before any content scanning, check whether the project already contains:

- An `AGENTS.md` file at the root.
- An `.ai/` folder with memory files.
- Any alternative memory system (e.g., `memory-bank/`, `.kilocode/`, loose notes in `.context/`, etc.).
- Any IDE-specific rules or system prompt file that may overlap (`CLAUDE.md`, `.cursor/rules/`, `.windsurfrules`, `GEMINI.md`, `.github/copilot-instructions.md`).

If any are found, **log the finding** for mandatory discussion during Phase 2 (Grill Me). Do not overwrite or delete anything during this phase.

## 1.2 Environment Scan

Use the native file tools available in your environment (e.g., Antigravity: `list_dir`, `view_file`, `grep_search`; Claude Code: `ls` / `read` / `grep`; Cursor: `list_directory` / `read_file`; Codex: equivalent shell tools). **Always exclude from scanning:** `.git/`, `node_modules/`, `dist/`, `build/`, `vendor/`, `.venv/`, `__pycache__/`, `target/`, and any artifact or package cache directory. Scanning depth depends on the project state:

- **Project with documentation:** Read `.md` files (README, specs, implementation plans), key configs (`package.json`, `requirements.txt`, `pyproject.toml`, etc.). **Capture a real directory listing with limited depth (e.g., `list_dir` recursive, max 3 levels) as input for the directory tree in `project_knowledge.md`.**
- **Project with code but no documentation:** Explore the directory structure, read main entry points and key modules to infer architecture, stack, and patterns. **Capture a real directory listing with limited depth (e.g., `list_dir` recursive, max 3 levels) as input for the directory tree in `project_knowledge.md`.**
- **Small project (few files but real code):** **Capture a real directory listing** as above.
- **Empty or near-empty project (< 2 code files):** Log that no usable context was found. Ask the user whether they want to initialize the memory system from scratch *(recommend starting from an implementation plan or structured specification file before generating the memory)*. Do NOT generate a directory tree — the structure will change too much.

## 1.3 Findings Declaration

Stop and respond in the chat with a structured summary in **bullet points** covering:

- Detected project type (language, framework, apparent purpose).
- Documentation found and its quality/completeness.
- Collisions detected (pre-existing memory files, if applicable).
- Information gaps identified that will require interrogation.

Do not generate any files during this phase.

---

# PHASE 2: Interrogation ("Grill Me")

Interrogate the user to resolve all ambiguity before generating the files.

## 2.1 Format

Prioritize using interactive question tools (e.g., `ask_question`) to present questions with selectable options and default recommendations whenever the environment supports tool-calling. If the environment limits the number of questions per call, split them into two thematic batches: **Batch 1** — Project scope, stack, versioning, platforms, CI/CD; **Batch 2** — Memory system configuration (autonomy level, synchronization rules). If tool-calling for questions is unavailable, send a numbered list in the chat. Each question must include a recommended answer or default value. If the information was already discovered during Phase 1, **do not ask — use it directly** and declare it as a confirmed finding.

## 2.2 Mandatory Categories

If Phase 1 did not yield clear information on the following points, it is **mandatory** to ask about them:

1. **Main objective and project scope** (Core Functionalities / MVP).
2. **Tech stack and tools** (Languages, Frameworks, Databases).
3. **Versioning system** (SemVer, CalVer, etc. If they don't have one, suggest SemVer and wait for approval).
4. **Target platforms or deployment environment** (OS, Cloud, Mobile, Web).
5. **CI/CD flow, required testing, or validation methods.**
6. **Autonomy level for `project_knowledge.md`:** Ask whether the AI should update `project_knowledge.md` autonomously without prior confirmation when changes occur (Recommended: `Prior confirmation: ❌ No` for rapid development), or if the AI must propose changes in chat and wait for human approval (`Prior confirmation: ✅ Yes, always`).
7. **Immediate Documentation Synchronization:** Ask whether to enforce the strict synchronization rule: any modification to code, UI/styles, scripts, or configuration must immediately update the relevant memory files in the same response/turn.

8. **Initial project version:** Ask what version the project is currently at if not defined in the project (e.g., `v0.1.0`, `v1.0.0`). This answer will be used as the initial entry header in `changelog.md`. Do not default or invent a version.
9. **`.ai/` Git versioning:** Ask whether the user wants to version the `.ai/` folder in Git (recommended for teams and continuity) or keep it local via `.gitignore`.
10. **Client auto-loads `AGENTS.md`:** Check whether the user's IDE/client auto-loads `AGENTS.md` at session start. If not, offer to inject a 3-line stub into the client's rules file (e.g., `CLAUDE.md`, `.cursor/rules/`, `GEMINI.md`) pointing to the Context Protocol (optional).

The agent may formulate additional questions at its discretion on areas such as: performance or security constraints, external integrations, data models, code conventions, or any aspect needed to generate a high-quality memory.

## 2.3 Collision Resolution

If a pre-existing `AGENTS.md` or another memory system was detected during Phase 1, explicitly discuss with the user:

- Which rules from the original file to preserve (those that do not conflict with the new memory system).
- Which previous memory systems to deprecate.
- Confirm that a backup of the original `AGENTS.md` will be created before overwriting.
- **Faithful data migration:** If previous memory files exist (e.g., `memory-bank/`), read them in full before generating the new system. Transfer all relevant content completely — do not summarize, condense, or discard any information. Zero data loss is mandatory in migrations.

## 2.4 Incomplete Responses

If the user does not answer all mandatory questions, the agent must:

1. Use sensible defaults for unanswered project-context questions (categories 1–5) and explicitly declare which defaults were assumed.
2. **Never assume defaults** for memory-configuration questions (categories 6–7: autonomy level, documentation synchronization). These must be answered explicitly — re-ask once if skipped.

## 2.5 Mandatory Pause

Wait for the user's explicit confirmation before advancing to generation. Do not proceed to Phase 3 without a green light.

---

# PHASE 3: Memory System Generation

Physically generate all 5 files on disk using `write_to_file` (or the native write tool available in your environment — `write_to_file`, `write_file`, `write`, or equivalent shell redirection). If a previous `AGENTS.md` exists, create a backup (`AGENTS.backup.md`) first before overwriting.

> **Tool Fallbacks:** If `grep` is unavailable, use the environment's native search (e.g., `grep_search`, `search`, `find_in_files`, or read the file and search in memory). If `list_dir` is unavailable, use the native directory listing tool (`ls`, `dir`, `list_directory`). If `write_to_file` is unavailable, use the native write tool (`write_file`, `write`, `create_file`). The skill must work with whatever tools the host environment provides.

> **Critical Language Rule:** `AGENTS.md` is always written in **technical English**. The remaining 4 files inside `.ai/` are always written in the **user's native language** (e.g., Spanish, English, Portuguese, etc.), regardless of the language of this skill document. **Structural tokens (headings, field names, state labels) are FIXED in English** — only prose/content is in the user's native language. This ensures grep, verification, and tooling remain stable across languages.

## 3.1 `AGENTS.md` — Agent Constitution

- **Location:** Project root.
- **Language:** Strictly **TECHNICAL ENGLISH** (regardless of conversation language).
- **Who modifies it post-creation:** Human only (or AI under explicit human instruction). The AI never edits this file on its own initiative.

### Minimum Required Structure:

**`## Role & Identity`**
Define the agent's technical profile for this project:

- Role title (e.g., *Senior Python Engineer*, *Full-Stack Architect*).
- Project-specific expertise stack.
- Primary objective for each work session.
- Sub-section `### Core Competencies` listing critical knowledge areas.

**`## The Context Protocol`**
Mandatory initialization ritual at the start of every session.

> **Session definition:** A session is a new conversation instance with the agent in this project. A new chat window or API call constitutes a new session; an IDE restart without a new conversation does not.

1. Read `AGENTS.md` (this file — if not auto-loaded by the environment, read it explicitly).
2. Read `.ai/project_knowledge.md` (foundational encyclopedia).
3. Read `.ai/active_context.md` (current dynamic state).
4. Acknowledge synchronization by emitting `[Context: Active]` as the first line of the response.

**Session Close Protocol:** When the agent detects that a session is ending (implementation plan completed, important task finished, or user signals closure), it must **propose** running the close procedure: execute the Task Close Checklist, persist any pending decisions to `decisions.md`, update `active_context.md`, and produce a 6-section handoff summary. Do not wait for a magic phrase — detect contextually and suggest closure.

> `changelog.md` is **NOT** included in the startup reading. It is only consulted upon explicit request by the human. The changelog grows without limit by design; including it in the mandatory reading would consume tokens unnecessarily.

**`## Memory Routing`**

Route every piece of information with one question: "What does a future agent need this for?"

| If it answers... | It goes to | Lifetime |
| --- | --- | --- |
| "What is true right now / what do I do next?" | `.ai/active_context.md` | Current phase only |
| "Why is it this way? What must not be redone or reopened?" | `.ai/decisions.md` | Until superseded |
| "What happened and when?" | `.ai/changelog.md` | Forever (append-only) |
| "How is the project built?" (stack, structure, conventions) | `.ai/project_knowledge.md` | Until the architecture changes |
| "How must the agent behave?" | `AGENTS.md` | Human-edited only |

`active_context.md` is a handoff note for the next task, not a history. If an item describes the past and is not needed to continue, it does not belong there.

**`## Decision Capture`**

Write to `.ai/decisions.md` in the same turn when any of these happens. Do not wait to be asked and do not postpone to session end:
- A design, architecture, tool, library, or convention is chosen after weighing options.
- The user confirms ("do that", "agreed"), rejects ("no, X instead"), or states a lasting preference ("always do it this way").
- The user issues a persistent instruction ("don't forget that...", "remember that...", "always ensure...") — these are treated as lasting preferences.
- A bug is fixed and the root cause is non-obvious, or an approach is tried and discarded (Technical Discard).
- A non-obvious gotcha, limitation, or environment fact is discovered.

**Admission Test** — Record only if **both** are true:
| Check | Question |
|-------|----------|
| 1. Relevance | Could ignoring this lead someone to a worse choice later? |
| 2. Unrecoverable | Is this **not** recoverable from code, git history, or changelog? |

> If unsure → write the **one-line form** instead of skipping.

**Conflict Surfacing & Deduplication** — Before writing, `grep` `decisions.md` for the same `Topic`:
| Scenario | Action |
|----------|--------|
| Same Topic, more detail | Edit existing entry in place. |
| Changed course (new decision contradicts old) | Create new entry; mark old as `[REPLACED->D-NN]`. |
| Reverses an **Active** architecture/convention decision | **Ask user first** (one line), then proceed. |
| Any other case | Proceed and report in one line. |

**`## Retrieval Order`**

Before taking a design decision, or when the user asks **"what did we do"**, **"how did we solve"**, **"remember"**, **"continue as before"**, **"as we agreed"**, **"as discussed"**, **"per our decision"**, **"following our previous choice"**, or any phrase referencing a prior decision/conversation, search in this order and stop at the first hit: `active_context.md` (Should already be loaded) → decision headings (`grep "^### D-"`) then open the matching entry → `changelog.md` by keyword or ID (avoid loading the full file unless necessary).

**`## Active Context Hygiene`**

> **Handoff Note definition:** `active_context.md` is a **session-to-session handoff note**, not a history or changelog. Its purpose is to give the next agent/session the minimal context to continue working: current objective, project state, key changes (max 10), active bugs only, next steps, and key files. It must stay under 125 lines. Past items that are not needed to continue belong in `changelog.md` (archival) or `decisions.md` (reasoning).

`active_context.md` starts with a metadata header, followed by `## Current Objective` as the first section (the goal of the current phase). Check these signals whenever you update the file, finish a task, or the user changes direction. If any is true and the current work is not a direct continuation of `Current Objective`, propose archiving in ONE line and wait for approval:
1. A plan, phase, or large task was just completed.
2. The user moved to a different topic, module, or working folder than `Current Objective`.
3. The file exceeds 125 lines.
4. Resolved or finished items are still listed.

Archiving procedure (non-destructive): (a) append a summary of the finished phase to the unversioned block of `changelog.md` under `### Update YYYY-MM-DD`; (b) make sure durable decisions are already in `decisions.md`; (c) rewrite `active_context.md` keeping only the Mandatory Remnant plus the new `Current Objective`; (d) confirm in one line. Never assign a version number.

**`## Context Reset Recovery`**

If you detect a compaction, summary injection, or context reset: (1) before anything else, write the current state into `active_context.md` and any pending decision into `decisions.md`; (2) re-read the Context Protocol files; (3) continue the task and emit `[Context: Active]`.

**`## Task Close Checklist`**

After each task, ask silently: Did we decide, confirm, or reject something? Did we learn something non-obvious or fix a bug with a root cause? Did the user state a lasting preference? Did the phase end? If yes to any, apply the matching rule above now. Memory work is bookkeeping: it never replaces the answer, and any memory report to the user is one line at most.

**`## Anti-Error Rules & Development Standards`**
Critical rules derived from real project errors and safety invariants. Organize them into numbered sub-sections by area (Safety, State, Logging, UX, Architecture, etc.).

*Mandatory Foundational Rule (always included in all projects):*

- **Zero Destructive Deletion / Mandatory Recycle Bin:** Permanent or forced deletions are strictly forbidden (`rm`, `rm -rf`, `del`, `Remove-Item -Force`, `unlink`, `shutil.rmtree`). Files may only be discarded if explicitly ordered by the user, and ALWAYS sent to the system Recycle Bin (in Windows via PowerShell `[Microsoft.VisualBasic.FileIO.FileSystem]::DeleteFile($path, 'OnlyErrorDialogs', 'SendToRecycleBin')` or moving to `_trash/`), or the native OS equivalent.

- **No Secrets in Memory Files:** Never write API keys, tokens, passwords, credentials, or any secret value into the 5 memory files. Reference them only by variable name or file location (e.g., "`API_KEY` — see `.env`").

*Conditional Rules (derived from Grill Me):*

- If configured in Grill Me: **Documentation Synchronization Rule:** Any change to code, styles, configuration, scripts, or interface behaviors must immediately be reflected in relevant memory files (`project_knowledge.md` and/or `active_context.md`) in the same response/turn.

If the project is new and has no error history, populate remaining sub-sections with code conventions and standards agreed upon during the Grill Me.

**`## Memory Maintenance Protocol`**
Explicit instructions on how the AI must maintain the project memory. Must include:

*Update rules table:*

| File | Who updates | When | Prior confirmation |
| --- | --- | --- | --- |
| `AGENTS.md` | Human only (or AI under explicit human instruction) | Philosophy or global rule changes | N/A |
| `project_knowledge.md` | AI proposes → human approves (or AI autonomously, as agreed in Grill Me) | Architectural changes, new stack, design decisions | As configured in Phase 2 |
| `active_context.md` | AI autonomously | Upon completing a **significant task** (see definition below) | ❌ No |
| `decisions.md` | AI autonomously | When Decision Capture conditions are met | ❌ No |
| `changelog.md` | AI drafts → human reviews | When closing a version or under partial archival | ✅ Yes, always |

*Definition of "Significant Task" (for `active_context.md` updates):* A task is significant if it meets **at least one** of the following criteria:

> **Proactive Archival Threshold:** At ~100 lines, warn the user and recommend archival before hitting the 125-line hard limit.

- Modified or created at least one file containing business logic, architecture, configuration, or UI/interface.
- Resolved or identified a registered bug (`ID-XX`).
- Introduced, removed, or changed a dependency, tool, or technology in the stack.
- Changed a design decision or added a Technical Discard.
- Produced a result visible to the end user (new feature, behavior change, fix).

> If **Immediate Documentation Synchronization** was enabled during Grill Me, this threshold does not apply — `active_context.md` is updated on every response/turn that modifies any file.

*Archival Rules* (`active_context.md` → `changelog.md`): Triggered by AI proposal, human approval. Two valid paths:

1. *Version close:* The human declares the close. Move all accumulated content from `active_context.md` for the closing version into a new entry in the changelog. Any Technical Discards accumulated during the session must be consolidated into `decisions.md`, not into `changelog.md`.
2. *Partial archive:* The AI proposes moving specific content (phase complete, topic changed, file >125 lines, RESOLVED/WONTFIX bugs still listed in Active Bugs). Human approves. Move only the indicated content to the active unversioned block (`## [Unversioned] — in progress`).

*Mandatory Remnant Rule:* `active_context.md` **must never be left empty** after an archival or version close. It must permanently retain:

1. Current project status and a 1–3 line summary of the last state.
2. Active bugs and technical debt section (`## Active Bugs & Technical Debt`).
3. Prioritized pending tasks for the next session (`## Next Steps`).
4. Last Bug ID tracker: `Last Bug ID: ID-XX` (set to `ID-00` if no bugs have been registered yet). This prevents ID reuse when `changelog.md` is not loaded at startup.

*Bug IDs:* Global sequential ID system (`ID-01`, `ID-02`...). IDs are permanent: never reassigned or reused after a bug is resolved. Referenced in the changelog with the format `[Resolves ID-XX]`.

*Chronological Session Separation:* When updating `active_context.md` or `changelog.md`, NEVER overwrite or merge the date of changes from previous sessions. If adding changes from a new session to an existing version, group them under a sub-heading with the date (e.g., `### Update YYYY-MM-DD`) to preserve the real chronological history.

*Versioning (Immutable Human Authority):* The version number is ALWAYS assigned exclusively by the human. The AI **must never** assign, infer, propose, increment, or change any version number autonomously — including after a version close, archival, or major feature completion. The AI must read and use the last version explicitly stated by the user and treat it as frozen until the human explicitly declares otherwise.

**`## Canonical Documentation`**
Include an explicit map of the memory system files and their purpose:

- `AGENTS.md` → The core constitution containing the agentic rules and the memory maintenance protocol for this project. Modified by the human (or AI under explicit human instruction).
- `.ai/project_knowledge.md` → Foundational project encyclopedia.
- `.ai/active_context.md` → Live state of the current phase (handoff note).
- `.ai/decisions.md` → Structured decisions, discards, discoveries with lifecycle and conflict surfacing.
- `.ai/changelog.md` → Chronological history (append-only, consulted on demand).

If migrated from a previous system, include a deprecation note (e.g., `memory-bank/ → DEPRECATED. Do not read or update.`).

**Merging with pre-existing rules:** If there was a previous `AGENTS.md`, the memory system sections (Context Protocol, Memory Maintenance Protocol, Canonical Documentation) take absolute priority. User rules that do not conflict are integrated under the corresponding sections (typically under Anti-Error Rules or as additional sections).

---

## 3.2 `.ai/project_knowledge.md` — Foundational Encyclopedia

- **Location:** `.ai/project_knowledge.md` (create the `.ai/` directory if it does not exist).
- **Language:** The user's native language.

### Minimum Required Structure:

- Metadata header: `> **Current Version:** vX.Y.Z (human-assigned, never modified by AI)` — placed at the very top of the file so the agent reads the active version without consulting `active_context.md`.
- `## Design & Product Philosophy` — Why the project exists, what problems it solves, what user experience is sought.
- `## Tech Stack` — Exhaustive list of the stack with versions and justifications. Format: bullets, not prose.
- `## Project Structure` — **Mandatory section.** Commented directory tree in a `text` code block using box-drawing characters (`├──`, `│`, `└──`, `│   `). Built from a real directory listing taken in this phase (`list_dir` or equivalent), never from memory. Rules:
  1. Root line: project folder name followed by `/`.
  2. List ALL **relevant** directories (exclude noise: `.git`, `node_modules`, `dist`, `build`, `vendor`, `.venv`, `__pycache__`, `target`, caches; also exclude empty dirs and dirs with only non-useful content).
  3. Every directory line gets a trailing `#` comment (≤12 words) describing its purpose and key contents.
  4. Under each directory, list **relevant files** using the same box-drawing style. Each file line gets a trailing `#` comment. Include: entry points, key configs, canonical docs, core modules, main scripts. Omit: lockfiles, generated output, bulk assets, test files, minor utilities; collapse repeated files into one line (`*.png`).
  5. Annotate special directories in the comment: gitignored, generated, backups, trash, read-only, source of truth.
  6. Beyond 4 levels deep, collapse with `...` and a comment.
  7. Keep in sync in the same turn whenever a directory or relevant file is created, moved, or deleted. This is factual maintenance and is exempt from the `project_knowledge.md` approval setting.
- `## Architecture` — Single Responsibility Table (`Component | Single Responsibility | Critical Restriction`).
- `## Design Decisions Pointer` — Single line: `> See .ai/decisions.md for all design decisions, technical discards, discoveries, and conventions with lifecycle tracking.`
- `## Data Flow` *(optional, recommended for complex projects)* — Diagram (Mermaid or other) showing the lifecycle of a typical system operation, allowing the AI to understand the flow without reading code.

---

## 3.3 `.ai/active_context.md` — Live State (Handoff Note)

- **Location:** `.ai/active_context.md`.
- **Language:** The user's native language.

### Minimum Required Structure:

- Metadata header: `> **Last updated:** YYYY-MM-DD | **Version:** vX.Y.Z | **Last Bug ID:** ID-XX`
- `## Current Objective` — **Anchor for archival detection.** A short prose summary (1–3 sentences) of the phase goal and working folder, followed by bullet points detailing specific objectives (short, one per bullet).
- `## Current State` — A short prose summary (1–3 sentences) of the project's health, followed by bullet points for key details (stability, blockers, performance notes, etc.).
- `## Current Phase Changes` — A brief introductory sentence, then bullet points (max 10). Each bullet: file path + brief reason for change. Extended reasoning goes to `decisions.md`.
- `## Active Bugs & Technical Debt` — Each entry includes: status (`[OPEN]`/`[MITIGATED]`), one-line description of the problem/impact, affected file(s), and root cause if known. `RESOLVED`/`WONTFIX` move to changelog on next archive.
- `## Next Steps` — Numbered prioritized list (one line each).
- `## Key Files in Play` — List of actively edited/relevant files (soft limit 12), each with a one-line purpose (equivalent to Engram's `Relevant Files`).

> **Hard limit:** File must not exceed 125 lines. **Proactive threshold:** At ~100 lines, warn the user and recommend archival. When updating, check the four archival signals (phase complete, topic changed, file >125 lines, RESOLVED/WONTFIX bugs still listed in Active Bugs). If any is true and work is not a direct continuation of `Current Objective`, propose archiving in one line and wait for approval. Never assign a version number.

---

## 3.4 `.ai/decisions.md` — Structured Decisions

- **Location:** `.ai/decisions.md`.
- **Language:** The user's native language.

### Minimum Required Structure:

- Metadata header: `> **Last updated:** YYYY-MM-DD | **Last decision:** D-00`
- Quick reference: `grep "^### D-"` lists all decisions with state. Replaced/Obsolete are preserved, never deleted.
- Each decision as a level-3 heading with permanent ID and state:
  ```markdown
  ### D-01 [ACTIVE] Choose Zustand over Redux
  - **Topic:** architecture/state-global
  - **Type:** decision | discard | discovery | convention | preference
  - **Date:** YYYY-MM-DD
  - **What:** one sentence on what was decided.
  - **Why:** motivation and discarded alternatives with reasons.
  - **Where:** affected files or paths.
  - **Learned:** gotchas or surprises (omit if not applicable).
  - **Reviewed:** YYYY-MM-DD (optional)
  ```
- Short form allowed for quick captures:
  ```markdown
  ### D-02 [ACTIVE] Avoid polling in proxy (short form)
  - **Topic:** architecture/proxy · **Type:** discard · **Date:** YYYY-MM-DD · Caused port 9194 blocking; uses event instead.
  ```
- Heading states: `[ACTIVE]`, `[REPLACED->D-NN]`, `[OBSOLETE]`.
- **Rule:** Update `Last decision` in header on every new `D-NN`. Mark `Reviewed` when closing a version.
- **Rule:** Generate only the header and quick-reference line. Do not invent decisions. IDs are permanent (like Bug IDs).
- **Conflict surfacing:** Before writing, grep for the same `Topic`. Same decision with more detail → edit in place. Changed course → new entry + mark old as `[REPLACED->D-NN]`. If reversing an Active architecture/convention decision, ask user first; otherwise proceed and report.

---

## 3.5 `.ai/changelog.md` — Chronological History

- **Location:** `.ai/changelog.md`.
- **Language:** The user's native language.
- **Not read at session startup.** Only consulted upon explicit human request.

### Minimum Required Structure:

- Group changes under version headings (`## [vX.Y.Z] - YYYY-MM-DD`) and/or session dates (`### Update YYYY-MM-DD`).
- Order: append-only in content; newest blocks inserted at the top. Historical entries are never modified or overwritten; new entries are always inserted at the top of the file. The immutability principle applies to existing entries, not to insertion position.
- **Changelog principle:** summarize phases, do not log tool calls.
- For a brand-new project, initialize with a base entry using the version declared by the user in Grill Me (category 8). Never default or infer a version number.
- References to resolved bugs use the format `[Resolves ID-XX]`.

**Unversioned block for partial archives:** A block `## [Unversioned] — in progress` is maintained at the top of the changelog (newest entries first) to receive summaries from partial archives without the AI inventing version numbers. When the human closes a version, this block is renamed to `## [vX.Y.Z] - YYYY-MM-DD`. The AI never assigns version numbers.

---

### Canonical Tree Example (Phase 3.2)

```text
project-root/
├── src/                    # Core application source
│   ├── components/         # UI components
│   ├── services/           # Business logic & API
│   │   └── api.ts          # API client & endpoints
│   └── utils/              # Helpers & shared utilities
├── tests/                  # Test suites
├── docs/                   # Documentation
├── package.json            # Dependencies & scripts
└── README.md               # Project overview
```

# PHASE 4: Post-Generation Review

After creating all 5 files:

1. Run `list_dir` on `.ai/` and verify the existence of `AGENTS.md` at the project root to confirm all files were written correctly.
2. **Verification checklist (all must pass):**
   - `project_knowledge.md` contains `## Project Structure` that matches a real `list_dir` listing (excluding noise dirs).
   - `decisions.md` exists with header and quick-reference line (`grep "^### D-"`).
   - `active_context.md` has `## Current Objective` filled in (not empty).
   - `AGENTS.md` contains `## Memory Routing`, `## Decision Capture`, `## Retrieval Order`, `## Active Context Hygiene`, `## Context Reset Recovery`, `## Task Close Checklist`.
   - No secrets in any memory file (scan for API keys, tokens, passwords).
3. Request a review from the user of the generated system, focusing especially on `project_knowledge.md` (the foundational encyclopedia). Explicitly ask whether any data is incorrect, incomplete, or if they wish to add, remove, or correct sections.
4. Apply any requested corrections before declaring the installation complete.

---

# Operational Constraints

1. **Mandatory physical writing:** Do not just display content in the chat. Use `write_to_file` to create each file on disk.
2. **Backup before overwrite:** If a previous `AGENTS.md` exists, create `AGENTS.backup.md` before replacing it.
3. **Rule priority in merges:** When merging with a pre-existing `AGENTS.md`, the memory system sections take absolute priority over the previous file's rules.
4. **Human versioning:** Never invent, infer, or propose version numbers. Ask the user if the current version is unknown.
5. **Post-installation autonomy:** Once generated, the memory system survives autonomously thanks to the directives written into `AGENTS.md`. This skill does not intervene in subsequent maintenance.
6. **Zero Destructive Deletion:** The agent must never use forced or permanent deletion commands (`rm`, `rm -rf`, `del`, `Remove-Item -Force`, `unlink`, `shutil.rmtree`). All removals must go to the system Recycle Bin or `_trash/`.

---

# APPENDIX: Migration v1 → v2 (for projects already using v1.0)

When the skill is invoked in a project that already has the v1.0 memory system (4 files), perform the following migration **before** declaring installation complete:

1. **Backup:** Create `AGENTS.backup.md` from the existing `AGENTS.md` (standard rule).
2. **Create `decisions.md`:** Generate the new file with header and quick-reference line. **Find the historical decisions section in `project_knowledge.md` (search for headings containing "decision", "design", "historical", "discard", or "archived" — case-insensitive) and confirm with the user before moving. Move the entire matched section textually into `decisions.md`**, assigning sequential `D-NN` IDs without rewriting content (zero data loss). Leave a pointer in `project_knowledge.md`: `> See .ai/decisions.md for all design decisions, technical discards, discoveries, and conventions with lifecycle tracking.`
3. **Restructure `active_context.md`:**
   - Content describing the past or resolved items → append to the unversioned block in `changelog.md` under `### Update YYYY-MM-DD — phase name`.
   - Decisions with extended reasoning → ensure they're in `decisions.md` (already done in step 2).
   - Remaining content → rewrite into the new structure: `## Current Objective` (short prose + bullets), `## Current State` (short prose + bullets), `## Current Phase Changes` (intro + bullets, max 10), `## Active Bugs & Technical Debt` (status + description + file + root cause), `## Next Steps` (numbered), `## Key Files in Play` (one-line purpose each, soft limit 12).
4. **Generate `## Project Structure`:** Run a real `list_dir` (recursive, max 3-4 levels, excluding noise) and build the commented tree per the rules in Phase 3.2.
5. **Update `AGENTS.md`:** Insert the new sections (`## Memory Routing`, `## Decision Capture`, `## Retrieval Order`, `## Active Context Hygiene`, `## Context Reset Recovery`, `## Task Close Checklist`, updated `## Memory Maintenance Protocol` table with `decisions.md` row, updated `## Canonical Documentation` with 5 files). Preserve user's custom rules from the original `AGENTS.md` under appropriate sections.
6. **Update `changelog.md`:** Ensure the unversioned block `## [Unversioned] — in progress` exists at the top for receiving partial archives.
7. **Verify:** Run the Phase 4 checklist on the migrated system.
