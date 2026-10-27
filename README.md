<div align="center">
  <br>
  <a href="https://yaislab.org">
    <img src="https://raw.githubusercontent.com/xnexuzx/lmstudio-telegram-bot/main/res/github/yais-bot.png" alt="nxz ai memory system logo" width="200" height="200">
  </a>
  <h1>🧠 NXZ AI Memory System Skill</h1>
  <p>
    <b>A robust, agentic memory system skill for AI coding assistants.</b><br>
    This skill guides the AI to autonomously initialize or migrate a standardized 5-file memory architecture in your projects, ensuring the AI maintains context, tracks bugs, captures decisions with lifecycle, and adheres to your design decisions across multiple coding sessions.
  </p>
  <br>
  
  <div align="center">
    <img src="https://img.shields.io/badge/By%3A-YAIS%20LAB-%23FFD700?style=flat&link=https%3A%2F%2Fyaislab.org" alt="YAIS LAB">
    <img src="https://img.shields.io/github/stars/xnexuzx/nxz-ai-memory-system" alt="GitHub stars">
    <img src="https://img.shields.io/badge/Framework-Agnostic-CF4141?style=flat" alt="Agnostic">
    <img src="https://img.shields.io/badge/Format-Markdown-3776AB?style=flat&logo=markdown&logoColor=white" alt="Markdown">
  </div>
</div>

### 🌟 Design Philosophy: Lightweight & Universal

The **NXZ AI Memory System** is built to be as simple and frictionless as possible while remaining highly effective.

- **Universally Compatible:** Because it relies entirely on standard Markdown files and directives based on the `AGENTS.md` standard, it is completely agnostic. It can be applied to any type of project, framework, or language.
- **Model Agnostic:** The architecture is intentionally lightweight, making it perfectly usable not only for frontier-level AI models, but also highly effective for smaller, local models running on your own hardware.

## 🆕 What's New in v2.0.0 🎉

### 📁 New File: `decisions.md` — Structured Decision Capture

A dedicated file for decisions, technical discards, discoveries, and conventions with full lifecycle tracking:

- **Permanent IDs** (`D-01`, `D-02`...) with states: `[ACTIVE]`, `[REPLACED->D-NN]`, `[OBSOLETE]`
- **Topic keys** for upsert/deduplication and conflict surfacing
- **Admission test** (relevance + unrecoverability) prevents noise
- **One-line short form** for quick captures
- Auto-updated `Last decision` header and `Reviewed` timestamp on version close

### 🏗️ `AGENTS.md` — 6 New Protocol Sections

| Section | Purpose |
| --------- | --------- |
| `## Memory Routing` | Route info by "what does a future agent need this for?" |
| `## Decision Capture` | Write decisions in same turn; admission test + conflict surfacing |
| `## Retrieval Order` | `active_context.md` → decisions → changelog (on trigger phrases: "what did we do", "how did we solve", "remember", "continue as before", "as we agreed", "as discussed", "per our decision", or any reference to prior decisions) |
| `## Active Context Hygiene` | Archival signals, 125-line limit, remnant rule |
| `## Task Close Checklist` | Silent self-check after each task |

### 🔄 Redesigned `active_context.md` — Handoff Note (Not History)

- **Hard 125-line limit** with proactive ~100-line archival threshold
- **6 structured sections**: `Current Objective` (anchor), `Current State`, `Current Phase Changes` (max 10), `Active Bugs & Technical Debt`, `Next Steps`, `Key Files in Play` (soft limit 12)
- **AI-proposed archival** with human approval (replaces human-only archival)
- **Mandatory Remnant Rule** never left empty after archival

### 📋 Enhanced `changelog.md` — Chronological History

- **Unversioned block** `## [Unversioned] — in progress` for partial archives (AI never invents versions)
- **Chronological session separation** dates preserved across sessions
- **Append-only content, newest blocks at top** immutable history
- **Changelog principle**: "summarize phases, do not log tool calls"

### 🛡️ Resilience & Operational Improvements

- **Tool fallbacks** (`grep`→native search, `list_dir`→shell, `write_to_file`→native write)
- **Idempotency guide** for maintenance runs (fix format, verify integrity, add info)
- **Structural tokens fixed in English** (headings, fields, states) prose in user's native language
- **Migration v1→v2** with flexible heading search + user confirmation (zero data loss)
- **Session close protocol** contextual detection (plan complete, task done) → propose full close with handoff
- **Auto-update protocol** version compare, confirm before apply, never downgrade without approval+backup

## 🧠 The 5-File Architecture

When triggered, the AI will create/update the following files:

