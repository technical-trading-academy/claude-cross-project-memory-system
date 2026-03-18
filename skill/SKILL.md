---
name: claude-memory
description: >
  Cross-project persistent memory system for Claude. Use this skill whenever the user wants to:
  - Set up a shared knowledge base across multiple Claude projects
  - Update a project knowledge document at the end of a session ("update the knowledge document", "update knowledge doc", "save what we learned")
  - Merge new learnings into a shared cross-project knowledge base
  - Query knowledge from other projects ("how did we handle X in another project?", "check what we know about X")
  - Set up the claude-memory system from scratch
  - Understand what was decided or built in a previous session
  This skill should trigger whenever the user mentions "knowledge document", "shared learnings", "cross-project memory", "update the knowledge", or asks Claude to remember something across projects.
---

# Claude Memory — Cross-Project Persistent Knowledge System

## Overview

This skill enables persistent, cross-project memory for Claude by maintaining structured knowledge documents in a GitHub repository. Every project writes its learnings to a shared repo, and every project can read from it — solving Claude's project isolation problem.

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

---

## Where to Start

- **New user setting up the system?** → Read `references/setup.md`
- **Updating knowledge at end of session?** → Follow the [Update Procedure](#update-procedure) below
- **Querying cross-project knowledge?** → Follow the [Query Procedure](#query-procedure) below

---

## Repository Structure

```
claude-memory/                          ← Your private GitHub repo
├── PROJECT-INSTRUCTIONS.md            ← Procedure Claude reads via MCP
├── PROJECT_KNOWLEDGE_TEMPLATE.md      ← Template for new project docs
├── SHARED-LEARNINGS.md                ← Aggregated learnings from ALL projects
└── [project-name].md                  ← One doc per project
```

**CRITICAL: Always confirm the exact local path with the user before writing any files.**
Common variants that cause failures:
- `C:\Claude-Code\claude-memory` (hyphen) vs `C:\Claude Code\claude-memory` (space)
- Forward vs backslash on different OS

---

## Update Procedure

Triggered by: *"update the knowledge document"*

1. **Identify filename** — check `PROJECT-INSTRUCTIONS.md` for the filename table
2. **Read existing doc** — `[path]/[project].md` — note what's already there
3. **Review conversation history** — scan for new decisions, what worked, what didn't, key learnings, open items
4. **Generate updated doc** — be thorough on Section 2 (Decisions), 4 (Works), 5 (Doesn't Work), 9 (Learnings)
5. **Write updated doc** — `[path]/[project].md`
6. **Read SHARED-LEARNINGS** — `[path]/SHARED-LEARNINGS.md`
7. **Identify new learnings** — entries not already present, applicable beyond this project
8. **Merge new learnings** — add to correct category table, no duplicates
9. **Write SHARED-LEARNINGS** — `[path]/SHARED-LEARNINGS.md`
10. **Confirm** — tell user: *"Done — run 'push claude-memory to GitHub' in Claude Code"*

---

## Query Procedure

Triggered by: cross-project questions, "how did we handle X?", "check what we know about X"

1. Read `SHARED-LEARNINGS.md` — scan the relevant category
2. If more detail needed, read the specific project doc
3. Answer with context from prior learnings, citing the source project

**Proactively read SHARED-LEARNINGS when:**
- Questions about Deployment, Architecture, Claude/AI, Workflow, or domain-specific categories
- Starting a new feature where prior learnings would help
- Debugging issues that may have been solved before

---

## Key Learnings Categories

Default categories — customize for your domain:

| Category | Contents |
|----------|----------|
| `[Deployment]` | Servers, CI/CD, infrastructure, hosting |
| `[Claude/AI]` | Prompt engineering, AI architecture, Claude patterns |
| `[Architecture]` | System design, data flow, integration patterns |
| `[Workflow]` | Development process, tooling, productivity |

Domain-specific examples:
- Trading: `[Pine Script]` `[Trading Logic]` `[IB/TWS]`
- Data: `[Data Pipeline]` `[ML/AI]` `[Data Science]`
- Mobile: `[iOS]` `[Android]` `[Mobile]`

---

## Project Instructions Field Setup

Each Claude project needs ONE LINE in its Project Instructions field:

```
When asked to "update the knowledge document", read [your-path]/PROJECT-INSTRUCTIONS.md and follow the instructions there exactly.
```

Claude reads the file live from disk via MCP — no uploads, no manual file management.

---

For full setup instructions, read `references/setup.md`.
