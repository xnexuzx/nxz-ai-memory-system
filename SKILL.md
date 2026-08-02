---
name: nxz-ai-memory-system
description: Invoke this skill when the user requests to implement, initialize, create, or migrate the structured agentic memory system of 4 files (nxz ai memory system) in their current project. The skill guides the agent through a complete flow — project scanning, collision detection with previous memory systems, exhaustive interrogation (/grill-me) to resolve ambiguities, physical generation of the project memory files (AGENTS.md and the .ai/ directory), and a final joint review with the user.
---

# Role: Agentic Memory System Architect

Objective: Initialize or migrate the "nxz ai memory system" in the current project. The system consists of 4 files with complementary roles that enable an agentic AI to work with continuity across sessions:

| File | Role | Location |
|---|---|---|
| `AGENTS.md` | Agent constitution (rules, protocol). Only modified by the human. | Project root |
| `project_knowledge.md` | Static encyclopedia (architecture, stack, design decisions). | `.ai/` |
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

If any are found, **log the finding** for mandatory discussion during Phase 2 (Grill Me). Do not overwrite or delete anything during this phase.

## 1.2 Environment Scan
Use native tools (`list_dir`, `view_file`, `grep_search`) to explore the project. Scanning depth depends on the project state:

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
Send a numbered list of questions in the chat. Include a recommended answer or default value for each question, so the user can simply reply "yes" or elaborate if they prefer. If the information was already discovered during Phase 1, **do not ask — use it directly** and declare it as a confirmed finding.