| File | Role | Location |
| --- | --- | --- |
| `AGENTS.md` | **The Constitution:** Core rules, Memory Routing, Decision Capture, Retrieval Order, Context Hygiene, Reset Recovery, Task Close Checklist. | Root |
| `project_knowledge.md` | **Foundational Encyclopedia:** Architecture, stack, directory tree (`## Project Structure`), data flow. Historical decisions moved to `decisions.md`. | `.ai/` |
| `active_context.md` | **Live State (Handoff Note):** `## Current Objective` anchor, phase state, max 10 changes, active bugs only, next steps, key files. Hard limit 125 lines. | `.ai/` |
| `decisions.md` | **Structured Decisions:** Decisions, discards, discoveries, conventions with lifecycle (`[ACTIVE]`/`[REPLACED]`/`[OBSOLETE]`), conflict surfacing, topic keys. | `.ai/` |
| `changelog.md` | **Chronological History:** Append-only with version headings + unversioned block `## [Unversioned] — in progress` for partial archives. | `.ai/` |

## 🚀 Installation & Compatibility

This skill is a pure Markdown file (`SKILL.md`), making it universally compatible with any modern AI coding assistant.

### Option A: Agentic Auto-Install (For any AI IDE)

Simply copy this prompt and paste it into your AI assistant (Cursor, Antigravity, Claude Code, Codex):
> *Navigate to `https://github.com/xnexuzx/nxz-ai-memory-system`. Read the `SKILL.md` file in the repository, understand its instructions, and install this skill in my current IDE environment according to its standard rules or skills format.*

*(Note: Your AI assistant must have web browsing and file-writing capabilities enabled for auto-installation).*

### Option B: Manual Installation (Global Skills Path)

Depending on whether you downloaded the full repository or just the file, choose the appropriate method:

- **Method 1 (Repository Folder):** Copy the entire `nxz-ai-memory-system` folder into the target global skills directory.
- **Method 2 (Single File):** Create a folder named `nxz-ai-memory-system` inside the target global skills directory and place `SKILL.md` inside it.

#### Target Global Directories by Platform

#### 1. Cursor

- Global Directory: `~/.cursor/skills/`
- Final Path: `~/.cursor/skills/nxz-ai-memory-system/SKILL.md`

#### 2. Antigravity IDE

- Global Directory: `~/.gemini/config/skills/`
- Final Path: `~/.gemini/config/skills/nxz-ai-memory-system/SKILL.md`

#### 3. Claude Code (CLI)

- Global Directory: `~/.claude/skills/`
- Final Path: `~/.claude/skills/nxz-ai-memory-system/SKILL.md`

#### 4. Codex (OpenAI CLI)

- Global Directory: `~/.codex/skills/`
- Final Path: `~/.codex/skills/nxz-ai-memory-system/SKILL.md`

## 🛠️ Usage

1. Open your project in your AI IDE.
2. In the chat, prompt the agent:
   > *Initialize the nxz memory system in this project.*
3. **The Grill Me Phase:** The AI will scan your project and ask you a series of questions (Stack, Goals, Versioning, CI/CD) to ensure the memory is perfectly tailored to your needs.
4. **Review & Approve:** Once the AI generates the files, review them. From then on, the AI will autonomously maintain its memory across sessions!
5. **Checking for Updates:** If you ever want to check for or pull upstream updates to the skill:
   > *Check if there is an update for the nxz-ai-memory-system skill from its repository and update it if available.*

## ⚙️ Features

- **Collision Detection & Migration:** Safely detects if you already have memory files (like `memory-bank/`) and helps you migrate, including v1→v2 zero-loss migration.
- **Strict Protocols:** Forces the AI to read the memory before acting, preventing hallucinations. Includes Memory Routing, Decision Capture, Retrieval Order, Context Hygiene, Reset Recovery, and Task Close Checklist.
- **Structured Decision Capture:** Decisions, technical discards, discoveries, and conventions with lifecycle states (`[ACTIVE]`, `[REPLACED]`, `[OBSOLETE]`), topic keys for upserts, and conflict surfacing. **Auto-loaded on trigger phrases** ("remember", "continue as before", "as we agreed", "as discussed", "per our decision", or any reference to prior decisions/conversations) so the AI recalls past choices without reminders.
- **Active Context as Handoff Note:** `## Current Objective` anchor with hard 125-line limit, archival triggered by AI proposal + human approval (not human-only), unversioned changelog block for partial archives.
- **Verified Directory Tree:** `## Project Structure` built from real `list_dir` output with strict rules, verified in Phase 4.
- **Chronological Separation:** Enforces real chronological logging in changelogs without merging dates. Unversioned block prevents AI from inventing versions.
- **Zero Destructive Deletion:** Mandates system Recycle Bin protection across all agent actions.
- **Interactive Customization:** Adapts memory autonomy, documentation sync, and client rules stub (Engram resilience layer 3) during setup via interactive questions.
- **Context Reset Recovery:** Two-step recovery protocol (persist → re-read → continue) if compaction/summary injection detected.

## 🗑️ Uninstall

Remove the `nxz-ai-memory-system/` folder from your IDE's global skills directory. Memory files inside your projects (`.ai/`, `AGENTS.md`) remain intact and fully functional after removal.

---
*Created by [xnexuzx](https://github.com/xnexuzx)*
