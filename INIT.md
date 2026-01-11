# Project Initialization Guide

**For any coding agent**: Follow this guide to initialize a new project. Use a purpose-first approach - understand what the user wants to accomplish, then set up the appropriate structure.

---

## Step 1: Understand Purpose

### Ask the Primary Question

**"What do you want to accomplish with this project?"**

Listen for signals and infer the appropriate archetype:

| User Says | Archetype | Default Setup |
|-----------|-----------|---------------|
| "Build X", "Create Y", clear deliverable | **Build** | GSD + dev branch |
| "Maintain", "manage", "evolve over time" | **Maintain** | beads + beads-sync |
| "Research", "investigate", "understand" | **Research** | beads + research notes |
| "Run automatically", "cron", "scheduled" | **Automate** | beads + logs + config |
| "Learn", "experiment", "try out" | **Learn** | minimal setup |
| "Document", "wiki", "knowledge base" | **Document** | beads + docs structure |
| "Team", "contributors", "PR workflow" | **Collaborate** | beads + full docs + PR |
| Quick task, one-off, simple | **Quick** | CLAUDE.md only |

### Task Systems: GSD vs Beads

Two systems appear above. Here's when to use each:

| System | Use When | How It Works |
|--------|----------|--------------|
| **GSD** | Building something new with clear milestones | Phase-based roadmap in `.planning/`. Work through phases sequentially. Best for greenfield projects where you know the destination. |
| **beads** | Ongoing work, discovered issues, dependencies | Issue tracking in `.beads/`. Create issues as you find them, track blockers. Best for maintenance, research, or when scope emerges over time. |

**Rule of thumb**: If you can write a roadmap upfront → GSD. If work will be discovered → beads.

### Confirm Your Understanding

**"Based on that, I'd suggest a [archetype] setup with [key features]. Does that sound right?"**

- If yes → proceed with archetype defaults
- If no → ask refinement questions (see questions/init-questions.md)

### Get Project Description

**"What's a one-sentence description?"**

Used for CLAUDE.md header and documentation.

---

## Step 2: Apply Archetype Configuration

### Build (Greenfield)

```
project/
├── CLAUDE.md              # From snippets/claude-md/gsd.md
└── .planning/
    ├── PROJECT.md         # User's project description
    ├── ROADMAP.md         # Via /gsd:create-roadmap
    ├── STATE.md           # Initial state
    └── config.json        # {"mode": "yolo", "depth": "comprehensive"}
```

**Git**: main + dev branches
**Next step**: "Run `/gsd:create-roadmap` to define phases"

---

### Maintain (Ongoing)

```
project/
├── CLAUDE.md              # From snippets/claude-md/beads.md
├── .ai/
│   └── architecture.md    # From snippets/ai-directory/architecture.md
└── .beads/                # Via `bd init`
```

**Git**: main + beads-sync branches
**Next step**: "Run `bd ready` to see available work"

---

### Research (Investigation)

```
project/
├── CLAUDE.md              # From snippets/claude-md/research.md
├── .ai/
│   └── research/
│       ├── questions.md   # From snippets/ai-directory/research/questions.md
│       ├── findings.md    # From snippets/ai-directory/research/findings.md
│       └── sources.md     # From snippets/ai-directory/research/sources.md
└── .beads/                # Via `bd init`
```

**Git**: main + beads-sync branches
**Next step**: "Add your research questions to .ai/research/questions.md"

---

### Automate (Agent-Managed)

```
project/
├── CLAUDE.md              # From snippets/claude-md/automate.md
├── .ai/
│   ├── schedule.md        # From snippets/ai-directory/automation/schedule.md
│   ├── triggers.md        # From snippets/ai-directory/automation/triggers.md
│   └── outputs.md         # From snippets/ai-directory/automation/outputs.md
├── config/
│   └── .gitkeep
├── logs/
│   └── .gitkeep
└── .beads/                # Via `bd init`
```

