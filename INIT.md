# Project Initialization Guide

**For any coding agent**: Follow this guide to initialize a new project. Use a purpose-first approach - understand what the user wants to accomplish, then set up the appropriate structure.

---

## Step 1: Understand Purpose

### Ask the Primary Question

**"What do you want to accomplish with this project?"**

Listen for signals and infer the project type:

| User Says | Project Type | What It Means |
|-----------|--------------|---------------|
| "Build X", "Create Y", clear deliverable | **Build** | New thing with defined end state |
| "Maintain", "manage", "evolve over time" | **Maintain** | Existing system that needs ongoing care |
| "Research", "investigate", "understand" | **Research** | Investigation, learning, no code output |
| "Run automatically", "cron", "scheduled" | **Automate** | Agent-managed, runs on schedule |
| "Learn", "experiment", "try out" | **Learn** | Skill building, experimentation |
| "Document", "wiki", "knowledge base" | **Document** | Knowledge capture and organization |
| "Team", "contributors", "PR workflow" | **Collaborate** | Multi-person, needs review process |
| Quick task, one-off, simple | **Quick** | Minimal overhead, get it done |

### Get Project Description

**"What's a one-sentence description?"**

Used for CLAUDE.md header and documentation.

---

## Step 2: Choose Task Management

**Always ask**: "How do you want to manage work on this project?"

| Option | Description |
|--------|-------------|
| **GSD** | Phase-based roadmap. Define milestones upfront, work through them sequentially. |
| **beads** | Issue tracking. Create tasks as you discover them, track dependencies and blockers. |
| **Minimal** | Just git commits. No formal tracking system. |
| **Help me decide** | Let's discuss your project to find the best fit. |

### If "Help me decide"

Ask these questions to recommend a system:

**Q1**: "Do you have a clear picture of the end result, or will the scope emerge as you work?"
- Clear end state → leans **GSD**
- Scope will emerge → leans **beads**

**Q2**: "Is this a one-time build, or something you'll maintain over time?"
- One-time build → leans **GSD** or **Minimal**
- Ongoing maintenance → leans **beads**

**Q3**: "Do you expect to discover bugs, issues, or follow-up work along the way?"
- Yes, lots of discovered work → **beads**
- No, straightforward path → **GSD** or **Minimal**

**Decision matrix**:
| Clear End | One-Time | Discovered Work | Recommendation |
|-----------|----------|-----------------|----------------|
| Yes | Yes | No | GSD or Minimal |
| Yes | Yes | Yes | GSD + beads (both) |
| Yes | No | Yes | beads |
| No | No | Yes | beads |
| No | Yes | No | Minimal |

### Task System Reference

| System | Best For | Creates |
|--------|----------|---------|
| **GSD** | Greenfield with clear milestones | `.planning/` with PROJECT.md, ROADMAP.md, STATE.md |
| **beads** | Ongoing work, discovered issues | `.beads/` directory, beads-sync branch |
| **Both** | Major features (GSD) + issues (beads) | Both directories |
| **Minimal** | Simple projects, scripts | Nothing extra |

---

## Step 3: Choose Git Workflow

**Always ask**: "How do you want to manage branches?"

| Option | Description |
|--------|-------------|
| **Direct to main** | Commit directly to main. Simplest approach for solo work. |
| **Dev branch** | Work on dev, merge to main for releases. Keeps main clean. |
| **Feature branches** | Branch per feature/fix, merge via PR. Good for review or collaboration. |
| **Worktrees** | Separate directories per branch. For parallel work across multiple contexts. |
| **Help me decide** | Let's discuss your workflow to find the best fit. |

### If "Help me decide"

**Q1**: "Will you work on multiple things in parallel, or one thing at a time?"
- Multiple parallel → leans **Worktrees** or **Feature branches**
- One at a time → leans **Direct to main** or **Dev branch**

**Q2**: "Do you want main to always be clean/deployable?"
- Yes → **Dev branch** or **Feature branches**
- Doesn't matter → **Direct to main**

**Q3**: "Do you need code review or collaborate with others?"
- Yes → **Feature branches**
- No → **Direct to main**, **Dev branch**, or **Worktrees**

---

## Step 4: Confirm Setup

**"I'll set up a [project type] project with [task system] and [git workflow]. Sound right?"**

- If yes → proceed
- If no → ask what they'd prefer

---

## Step 5: Apply Configuration

Configuration = Project Type + Task System. Combine as needed.

### Project Type Structures

Each type creates a base structure. Task system is added on top.

#### Build
```
project/
└── CLAUDE.md              # From snippets/claude-md/minimal.md (or gsd.md/beads.md based on task system)
```

#### Maintain
```
project/
└── CLAUDE.md
```

#### Research
```
project/
├── CLAUDE.md              # From snippets/claude-md/research.md
└── .ai/
    └── research/
        ├── questions.md
        ├── findings.md
        └── sources.md
```

#### Automate
```
project/
├── CLAUDE.md              # From snippets/claude-md/automate.md
├── .ai/
│   ├── schedule.md
│   ├── triggers.md
│   └── outputs.md
├── config/
└── logs/
```

#### Learn
```
project/
├── CLAUDE.md              # From snippets/claude-md/minimal.md
└── scratch/
```

#### Document
```
project/
├── CLAUDE.md
└── docs/
    └── index.md
```

#### Collaborate
```
project/
├── CLAUDE.md
├── AGENTS.md              # From snippets/agents-md/full.md
└── .claude/
    └── commands/          # From snippets/claude-code/commands/
```

#### Quick
```
project/
└── CLAUDE.md              # From snippets/claude-md/minimal.md
```

---

### Task System Additions

Layer these on top of the project type structure:

#### If GSD
```
+ .planning/
    ├── PROJECT.md         # Project context
    ├── ROADMAP.md         # Phases and milestones
    ├── STATE.md           # Current position
    └── config.json        # {"mode": "yolo", "depth": "comprehensive"}
```
**CLAUDE.md**: Use snippets/claude-md/gsd.md
**Next step**: Run `/gsd:create-roadmap`

#### If beads
```
+ .beads/                  # Via `bd init`
```
**CLAUDE.md**: Use snippets/claude-md/beads.md
**Next step**: Run `bd ready`

#### If Both (GSD + beads)
```
+ .planning/               # For major milestones
+ .beads/                  # For discovered issues
```
**CLAUDE.md**: Mention both systems

#### If Minimal
No additional structure. Just git commits.

---

## Step 6: Initialize Systems

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

### Git Workflow Setup

#### If Direct to main:
No additional setup needed.

#### If Dev branch:
```bash
git checkout -b dev
git push -u origin dev
```

#### If Feature branches:
No initial setup. Create branches as needed: `git checkout -b feat/feature-name`

#### If Worktrees:
```bash
# After initial commit on main, add dev worktree as sibling folder
# Pattern: project/ (main), project-dev/ (dev)
git worktree add ../$(basename "$PWD")-dev -b dev
```

### Git initial commit:

```bash
git add .
git commit -m "Initialize project structure

Co-Authored-By: Claude <noreply@anthropic.com>"
```

---

## Step 7: Claude Code Setup (Optional)

If user wants Claude Code slash commands:

1. Copy commands from `snippets/claude-code/commands/` to `.claude/commands/`
2. Set up hooks per `snippets/claude-code/hooks.md`
3. Verify with `/commit` or `/status`

---

## Step 8: Customize & Verify

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
| Architecture (reference) | snippets/ai-directory/architecture.md |
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
