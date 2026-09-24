---
name: nxz-ai-memory-system
description: Invoke this skill when the user requests to implement, initialize, create, or migrate the structured agentic memory system of 4 files (nxz ai memory system) in their current project, or when requested to check for updates or sync this skill from its official repository.
---

# Role: Agentic Memory System Architect

> **Repo (v1.0.0):** <https://github.com/xnexuzx/nxz-ai-memory-system> | **Raw:** `https://raw.githubusercontent.com/xnexuzx/nxz-ai-memory-system/main/SKILL.md`  
> *Self-update:* If asked to check updates or sync, fetch raw upstream, compare diff/version, and apply changes upon human approval.

Objective: Initialize or migrate the "nxz ai memory system" in the current project. The system consists of 4 files with complementary roles that enable an agentic AI to work with continuity across sessions:

| File | Role | Location |
| --- | --- | --- |
| `AGENTS.md` | Agent constitution (rules, protocol). Modified by the human (or AI under explicit human instruction). | Project root |
| `project_knowledge.md` | Foundational encyclopedia (architecture, stack, design decisions). Updated per autonomy level configured during setup. | `.ai/` |
| `active_context.md` | Live state of the current version. | `.ai/` |
| `changelog.md` | Chronological history by version (append-only). | `.ai/` |

Follow the phases below strictly and in order. Do not skip any.

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

- **Project with documentation:** Read `.md` files (README, specs, implementation plans), key configs (`package.json`, `requirements.txt`, `pyproject.toml`, etc.).
- **Project with code but no documentation:** Explore the directory structure, read main entry points and key modules to infer architecture, stack, and patterns.
- **Empty or near-empty project:** Log that no usable context was found. Ask the user whether they want to initialize the memory system from scratch *(recommend starting from an implementation plan or structured specification file before generating the memory)*.

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

Physically generate all 4 files on disk using `write_to_file`. If a previous `AGENTS.md` exists, create a backup (`AGENTS.backup.md`) first before overwriting.

> **Critical Language Rule:** `AGENTS.md` is always written in **technical English**. The remaining 3 files inside `.ai/` are always written in the **user's native language** (e.g., Spanish, English, Portuguese, etc.), regardless of the language of this skill document.

## 1. `AGENTS.md` — Agent Constitution

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

**Session Close Protocol:** If the user announces the end of a session (e.g. "one last thing", "let's end the session", "goodbye", "done here", "that's all for today/now", "I have to go", etc...) or issues a "save state" directive, and a significant task was completed or is still in progress: immediately update `active_context.md` with the current state/turn before the conversation ends. Do not wait for the next session.

> `changelog.md` is **NOT** included in the startup reading. It is only consulted upon explicit request by the human. The changelog grows without limit by design; including it in the mandatory reading would consume tokens unnecessarily.

**`## Anti-Error Rules & Development Standards`**
Critical rules derived from real project errors and safety invariants. Organize them into numbered sub-sections by area (Safety, State, Logging, UX, Architecture, etc.).

*Mandatory Foundational Rule (always included in all projects):*

- **Zero Destructive Deletion / Mandatory Recycle Bin:** Permanent or forced deletions are strictly forbidden (`rm`, `rm -rf`, `del`, `Remove-Item -Force`, `unlink`, `shutil.rmtree`). Files may only be discarded if explicitly ordered by the user, and ALWAYS sent to the system Recycle Bin (in Windows via PowerShell `[Microsoft.VisualBasic.FileIO.FileSystem]::DeleteFile($path, 'OnlyErrorDialogs', 'SendToRecycleBin')` or moving to `_trash/`), or the native OS equivalent.

- **No Secrets in Memory Files:** Never write API keys, tokens, passwords, credentials, or any secret value into the 4 memory files. Reference them only by variable name or file location (e.g., "`API_KEY` — see `.env`").

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
| `changelog.md` | AI drafts → human reviews | When closing a version or under partial archival | ✅ Yes, always |

*Definition of "Significant Task" (for `active_context.md` updates):* A task is significant if it meets **at least one** of the following criteria:

- Modified or created at least one file containing business logic, architecture, configuration, or UI/interface.
- Resolved or identified a registered bug (`ID-XX`).
- Introduced, removed, or changed a dependency, tool, or technology in the stack.
- Changed a design decision or added a Technical Discard.
- Produced a result visible to the end user (new feature, behavior change, fix).

> If **Immediate Documentation Synchronization** was enabled during Grill Me, this threshold does not apply — `active_context.md` is updated on every response/turn that modifies any file.

*Archival Rules* (`active_context.md` → `changelog.md`): Triggered ONLY by the human, never automatic. Two valid paths:

1. *Version close:* The human declares the close. Move all accumulated content from `active_context.md` for the closing version into a new entry in the changelog. Any Technical Discards accumulated during the session must be consolidated into `project_knowledge.md` (`## Historical Design Decisions & Technical Discards`), not into `changelog.md`.
2. *Partial archive:* The human requests moving specific content without changing versions. Move only the indicated content to the current version entry.

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
- `.ai/active_context.md` → Live state of the current version.
- `.ai/changelog.md` → Chronological history (append-only, consulted on demand).

