# Project Initialization Guide

**For coding agents**: Follow this guide to initialize a new project. Ask the user the questions below, then set up the appropriate structure.

---

## Step 1: Gather Information

Ask the user these questions (adapt phrasing naturally):

### Q1: Project Type
"What kind of project is this?"
- **Greenfield**: New feature build with clear milestones
- **Maintenance**: Ongoing system/tool that will evolve over time
- **Complex**: Multi-contributor project needing PR workflows
- **Script**: Quick utility, minimal structure needed

### Q2: Task Management
"How do you want to track work?"
- **GSD**: Phase-based milestones (best for greenfield builds)
- **bd (beads)**: Issue tracking with dependencies (best for ongoing work)
- **Both**: GSD for major features, bd for bugs/discovered work
- **None**: Just git commits, no formal tracking

### Q3: Git Workflow
"How should we handle git?"
- **Simple**: master/main branch only, direct commits
- **Beads sync**: main + beads-sync branch (keeps issues off main)
- **PR workflow**: main + dev + beads-sync, PRs for significant changes

### Q4: Documentation Level
"How much documentation structure?"
- **Minimal**: Just CLAUDE.md
- **Standard**: CLAUDE.md + .ai/architecture.md
- **Full**: CLAUDE.md + AGENTS.md + .ai/ + .claude/commands/

### Q5: Project Context
"Brief description of what you're building?"
(Used to customize architecture docs and CLAUDE.md)

---

## Step 2: Apply Configuration

Based on answers, create the appropriate structure:

### Greenfield + GSD + Simple Git + Minimal Docs
```
project/
├── CLAUDE.md           # From snippets/claude-md/gsd.md
└── .planning/
    ├── PROJECT.md      # User's project description
    ├── ROADMAP.md      # Empty, to be filled via /gsd:create-roadmap
    ├── STATE.md        # Initial state
    └── config.json     # {"mode": "yolo", "depth": "comprehensive"}
```

### Maintenance + Beads + Beads Sync + Standard Docs
```
project/
├── CLAUDE.md           # From snippets/claude-md/beads.md
├── .ai/
│   └── architecture.md # From snippets/ai-directory/architecture.md
└── .beads/             # Created via `bd init`
```

### Complex + Beads + PR Workflow + Full Docs
```
project/
├── CLAUDE.md           # From snippets/claude-md/beads.md
├── AGENTS.md           # From snippets/agents-md/full.md
├── .ai/
│   ├── architecture.md
│   └── conventions.md
├── .beads/             # Created via `bd init`
└── .claude/
    └── commands/
        ├── commit.md   # From snippets/git-commands/commit.md
        ├── pr.md
        └── wip.md
```

---

## Step 3: Initialize Systems

### If using beads:
```bash
bd init
bd config set sync.branch beads-sync
# Create beads-sync branch if using that workflow
git checkout --orphan beads-sync
git add .beads/
git commit -m "Initialize beads tracking"
git checkout main  # or master
```

### If using GSD:
```bash
mkdir -p .planning/phases
# Create initial files (PROJECT.md, ROADMAP.md, STATE.md, config.json)
```

### Git setup:
```bash
git init  # if not already
git add .
git commit -m "Initialize project structure"
```

---

## Step 4: Customize Content

Replace placeholders in created files:
- `{{PROJECT_NAME}}` - Project name
- `{{PROJECT_DESCRIPTION}}` - Brief description
- `{{DATE}}` - Current date

---

## Step 5: Verify & Handoff

Confirm with user:
1. Show them what was created: `ls -la` or tree view
2. Explain next steps based on their workflow
3. If beads: "Run `bd ready` to see available work"
4. If GSD: "Run `/gsd:create-roadmap` to define phases"

---

## Quick Reference: Snippet Locations

| Need | Snippet Path |
|------|--------------|
| Minimal CLAUDE.md | snippets/claude-md/minimal.md |
| Beads CLAUDE.md | snippets/claude-md/beads.md |
| GSD CLAUDE.md | snippets/claude-md/gsd.md |
| Full AGENTS.md | snippets/agents-md/full.md |
| Architecture template | snippets/ai-directory/architecture.md |
| Conventions template | snippets/ai-directory/conventions.md |
| /commit command | snippets/git-commands/commit.md |
| /pr command | snippets/git-commands/pr.md |
| /wip command | snippets/git-commands/wip.md |

---

## Notes

- This file (INIT.md) can be deleted after initialization, or kept for reference
- The template at ~/code/template should not be modified during project init
- If you notice useful patterns missing, create an issue: `cd ~/code/template && bd create "Add: ..."`