**Git**: main + beads-sync branches
**Next step**: "Define your schedule in .ai/schedule.md"

---

### Learn (Experimentation)

```
project/
├── CLAUDE.md              # From snippets/claude-md/minimal.md
└── scratch/
    └── .gitkeep
```

**Git**: main branch only
**Next step**: "Start experimenting!"

---

### Document (Knowledge Base)

```
project/
├── CLAUDE.md              # From snippets/claude-md/beads.md
├── .ai/
│   ├── structure.md       # How content is organized
│   └── conventions.md     # From snippets/ai-directory/conventions.md
├── docs/
│   └── index.md
└── .beads/                # Via `bd init`
```

**Git**: main + beads-sync branches
**Next step**: "Start building your documentation in docs/"

---

### Collaborate (Multi-Contributor)

```
project/
├── CLAUDE.md              # From snippets/claude-md/beads.md
├── AGENTS.md              # From snippets/agents-md/full.md
├── .ai/
│   ├── architecture.md
│   └── conventions.md
├── .beads/                # Via `bd init`
└── .claude/
    └── commands/          # From snippets/claude-code/commands/
        ├── commit.md
        ├── pr.md
        ├── release.md
        ├── status.md
        ├── wip.md
        └── sync.md
```

**Git**: main + dev + beads-sync branches
**Next step**: "Run `bd ready` to see available work"

---

### Quick (One-Off)

```
project/
└── CLAUDE.md              # From snippets/claude-md/minimal.md
```

**Git**: main branch only
**Next step**: "Let's get to work!"

---

## Step 3: Initialize Systems

### If using beads:

```bash
bd init
bd config set sync.branch beads-sync

# Create beads-sync branch (orphan)
git checkout --orphan beads-sync
git rm -rf .
git add .beads/
git commit -m "Initialize beads tracking"
git checkout main  # or master
```

### If using GSD:

```bash
mkdir -p .planning/phases
# Create PROJECT.md, ROADMAP.md, STATE.md, config.json
```

### If using dev branch workflow:

```bash
git checkout -b dev
git push -u origin dev
```

### Git initial commit:

```bash
git add .
git commit -m "Initialize project structure

Co-Authored-By: Claude <noreply@anthropic.com>"
```

---

## Step 4: Claude Code Setup (Optional)

If user wants Claude Code slash commands:

1. Copy commands from `snippets/claude-code/commands/` to `.claude/commands/`
2. Set up hooks per `snippets/claude-code/hooks.md`
3. Verify with `/commit` or `/status`

---

## Step 5: Customize & Verify

### Replace placeholders:

- `{{PROJECT_NAME}}` - Project name
- `{{PROJECT_DESCRIPTION}}` - Brief description
- `{{DATE}}` - Current date

### Show user what was created:

```bash
tree -a -I '.git' .
```

### Explain next steps based on archetype.

---

## Quick Reference: Snippet Locations

| Need | Snippet Path |
|------|--------------|
| Minimal CLAUDE.md | snippets/claude-md/minimal.md |
| Beads CLAUDE.md | snippets/claude-md/beads.md |
| GSD CLAUDE.md | snippets/claude-md/gsd.md |
| Research CLAUDE.md | snippets/claude-md/research.md |
| Automate CLAUDE.md | snippets/claude-md/automate.md |
| Full AGENTS.md | snippets/agents-md/full.md |
| Architecture | snippets/ai-directory/architecture.md |
| Conventions | snippets/ai-directory/conventions.md |
| Research templates | snippets/ai-directory/research/*.md |
| Automation templates | snippets/ai-directory/automation/*.md |
| Claude Code commands | snippets/claude-code/commands/*.md |
| Claude Code hooks | snippets/claude-code/hooks.md |

---

## Notes

- This file can be deleted after initialization, or kept for reference
- The template at ~/code/template should not be modified during project init
- If you notice useful patterns missing, create an issue: `cd ~/code/template && bd create "Add: ..."`
- For detailed question flow, see: questions/init-questions.md
