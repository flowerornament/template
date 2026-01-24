# Project Starter Pack Research

## Projects Analyzed
- ~/code/zed-supercollider (Zed extension, mature)
- ~/code/audio-loop (Python audio tool, GSD-driven)
- ~/.config/nix-config (System config, beads-driven)
- ~/code/torrent-getter (Go+TS CLI/MCP, GSD-driven)

---

## Pattern Summary

### 1. Agent Instruction Files

| Project | Files | Pattern |
|---------|-------|---------|
| zed-supercollider | CLAUDE.md → AGENTS.md | CLAUDE.md is pointer, AGENTS.md has full workflow |
| audio-loop | CLAUDE.md only | Minimal, references GSD workflow |
| nix-config | CLAUDE.md only | Comprehensive system-specific instructions |
| torrent-getter | CLAUDE.md only | Minimal, references GSD workflow |

**Insight**: CLAUDE.md is universal. AGENTS.md used for complex multi-contributor projects.

**Symlink Pattern**: For projects needing both files, symlink CLAUDE.md → AGENTS.md instead of maintaining two separate files. This ensures agents see the same content regardless of which file they read, with zero maintenance overhead: `ln -s AGENTS.md CLAUDE.md`

### 2. Task Management Systems

| Project | System | Why |
|---------|--------|-----|
| zed-supercollider | bd (beads) | Long-lived, multiple contributors, dependency tracking |
| nix-config | bd (beads) | Ongoing maintenance, issue discovery |
| audio-loop | GSD | Greenfield, milestone-driven development |
| torrent-getter | GSD | Greenfield, phase-based feature build |

**Decision Heuristic**:
- **Use bd (beads)**: Ongoing/maintenance projects, discovered work, dependency tracking needed
- **Use GSD**: New projects with clear milestones, phase-by-phase development

### 3. .ai Directory Structure

| Project | Has .ai/ | Contents |
|---------|----------|----------|
| zed-supercollider | Yes | architecture.md, conventions.md, commands.md, decisions/, prompts/, research/ |
| nix-config | Yes | ARCHITECTURE.md, RECOMMENDATIONS.md |
| audio-loop | No | (Uses .planning/ instead) |
| torrent-getter | Yes | redacted_api.md (API research only) |

**Pattern**: .ai/ for architectural knowledge. Subfolders:
- `architecture.md` - System design
- `conventions.md` - Code standards
- `commands.md` - Build/debug commands
- `decisions/` - ADRs (001-*.md)
- `prompts/` - Reusable debug/task prompts
- `research/` - Investigation artifacts

### 4. Git Workflows

