<div align="center">
  <br>
  <a href="https://yaislab.org">
    <img src="https://raw.githubusercontent.com/xnexuzx/lmstudio-telegram-bot/main/res/github/yais-bot.png" alt="nxz ai memory system logo" width="200" height="200">
  </a>
  <h1>🧠 NXZ AI Memory System Skill</h1>
  <p>
    <b>A robust, agentic memory system skill for AI coding assistants.</b><br>
    This skill guides the AI to autonomously initialize or migrate a standardized 4-file memory architecture in your projects, ensuring the AI maintains context, tracks bugs, and adheres to your design decisions across multiple coding sessions.
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

## 🧠 The 4-File Architecture

When triggered, the AI will create/update the following files:

| File | Role | Location |
|---|---|---|
| `AGENTS.md` | **The Constitution:** Core rules and the Memory Maintenance Protocol. | Root |
| `project_knowledge.md` | **Static Encyclopedia:** Architecture, stack, and historical design decisions. | `.ai/` |
| `active_context.md` | **Live State:** Current bugs, recent changes, and next steps. | `.ai/` |
| `changelog.md` | **Chronological History:** Append-only log of past versions and sessions. | `.ai/` |

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

#### Target Global Directories by Platform:

**1. Cursor**
- Global Directory: `~/.cursor/skills/`
- Final Path: `~/.cursor/skills/nxz-ai-memory-system/SKILL.md`

**2. Antigravity IDE**
- Global Directory: `~/.gemini/config/skills/`
- Final Path: `~/.gemini/config/skills/nxz-ai-memory-system/SKILL.md`

**3. Claude Code (CLI)**
- Global Directory: `~/.claude/skills/`
- Final Path: `~/.claude/skills/nxz-ai-memory-system/SKILL.md`

**4. Codex (OpenAI CLI)**
- Global Directory: `~/.codex/skills/`
- Final Path: `~/.codex/skills/nxz-ai-memory-system/SKILL.md`

## 🛠️ Usage

1. Open your project in your AI IDE.
2. In the chat, prompt the agent:
   > *Initialize the nxz memory system in this project.*
3. **The Grill Me Phase:** The AI will scan your project and ask you a series of questions (Stack, Goals, Versioning, CI/CD) to ensure the memory is perfectly tailored to your needs.
4. **Review & Approve:** Once the AI generates the files, review them. From then on, the AI will autonomously maintain its memory across sessions!

## ⚙️ Features
- **Collision Detection:** Safely detects if you already have memory files (like `memory-bank/`) and helps you migrate.
- **Strict Protocols:** Forces the AI to read the memory before acting, preventing hallucinations.
- **Chronological Separation:** Enforces real chronological logging in your changelogs without merging dates.

---
*Created by [xnexuzx](https://github.com/xnexuzx)*