If migrated from a previous system, include a deprecation note (e.g., `memory-bank/ → DEPRECATED. Do not read or update.`).

**Merging with pre-existing rules:** If there was a previous `AGENTS.md`, the memory system sections (Context Protocol, Memory Maintenance Protocol, Canonical Documentation) take absolute priority. User rules that do not conflict are integrated under the corresponding sections (typically under Anti-Error Rules or as additional sections).

---

## 2. `.ai/project_knowledge.md` — Foundational Encyclopedia

- **Location:** `.ai/project_knowledge.md` (create the `.ai/` directory if it does not exist).
- **Language:** The user's native language.

### Minimum Required Structure:

- Metadata header: `> **Current Version:** vX.Y.Z (human-assigned, never modified by AI)` — placed at the very top of the file so the agent reads the active version without consulting `active_context.md`.
- `## Design & Product Philosophy` — Why the project exists, what problems it solves, what user experience is sought.
- `## Tech Stack` — Exhaustive list of the stack with versions and justifications. Format: bullets, not prose.
- `## Architecture` — Commented directory tree (in a `text` code block) and a Single Responsibility Table (`Component | Single Responsibility | Critical Restriction`).
- `## Historical Design Decisions & Technical Discards` — Numbered list of non-negotiable decisions with the *why* behind each one. Must explicitly record Technical Discards (approaches, libraries, or patterns explored that failed or were discarded, along with the technical rationale) to prevent future agents from repeating failed paths or reverting hard-learned lessons.
- `## Data Flow` *(optional, recommended for complex projects)* — Diagram (Mermaid or other) showing the lifecycle of a typical system operation, allowing the AI to understand the flow without reading code.

---

## 3. `.ai/active_context.md` — Live State

- **Location:** `.ai/active_context.md`.
- **Language:** The user's native language.

### Minimum Required Structure:

- Metadata header: `> **Last updated:** YYYY-MM-DD | **Version:** vX.Y.Z | **Last Bug ID:** ID-XX`
- `## Current State` — 1–3 lines describing the project's health.
- `## Recent Changes` — List of significant changes in the current version. Each item must be specific (name files) and justified (explain the *why*).
- `## ⚠️ Active Bugs & Technical Debt` — Structured format per bug:

  ```markdown
  - **[STATUS] ID-XX: Descriptive name**
    - *Symptom:* What the user or system observes.
    - *Affected file(s):* `path/to/file`
    - *Root cause:* Technical explanation (if known).
  ```

  Possible statuses: `[OPEN]`, `[MITIGATED]`, `[RESOLVED]`, `[WONTFIX]`, `[DUPLICATE]`, `[NOT_A_BUG]`.
- `## Next Steps` — Numbered list of prioritized pending tasks.

> **Size guidance (non-binding):** `## Recent Changes` should ideally not exceed ~15 items per version cycle. If it grows beyond this, the agent should proactively suggest a version close or partial archival to the human — without executing it autonomously.

---

## 4. `.ai/changelog.md` — Chronological History

- **Location:** `.ai/changelog.md`.
- **Language:** The user's native language.
- **Not read at session startup.** Only consulted upon explicit human request.

### Minimum Required Structure:

- Group changes under version headings (`## [vX.Y.Z] - YYYY-MM-DD`) and/or session dates (`### Update YYYY-MM-DD`).
- Order: newest entry first (prepend-only). Historical entries are never modified or overwritten; new entries are always inserted at the top of the file. The immutability principle applies to existing entries, not to insertion position.
- For a brand-new project, initialize with a base entry using the version declared by the user in Grill Me (category 8). Never default or infer a version number.
- References to resolved bugs use the format `[Resolves ID-XX]`.

---

# PHASE 4: Post-Generation Review

After creating all 4 files:

1. Run `list_dir` on `.ai/` and verify the existence of `AGENTS.md` at the project root to confirm all files were written correctly.
2. Request a review from the user of the generated system, focusing especially on `project_knowledge.md` (the foundational encyclopedia). Explicitly ask whether any data is incorrect, incomplete, or if they wish to add, remove, or correct sections.
3. Apply any requested corrections before declaring the installation complete.

---

# Operational Constraints

1. **Mandatory physical writing:** Do not just display content in the chat. Use `write_to_file` to create each file on disk.
2. **Backup before overwrite:** If a previous `AGENTS.md` exists, create `AGENTS.backup.md` before replacing it.
3. **Rule priority in merges:** When merging with a pre-existing `AGENTS.md`, the memory system sections take absolute priority over the previous file's rules.
4. **Human versioning:** Never invent, infer, or propose version numbers. Ask the user if the current version is unknown.
5. **Post-installation autonomy:** Once generated, the memory system survives autonomously thanks to the directives written into `AGENTS.md`. This skill does not intervene in subsequent maintenance.
6. **Zero Destructive Deletion:** The agent must never use forced or permanent deletion commands (`rm`, `rm -rf`, `del`, `Remove-Item -Force`, `unlink`, `shutil.rmtree`). All removals must go to the system Recycle Bin or `_trash/`.