| Project | Branches | Pattern |
|---------|----------|---------|
| zed-supercollider | main, dev, beads-sync, feature/* | PR workflow with beads sync |
| nix-config | main, beads-sync | Direct to main with beads sync |
| audio-loop | master only | Direct commits, GSD phase tags |
| torrent-getter | master only | Direct commits, GSD phase tags |

**Decision Heuristic**:
- **main + dev + beads-sync**: Multi-contributor, PR-based
- **main + beads-sync**: Solo, using beads
- **master only**: Solo, using GSD (phases tracked in .planning/)

### 5. .claude Directory

**Common Structure**:
```
.claude/
├── settings.json           # Plugin settings (beads enabled, etc.)
├── settings.local.json     # Permission allowlists
└── commands/               # Project-specific slash commands
    ├── commit.md
    ├── pr.md
    └── ...
```

**zed-supercollider commands**: /commit, /pr, /release, /smart-commit, /status, /sync, /wip

**Permission Patterns** (settings.local.json):
- bd commands: `bd ready`, `bd list`, `bd show`, `bd update`, `bd close`, `bd sync`
- gsd commands: various /gsd:* workflows
- git operations specific to project
- WebFetch domains for documentation

### 6. GSD .planning Structure

```
.planning/
├── PROJECT.md      # Living project context
├── ROADMAP.md      # Phases and milestones
├── STATE.md        # Current position, metrics, decisions
├── config.json     # {mode: "yolo"|"careful", depth: "comprehensive"|"minimal"}
└── phases/
    └── NN-phase-name/
        ├── NN-MM-PLAN.md     # Executable phase plan
        ├── NN-MM-SUMMARY.md  # Completion record
        └── RESEARCH.md       # Pre-planning research
```

**Key Files**:
- PROJECT.md: Core value proposition, requirements
- ROADMAP.md: All phases with Research: Likely/Not needed
- STATE.md: Current phase, plan, velocity metrics, key decisions

### 7. Beads Configuration

```
.beads/
├── config.yaml      # sync-branch setting
├── issues.jsonl     # Issue data (git-tracked on sync branch)
├── interactions.jsonl
└── metadata.json
```

**Key config**: `sync-branch: "beads-sync"` - keeps issues off main branch

---

## Project Type Classification

### Type A: Greenfield Development
- **Examples**: audio-loop, torrent-getter
- **Task System**: GSD (phases, milestones)
- **Git**: master/main, direct commits with phase tags
- **Structure**: .planning/, CLAUDE.md

### Type B: Ongoing Maintenance/Tool
- **Examples**: nix-config
- **Task System**: bd (beads)
- **Git**: main + beads-sync
- **Structure**: .ai/, .beads/, CLAUDE.md

### Type C: Complex Multi-Contributor
- **Examples**: zed-supercollider
- **Task System**: bd (beads)
- **Git**: main + dev + beads-sync + feature/*
- **Structure**: .ai/, .beads/, CLAUDE.md, AGENTS.md, .claude/commands/

---

## Starter Pack Design Options

### Option 1: Template Repository
- Location: ~/code/template
- Usage: Copy to new project, run agent to customize
- Pros: Simple, portable
- Cons: Drift between copies and original

### Option 2: Init-from-Template Command
- Location: ~/code/template with INIT.md
- Usage: `cd ~/code/newproject && claude "init from ~/code/template"`
- Pros: Template stays canonical, projects get fresh setup
- Cons: Requires reading external directory

### Option 3: Global Slash Command
- Location: ~/.claude/commands/init-project.md
- Usage: `cd ~/code/newproject && claude "/init-project"`
- Pros: Always available, no file copying, single source of truth
- Cons: All logic in one file, harder to evolve with examples

### Option 4: Hybrid (Recommended)
- Location: ~/code/template (reference), ~/.claude/commands/init-project.md (invoker)
- Usage: `/init-project` reads ~/code/template for patterns
- Pros: Command is portable, template has rich examples, both evolve
- The template repo has its own AGENTS.md noting it's agent-managed and evolving

---

## Recommended Starter Pack Contents

### ~/code/template/
```
template/
├── AGENTS.md                    # Meta: this is an evolving starter template
├── examples/
│   ├── greenfield/              # GSD-based project example
│   │   ├── CLAUDE.md
│   │   └── .planning/...
│   ├── maintenance/             # Beads-based project example
│   │   ├── CLAUDE.md
│   │   └── .beads/...
│   └── complex/                 # Full setup with commands
│       ├── CLAUDE.md
│       ├── AGENTS.md
│       ├── .ai/...
│       └── .claude/commands/...
├── snippets/
│   ├── claude-md-minimal.md
│   ├── claude-md-beads.md
│   ├── agents-md-full.md
│   └── git-commands/
│       ├── commit.md
│       ├── pr.md
│       └── ...
└── init-checklist.md            # What to ask when initializing
```

### ~/.claude/commands/init-project.md
- Reads ~/code/template for context
- Asks: Project type? Task system? Git workflow?
- Creates appropriate structure
- Self-documents in project CLAUDE.md

---

## Key Decisions to Make

1. **Task System Selection**:
   - Greenfield with milestones → GSD
   - Ongoing/discovered work → bd
   - Could use both (bd for issues, GSD for major features)

2. **Git Workflow Selection**:
   - Solo + GSD → master only
   - Solo + beads → main + beads-sync
   - Team → main + dev + beads-sync

3. **Documentation Level**:
   - Minimal: CLAUDE.md only
   - Standard: CLAUDE.md + .ai/architecture.md
   - Full: CLAUDE.md + AGENTS.md + .ai/* + .claude/commands/*

4. **Slash Commands**:
   - Always useful: /commit (bd sync first if using beads)
   - PR workflow: /pr, /release
   - Convenience: /status, /wip
