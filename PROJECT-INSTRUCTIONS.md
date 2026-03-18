# Claude Project Instructions
> This file is read automatically via MCP filesystem when Claude is triggered.
> The Project Instructions field in each Claude project contains one line pointing here.

---

## ONE-LINER for Project Instructions Field

Copy this into every Claude project's **Project Instructions** field (update the path to match your system):

```
When asked to "update the knowledge document", read [your-claude-memory-path]/PROJECT-INSTRUCTIONS.md and follow the instructions there exactly.
```

Example paths:
- Windows (hyphen): `C:\Claude-Code\claude-memory\PROJECT-INSTRUCTIONS.md`
- Windows (space): `C:\Claude Code\claude-memory\PROJECT-INSTRUCTIONS.md`
- Mac/Linux: `~/claude-memory/PROJECT-INSTRUCTIONS.md`

---

## Update Procedure (Claude follows this when triggered)

CRITICAL: Always confirm the exact local path before writing files.
Replace `[claude-memory-path]` below with your actual path.

When asked to **"update the knowledge document"**:

1. Review the ENTIRE conversation history in this project
2. Identify what's new since the last update — new decisions, what worked, what didn't, key learnings
3. Read the existing doc: `[claude-memory-path]/[filename].md` (see filename table below)
4. Generate a COMPLETE updated knowledge doc with all sections filled in
5. Write the updated doc to `[claude-memory-path]/[filename].md`
6. Read `[claude-memory-path]/SHARED-LEARNINGS.md`
7. For each category with new learnings, read only that category file in `shared-learnings/`, add entries (no duplicates), write it back
8. Write updated SHARED-LEARNINGS back to `[claude-memory-path]/SHARED-LEARNINGS.md`
9. Confirm BOTH files written
10. Tell user: *"Done — run 'push claude-memory to GitHub' in Claude Code"*

---

## Per-Project Filenames

Update this table with your own projects:

| Project | Filename |
|---------|----------|
| [Project 1 Name] | `project-1.md` |
| [Project 2 Name] | `project-2.md` |
| [Project 3 Name] | `project-3.md` |

---

## Key Learnings Categories (Section 9)

Tag every learning with one of your categories. Default set:
`[Deployment]` `[Claude/AI]` `[Architecture]` `[Workflow]`

Add domain-specific categories as needed:
`[Pine Script]` `[Trading Logic]` `[IB/TWS]` — for trading projects
`[Data Science]` `[ML/AI]` `[Data Pipeline]` — for data projects
`[Mobile]` `[iOS]` `[Android]` — for mobile projects

---

## Cross-Project Knowledge

SHARED-LEARNINGS.md contains distilled learnings from ALL projects.

**When answering any question:**
- If the question relates to Deployment, Architecture, Claude/AI, Workflow, or your domain categories — read SHARED-LEARNINGS.md first
- Use it to provide answers informed by lessons learned across all projects

**When starting a new feature or debugging:**
- Read SHARED-LEARNINGS.md to surface relevant prior learnings before writing any code
- Read the specific project doc for deeper context on decisions

---

## Cross-Project Queries

From any project:
> *"Check the claude-memory repo and tell me how we handled [topic] in [other project]"*

Claude reads `[claude-memory-path]/[project].md` directly and answers with full context.

---

## Claude Code Push Command

After any update:
> *"Push claude-memory to GitHub"*