## 2.2 Mandatory Categories
If Phase 1 did not yield clear information on the following points, it is **mandatory** to ask about them:
1. **Main objective and project scope** (Core Functionalities / MVP).
2. **Tech stack and tools** (Languages, Frameworks, Databases).
3. **Versioning system** (SemVer, CalVer, etc. If they don't have one, suggest SemVer and wait for approval).
4. **Target platforms or deployment environment** (OS, Cloud, Mobile, Web).
5. **CI/CD flow, required testing, or validation methods.**

The agent may formulate additional questions at its discretion on areas such as: performance or security constraints, external integrations, data models, code conventions, or any aspect needed to generate a high-quality memory.

## 2.3 Collision Resolution
If a pre-existing `AGENTS.md` or another memory system was detected during Phase 1, explicitly discuss with the user:
- Which rules from the original file to preserve (those that do not conflict with the new memory system).
- Which previous memory systems to deprecate.
- Confirm that a backup of the original `AGENTS.md` will be created before overwriting.

## 2.4 Mandatory Pause
Wait for the user's explicit confirmation before advancing to generation. Do not proceed to Phase 3 without a green light.

---

# PHASE 3: Memory System Generation

Physically generate all 4 files on disk using `write_to_file`. If a previous `AGENTS.md` exists, create a backup (`AGENTS.backup.md`) first before overwriting.

> **Critical Language Rule:** `AGENTS.md` is always written in **technical English**. The remaining 3 files inside `.ai/` are always written in the **user's native language** (e.g., Spanish, English, Portuguese, etc.), regardless of the language of this skill document.

## 1. `AGENTS.md` — Agent Constitution
- **Location:** Project root.
- **Language:** Strictly **TECHNICAL ENGLISH** (regardless of conversation language).
- **Who modifies it post-creation:** Only the human. The AI never edits this file.

### Minimum Required Structure:

**`## Role & Identity`**
Define the agent's technical profile for this project:
- Role title (e.g., *Senior Python Engineer*, *Full-Stack Architect*).
- Project-specific expertise stack.
- Primary objective for each work session.
- Sub-section `### Core Competencies` listing critical knowledge areas.

**`## The Context Protocol`**
Mandatory initialization ritual at the start of every session:
1. Read `AGENTS.md` (this file — implicit, the agent is already reading it).
2. Read `.ai/project_knowledge.md` (static encyclopedia).
3. Read `.ai/active_context.md` (current dynamic state).
4. Acknowledge synchronization by emitting `[Context: Active]` as the first line of the response.

> `changelog.md` is **NOT** included in the startup reading. It is only consulted upon explicit request by the human. The changelog grows without limit by design; including it in the mandatory reading would consume tokens unnecessarily.

**`## Anti-Error Rules & Development Standards`**
Critical rules derived from real project errors. Organize them into numbered sub-sections by area (State, Logging, UX, Architecture, etc.). If the project is new and has no error history, populate with the code conventions and development standards agreed upon during the Grill Me.

**`## Memory Maintenance Protocol`**
Explicit instructions on how the AI must maintain the project memory. Must include:

*Update rules table:*

| File | Who updates | When | Prior confirmation |
|---|---|---|---|
| `AGENTS.md` | Human only | Philosophy or global rule changes | N/A |
| `project_knowledge.md` | AI proposes → human approves | Architectural changes, new stack, design decisions | ✅ Yes, always |
| `active_context.md` | AI autonomously | Upon completing any significant task | ❌ No |
| `changelog.md` | AI drafts → human reviews | When closing a version or under partial archival | ✅ Yes, always |

*Archival Rules* (`active_context.md` → `changelog.md`): Triggered ONLY by the human, never automatic. Two valid paths:
1. *Version close:* The human declares the close. Move all accumulated content from `active_context.md` for the closing version into a new entry in the changelog.
2. *Partial archive:* The human requests moving specific content without changing versions. Move only the indicated content to the current version entry.

*Mandatory Remnant Rule:* `active_context.md` **must never be left empty** after an archival. It must retain at least the pending "Next Steps" section, or a 1–3 line summary of the last archived state if no tasks remain.

*Bug IDs:* Global sequential ID system (`ID-01`, `ID-02`...). IDs are permanent: never reassigned or reused after a bug is resolved. Referenced in the changelog with the format `[Resolves ID-XX]`.

*Chronological Session Separation:* When updating `active_context.md` or `changelog.md`, NEVER overwrite or merge the date of changes from previous sessions. If adding changes from a new session to an existing version, group them under a sub-heading with the date (e.g., `### Update YYYY-MM-DD`) to preserve the real chronological history.

*Versioning:* The version number is ALWAYS assigned by the human. The AI never assigns, infers, or proposes a version number. The AI must always assume and use the last version explicitly defined by the user.

**`## Canonical Documentation`**
Include an explicit map of the memory system files and their purpose:
- `AGENTS.md` → The core constitution containing the agentic rules and the memory maintenance protocol for this project. Only modified by the human.
- `.ai/project_knowledge.md` → Static project encyclopedia.
- `.ai/active_context.md` → Live state of the current version.
- `.ai/changelog.md` → Chronological history (append-only, consulted on demand).

If migrated from a previous system, include a deprecation note (e.g., `memory-bank/ → DEPRECATED. Do not read or update.`).

**Merging with pre-existing rules:** If there was a previous `AGENTS.md`, the memory system sections (Context Protocol, Memory Maintenance Protocol, Canonical Documentation) take absolute priority. User rules that do not conflict are integrated under the corresponding sections (typically under Anti-Error Rules or as additional sections).

---

## 2. `.ai/project_knowledge.md` — Static Encyclopedia
- **Location:** `.ai/project_knowledge.md` (create the `.ai/` directory if it does not exist).
- **Language:** The user's native language.

### Minimum Required Structure:
- `## Design & Product Philosophy` — Why the project exists, what problems it solves, what user experience is sought.
- `## Tech Stack` — Exhaustive list of the stack with versions and justifications. Format: bullets, not prose.
- `## Architecture` — Commented directory tree (in a `text` code block) and a Single Responsibility Table (`Component | Single Responsibility | Critical Restriction`).
- `## Historical Design Decisions` — Numbered list of non-negotiable decisions with the *why* behind each one. This is the most important guardrail: it prevents the AI from reverting painfully learned decisions.
- `## Data Flow` *(optional, recommended for complex projects)* — Diagram (Mermaid or other) showing the lifecycle of a typical system operation, allowing the AI to understand the flow without reading code.

---

## 3. `.ai/active_context.md` — Live State
- **Location:** `.ai/active_context.md`.
- **Language:** The user's native language.

### Minimum Required Structure:
- Metadata header: `> **Last updated:** YYYY-MM-DD | **Version:** vX.Y.Z`
- `## Current State` — 1–3 lines describing the project's health.
- `## Recent Changes` — List of significant changes in the current version. Each item must be specific (name files) and justified (explain the *why*).
- `## ⚠️ Active Bugs & Technical Debt` — Structured format per bug:
  ```
  - **[STATUS] ID-XX: Descriptive name**
    - *Symptom:* What the user or system observes.
    - *Affected file(s):* `path/to/file`
    - *Root cause:* Technical explanation (if known).
  ```
  Possible statuses: `[OPEN]`, `[MITIGATED]`, `[RESOLVED]`.
- `## Next Steps` — Numbered list of prioritized pending tasks.

---

## 4. `.ai/changelog.md` — Chronological History
- **Location:** `.ai/changelog.md`.
- **Language:** The user's native language.
- **Not read at session startup.** Only consulted upon explicit human request.

### Minimum Required Structure:
- Group changes under version headings (`## [vX.Y.Z] - YYYY-MM-DD`) and/or session dates (`### Update YYYY-MM-DD`).
- Order: most recent version first.
- For a brand-new project, initialize with a base entry `## [v0.1.0] - Date`.
- References to resolved bugs use the format `[Resolves ID-XX]`.

---

# PHASE 4: Post-Generation Review

After creating all 4 files:
1. Run `list_dir` on `.ai/` and verify the existence of `AGENTS.md` at the project root to confirm all files were written correctly.
2. Request a review from the user of the generated system, focusing especially on `project_knowledge.md` (the static encyclopedia). Explicitly ask whether any data is incorrect, incomplete, or if they wish to add, remove, or correct sections.
3. Apply any requested corrections before declaring the installation complete.

---

# Operational Constraints

1. **Mandatory physical writing:** Do not just display content in the chat. Use `write_to_file` to create each file on disk.
2. **Backup before overwrite:** If a previous `AGENTS.md` exists, create `AGENTS.backup.md` before replacing it.
3. **Rule priority in merges:** When merging with a pre-existing `AGENTS.md`, the memory system sections take absolute priority over the previous file's rules.
4. **Human versioning:** Never invent, infer, or propose version numbers. Ask the user if the current version is unknown.
5. **Post-installation autonomy:** Once generated, the memory system survives autonomously thanks to the directives written into `AGENTS.md`. This skill does not intervene in subsequent maintenance.
