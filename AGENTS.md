# Project Starter Template

This repository is an **agent-managed project initialization template**. It contains patterns, snippets, and examples extracted from real projects to help bootstrap new work with any coding agent.

## What This Is

A collection of markdown files that any coding agent (Claude Code, opencode, codex, etc.) can read and follow to set up new projects with established patterns.

**Key principles**:
- Agent-agnostic core: Plain markdown that any agent can interpret
- Purpose-first: Ask what user wants to accomplish, infer appropriate setup
- Claude Code enhancement: Optional `.claude/` setup for Claude Code users
- Self-evolving: Template tracks itself and improves over time

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

The agent will ask what you want to accomplish, suggest an appropriate setup, and create the structure.

## Project Archetypes

| Archetype | Description | Typical Setup |
|-----------|-------------|---------------|
| **Build** | New feature/app with clear deliverable | GSD + dev branch |
| **Maintain** | Ongoing system that evolves | beads + beads-sync |
| **Research** | Investigation, no code output | beads + research notes |
| **Automate** | Agent-managed system (cron, scheduled) | beads + logs + config |
| **Learn** | Experimentation, skill building | minimal |
| **Document** | Knowledge base, wiki | beads + docs structure |
| **Collaborate** | Multi-contributor, needs review | beads + PR workflow + full docs |
| **Quick** | One-off task, minimal overhead | CLAUDE.md only |

## What Gets Created

Depending on your archetype, you'll get some combination of:

- **CLAUDE.md** - Agent instructions (always created)
- **AGENTS.md** - Detailed workflow for complex projects
- **.ai/** - Architecture and research documentation
- **.beads/** - Issue tracking with bd
- **.planning/** - GSD phase-based planning
- **.claude/commands/** - Claude Code slash commands
- **logs/** and **config/** - For automation projects

## Structure

```
template/
├── AGENTS.md               # You are here - meta documentation
├── INIT.md                 # Main initialization guide (what agents follow)
├── RESEARCH.md             # Pattern research from real projects
├── questions/
│   └── init-questions.md   # Purpose-first question flow
├── snippets/
│   ├── claude-md/          # CLAUDE.md templates
│   │   ├── minimal.md      # Basic
│   │   ├── beads.md        # For beads workflow
│   │   ├── gsd.md          # For GSD workflow
│   │   ├── research.md     # For research projects
│   │   └── automate.md     # For automation projects
│   ├── agents-md/          # AGENTS.md templates
│   │   └── full.md
│   ├── ai-directory/       # .ai/ templates
│   │   ├── architecture.md
│   │   ├── conventions.md
│   │   ├── research/       # Research project structure
│   │   │   ├── questions.md
│   │   │   ├── findings.md
│   │   │   └── sources.md
│   │   └── automation/     # Automation project structure
│   │       ├── schedule.md
│   │       ├── triggers.md
│   │       └── outputs.md
│   ├── git-commands/       # Agent-agnostic git workflows
│   │   ├── commit.md
│   │   ├── pr.md
│   │   └── wip.md
│   └── claude-code/        # Claude Code specific setup
│       ├── commands/       # Slash commands
│       │   ├── commit.md
│       │   ├── pr.md
│       │   ├── release.md
│       │   ├── status.md
│       │   ├── wip.md
│       │   └── sync.md
│       └── hooks.md        # Hooks configuration
└── examples/               # (Planned) Full working examples
```

## Source Projects

Patterns extracted from:
- zed-supercollider (complex, multi-contributor)
- audio-loop (greenfield, GSD)
- nix-config (maintenance, beads)
- torrent-getter (greenfield, GSD)

See RESEARCH.md for detailed pattern analysis.

## This Template Evolves

This template is itself a tracked project:
- Has its own .beads/ for improvement tracking
- Updated when new patterns emerge from real projects
- Maintained by agents working on real projects who notice gaps

### Contributing Patterns

When working on a project and you discover a useful pattern:
1. Note it in a beads issue here: `cd ~/code/template && bd create "Add pattern: <description>"`
2. Or update snippets directly if the pattern is clear

### Current Issues

Run `bd list` to see open improvements for this template.

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
