# Claude Memory — Setup Guide

## What This System Does

Claude projects are isolated — knowledge from one project is invisible to others. This system solves that by maintaining a shared GitHub repository of structured knowledge documents that any Claude project can read and write via MCP filesystem access.

---

## Prerequisites

- GitHub account
- Claude Desktop with MCP filesystem server configured
- Claude Code (for git push operations)

---

## One-Time Setup (~30 minutes)

### Step 1 — Create a private GitHub repo

1. Go to GitHub → New repository
2. Name it `claude-memory`
3. Set to **Private**
4. Initialize with a README

### Step 2 — Clone locally

```bash
git clone https://github.com/[your-username]/claude-memory.git
```

**Windows examples:**
- `C:\Claude-Code\claude-memory` (recommended — hyphen, no space)
- `C:\Users\[you]\claude-memory`

**Mac/Linux:**
- `~/claude-memory`

> ⚠️ Note your exact path — spaces vs hyphens matter later.

### Step 3 — Add path to Claude Desktop MCP config

**Windows:** Open `%APPDATA%\Claude\claude_desktop_config.json`
**Mac:** Open `~/Library/Application Support/Claude/claude_desktop_config.json`

Add your claude-memory path to the filesystem MCP server args:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "C:\\Claude-Code\\claude-memory",
        "C:\\your-other-dirs"
      ]
    }
  }
}
```

**Restart Claude Desktop** after saving.

### Step 4 — Copy template files into your repo

Copy these files from this public repo into your `claude-memory` folder:

- `PROJECT_KNOWLEDGE_TEMPLATE.md` → your `claude-memory/` folder
- `SHARED-LEARNINGS-template.md` → rename to `SHARED-LEARNINGS.md` in your folder
- `PROJECT-INSTRUCTIONS.md` → your `claude-memory/` folder

**Edit PROJECT-INSTRUCTIONS.md:**
- Replace `[claude-memory-path]` with your actual local path everywhere
- Add your project names and filenames to the Per-Project Filenames table
- Customize the Key Learnings categories for your domain

### Step 5 — Push to GitHub

```bash
cd claude-memory
git add .
git commit -m "Initial claude-memory setup"
git push origin main
```

### Step 6 — Add one line to each Claude project

In each Claude project → Settings → Project Instructions, paste:

```
When asked to "update the knowledge document", read [your-exact-path]/PROJECT-INSTRUCTIONS.md and follow the instructions there exactly.
```

Replace `[your-exact-path]` with your actual local path, e.g.:
- `C:\Claude-Code\claude-memory\PROJECT-INSTRUCTIONS.md`
- `~/claude-memory/PROJECT-INSTRUCTIONS.md`

### Step 7 — Generate your first project knowledge doc

Go to your most important Claude project and say:

> *"Using the PROJECT_KNOWLEDGE_TEMPLATE.md from my claude-memory repo, generate a project knowledge document based on our conversation history in this project."*

Review the generated doc, make any corrections, then say:

> *"Save this as [project-name].md in my claude-memory folder and merge the Key Learnings into SHARED-LEARNINGS.md"*

### Step 8 — Push and repeat

In Claude Code:
> *"Push claude-memory to GitHub"*

Repeat Step 7 for each project. After 3-4 projects, SHARED-LEARNINGS.md becomes genuinely valuable.

---

## Ongoing Workflow

**End of any significant session (inside any Claude project):**
> *"Update the knowledge document"*

Claude automatically:
- Reads the full project chat history
- Updates the project knowledge doc
- Merges new learnings into SHARED-LEARNINGS.md
- Writes both files to your local claude-memory folder

**Then in Claude Code (one command):**
> *"Push claude-memory to GitHub"*

**Cross-project questions (from any project):**
> *"Check the claude-memory repo — how did we handle [topic] in [other project]?"*

---

## Troubleshooting

**Claude saves to wrong path**
Verify your exact path — hyphen (`Claude-Code`) vs space (`Claude Code`) causes failures. Add a CRITICAL PATH comment to your PROJECT-INSTRUCTIONS.md with the exact correct path marked clearly.

**MCP not working inside a Claude project**
- Confirm your claude-memory path is in the MCP filesystem server args
- Restart Claude Desktop after any config changes
- Test by asking Claude to list files in your claude-memory folder

**SHARED-LEARNINGS not being updated**
Check your PROJECT-INSTRUCTIONS.md — steps 6-9 must explicitly read, merge, and write SHARED-LEARNINGS. If any step is missing, Claude may skip it.

**"I can't find the file" errors**
Always use the full absolute path. Relative paths like `./claude-memory` don't work with MCP filesystem.

---

## Customizing for Your Domain

The default categories (`[Deployment]`, `[Claude/AI]`, `[Architecture]`, `[Workflow]`) work for most software projects. Customize by editing SHARED-LEARNINGS.md and PROJECT-INSTRUCTIONS.md:

**Trading/Finance:** Add `[Pine Script]` `[Trading Logic]` `[Broker API]`
**Data Science:** Add `[Data Pipeline]` `[ML/AI]` `[Data Quality]`
**Mobile:** Add `[iOS]` `[Android]` `[Mobile UX]`
**DevOps:** Add `[Infrastructure]` `[Security]` `[Monitoring]`

The system is domain-agnostic — the categories are just organizational labels.
