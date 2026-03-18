# Claude Cross-Project Memory System

A lightweight system that gives Claude persistent, cross-project memory using GitHub + MCP filesystem access.

## The Problem

Claude projects are isolated. Knowledge from one project — decisions made, lessons learned, patterns discovered — is invisible to every other project. Every new project starts from zero.

## The Solution

A shared GitHub repository of structured knowledge documents that any Claude project can read and write via MCP filesystem access.

```
Any Claude Project
      ↓
"update the knowledge document"
      ↓
Claude reads chat history → updates [project].md → merges into SHARED-LEARNINGS.md
      ↓
"push claude-memory to GitHub"  (in Claude Code)
      ↓
Knowledge available across ALL projects forever
```

## How It Works

1. **One repo** — a private GitHub repo called `claude-memory` cloned locally
2. **One doc per project** — structured knowledge document capturing decisions, what works, what doesn't, key learnings
3. **One shared file** — `SHARED-LEARNINGS.md` aggregates cross-project insights by category
4. **One trigger phrase** — *"update the knowledge document"* at the end of any significant session
5. **One push command** — *"push claude-memory to GitHub"* in Claude Code

## What's in This Repo

```
claude-cross-project-memory-system/
├── README.md                         ← You are here
├── PROJECT_KNOWLEDGE_TEMPLATE.md     ← Template for new project docs
├── SHARED-LEARNINGS-template.md      ← Empty SHARED-LEARNINGS to start with
├── PROJECT-INSTRUCTIONS.md           ← Procedure Claude follows when triggered
└── skill/
    ├── SKILL.md                      ← Installable Claude skill
    └── references/
        └── setup.md                  ← Step-by-step setup guide
```

## Quick Start

**30-minute one-time setup:**

1. Create a private GitHub repo called `claude-memory`
2. Clone it locally
3. Add the local path to Claude Desktop's MCP filesystem config
4. Copy the template files from this repo into your `claude-memory` folder
5. Add one line to each Claude project's Project Instructions field
6. Generate your first project knowledge doc

See `skill/references/setup.md` for the complete step-by-step guide.

## The Trigger Phrase

Inside any Claude project, at the end of a significant session:

> *"Update the knowledge document"*

Claude will:
- Read the entire project chat history
- Update the project knowledge doc
- Merge new learnings into SHARED-LEARNINGS.md
- Write both files directly to your local `claude-memory` folder

Then in Claude Code:

> *"Push claude-memory to GitHub"*

Done. Two commands. Everything saved.

## Cross-Project Queries

From any project:

> *"Check the claude-memory repo — how did we handle [topic] in [other project]?"*

Claude reads the relevant project doc and answers with full context from your actual history.

## Key Learning Categories

SHARED-LEARNINGS.md organizes insights into 7 categories that cover most technical projects:

- `[Pine Script]` — TradingView strategy patterns (or your domain equivalent)
- `[Trading Logic]` — Domain-specific business logic
- `[IB/TWS]` — API/integration patterns
- `[Deployment]` — Infrastructure, hosting, CI/CD
- `[Claude/AI]` — Prompt engineering, AI architecture
- `[Architecture]` — System design, data flow
- `[Workflow]` — Development process, tooling, productivity

Customize these categories for your own domain.

## Why This Works

- **No new tools** — GitHub + MCP filesystem you likely already have
- **No uploads** — Claude reads files live from disk via MCP
- **No maintenance** — One trigger phrase handles everything
- **Compounds over time** — Every session makes the system smarter
- **Works everywhere** — Inside projects, outside projects, Claude Code

## Contributing

If you improve the system, PRs welcome. Particularly interested in:
- Additional category sets for different domains (web dev, data science, etc.)
- Alternative knowledge doc templates
- Workflow variations that work better for different use cases

---

*Built by a trader with 25+ years institutional experience who uses Claude Code daily to build automated trading systems — without writing a single line of code manually.*
