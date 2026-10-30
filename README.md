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

## 🆕 What's New in v2.1.0 (since v1.0) 🎉

v2.1.0 is the full upgrade from the original 4-file system (v1.0). It includes everything introduced in v2.0.0, refined so that smaller local models can follow it reliably.

### 📊 At a Glance

| Aspect | v1.0 | v2.1.0 |
| --- | --- | --- |
| **Memory files** | 4 | **5** (`decisions.md` added) |
| **How files are generated** | Written by the AI from a prose description | **Copied from literal templates** with `{{MARKERS}}` |
| **Decisions** | Historical appendix inside `project_knowledge.md` | **Dedicated file** with permanent IDs, lifecycle states, and deduplication |
| **Active Context** | ~15 loose items, archived by the human | **6 sections with per-section limits**, archival proposed by the AI and approved by the human |
| **Changelog** | Simple append-only | **Unversioned block**, session dates preserved, explicit version close |
| **Grill Me (Phase 2)** | ~5 questions | **11 categories**, each tagged `[assume default]` or `[no default]` |
| **Versioning** | Human-assigned | Human-assigned, **stored in one place**, never proposed by the AI |
| **Permanent deletion** | Always forbidden | **Your choice** during setup |
| **Migration** | None | **v1→v2 zero-loss migration** |
| **Language** | Mixed | **Structural tokens fixed in English**, content in your language |

### ✨ Highlights

- **📁 New `decisions.md`:** decisions, discards, and preferences get their own file with permanent IDs (`D-01`...) and states (`[ACTIVE]`, `[REPLACED->D-NN]`, `[OBSOLETE]`). The AI checks it before deciding, so settled choices are not reopened.
- **📐 Literal templates:** the AI copies a template for each file and fills its markers, so every installation looks the same, whatever model you use.
- **🏗️ One Memory Protocol in `AGENTS.md`:** clear rules for session start, while working, and after each task. Decisions are saved in the same turn, not at session end.
- **🔄 `active_context.md` as a handoff note:** 6 sections with visible limits. The AI proposes archiving to the changelog when a phase ends; you approve.
- **📋 Safer versioning:** the AI never invents or proposes version numbers. Closing a version is a single message in the chat.
- **⚙️ Tailored setup:** 11 Grill Me questions, including memory autonomy, documentation sync, and optional recoverable deletion (Recycle Bin or `_trash/`).
- **🛡️ Safe migration:** detects existing memory systems, backs up `AGENTS.md`, and migrates v1 projects with zero data loss.

## 🧠 The 5-File Architecture

When triggered, the AI will create/update the following files:

| File | Role | Location |
| --- | --- | --- |
| `AGENTS.md` | **The Constitution:** Role, Memory Protocol (start, while working, after each task, never, files), Memory File Formats, and project rules. | Root |
| `project_knowledge.md` | **Foundational Encyclopedia:** Current version, philosophy, stack, directory tree (`## Project Structure`), architecture, data flow. | `.ai/` |
| `active_context.md` | **Live State (Handoff Note):** 6 sections with per-section limits: objective, state, phase changes, active bugs, next steps, key files. | `.ai/` |
| `decisions.md` | **Structured Decisions:** Decisions, discards, discoveries, conventions, and preferences with lifecycle (`[ACTIVE]`/`[REPLACED->D-NN]`/`[OBSOLETE]`). | `.ai/` |
| `changelog.md` | **Chronological History:** Append-only, newest first, with the `## [Unversioned] — in progress` block for partial archives. | `.ai/` |

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
3. **The Grill Me Phase:** The AI will scan your project and ask you a series of questions (goals, stack, versioning, CI/CD, memory autonomy, documentation sync, recoverable deletion...) to ensure the memory is perfectly tailored to your needs.
4. **Review & Approve:** Once the AI generates the files, review them. From then on, the AI will autonomously maintain its memory across sessions!
5. **Checking for Updates:** If you ever want to check for or pull upstream updates to the skill:
   > *Check if there is an update for the nxz-ai-memory-system skill from its repository and update it if available.*

## ⚙️ Features

- **Collision Detection & Migration:** Safely detects existing memory files (like `memory-bank/`) or IDE rules files and helps you migrate, including a zero-loss v1→v2 migration.
- **Deterministic Output:** Literal templates with markers, resolved Grill Me options, and a Phase 4 checklist.
- **Observable Triggers:** Decisions are captured in the same turn when the user says "always", "never", "remember", accepts or rejects a proposal, or when an option is chosen, discarded, or discovered.
- **Retrieval Before Deciding:** Before a design decision, or when the user refers to past work, the AI checks `active_context.md`, then decision headings, then the changelog.
- **Active Context as Handoff Note:** Per-section limits and AI-proposed archival with human approval. The file is never left empty.
- **Verified Directory Tree:** `## Project Structure` built from a real directory listing (max 3 levels), kept in sync without approval.
- **Human-Only Versioning:** The AI never invents, proposes, or increments version numbers.
- **Optional Recoverable Deletion:** If enabled, permanent deletion commands are forbidden and removals go to the Recycle Bin or `_trash/`. The skill itself never deletes permanently during installation.
- **Context Reset Recovery:** On compaction or summary, the AI saves state and pending decisions first, then re-reads the memory.

## 🗑️ Uninstall

Remove the `nxz-ai-memory-system/` folder from your IDE's global skills directory. Memory files inside your projects (`.ai/`, `AGENTS.md`) remain intact and fully functional after removal.

---
*Created by [xnexuzx](https://github.com/xnexuzx)*
