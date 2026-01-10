# Project Starter Template

This repository is an **agent-managed project initialization template**. It contains patterns, snippets, and examples extracted from real projects to help bootstrap new work.

## What This Is

A collection of markdown files that any coding agent (Claude Code, opencode, codex, etc.) can read and follow to set up new projects with established patterns.

**Key principle**: No agent-specific features in the core workflow. The template is plain markdown that any agent can interpret.

## How to Use

```bash
# 1. Create and enter your new project
mkdir ~/code/myproject && cd ~/code/myproject
git init

# 2. Start any coding agent
claude  # or opencode, codex, etc.

# 3. Give the initialization prompt
"Initialize this project following ~/code/template/INIT.md"
```

The agent will read INIT.md, ask you interactive questions, and set up the appropriate structure based on your answers.

## What Gets Created

Depending on your choices, you'll get some combination of:

- **CLAUDE.md** - Agent instructions (always created)
- **AGENTS.md** - Detailed workflow for complex projects
- **.ai/** - Architecture documentation
- **.beads/** - Issue tracking with bd
- **.planning/** - GSD phase-based planning
- **.claude/commands/** - Git workflow shortcuts

## This Template Evolves

This template is itself a tracked project:
- Has its own .beads/ for improvement tracking
- Updated when new patterns emerge from real projects
- Maintained by agents working on real projects who notice gaps

### Contributing Patterns

When working on a project and you discover a useful pattern:
1. Note it in a beads issue here: `cd ~/code/template && bd create "Add pattern: <description>"`
2. Or update snippets directly if the pattern is clear

## Structure

```
template/
├── AGENTS.md           # You are here - meta documentation
├── INIT.md             # Main initialization guide (what agents follow)
├── RESEARCH.md         # Pattern research from real projects
├── questions/
│   └── init-questions.md   # Interactive questions for project setup
├── snippets/
│   ├── claude-md/      # CLAUDE.md templates
│   ├── agents-md/      # AGENTS.md templates
│   ├── ai-directory/   # .ai/ templates
│   └── git-commands/   # Slash command templates
└── examples/           # Full working examples
    ├── greenfield/     # GSD-based new project
    ├── maintenance/    # Beads-based ongoing project
    └── complex/        # Full setup with everything
```

## Decision Framework

| Project Type | Task System | Git Workflow | Documentation |
|--------------|-------------|--------------|---------------|
| New feature build | GSD | master only | CLAUDE.md + .planning/ |
| Ongoing maintenance | bd (beads) | main + beads-sync | CLAUDE.md + .ai/ |
| Multi-contributor | bd (beads) | main + dev + beads-sync | Full stack |
| Quick script | none | master only | CLAUDE.md only |

## Source Projects

Patterns extracted from:
- zed-supercollider (complex, multi-contributor)
- audio-loop (greenfield, GSD)
- nix-config (maintenance, beads)
- torrent-getter (greenfield, GSD)

See RESEARCH.md for detailed pattern analysis.

## Landing the Plane (Session Completion)

**When ending a work session**, you MUST complete ALL steps below. Work is NOT complete until `git push` succeeds.

**MANDATORY WORKFLOW:**

1. **File issues for remaining work** - Create issues for anything that needs follow-up
2. **Run quality gates** (if code changed) - Tests, linters, builds
3. **Update issue status** - Close finished work, update in-progress items
4. **PUSH TO REMOTE** - This is MANDATORY:
   ```bash
   git pull --rebase
   bd sync
   git push
   git status  # MUST show "up to date with origin"
   ```
5. **Clean up** - Clear stashes, prune remote branches
6. **Verify** - All changes committed AND pushed
7. **Hand off** - Provide context for next session

**CRITICAL RULES:**
- Work is NOT complete until `git push` succeeds
- NEVER stop before pushing - that leaves work stranded locally
- NEVER say "ready to push when you are" - YOU must push
- If push fails, resolve and retry until it succeeds
