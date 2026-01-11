# Project Initialization Questions

A purpose-first approach to project setup. Start with understanding what the user wants to accomplish, then infer the appropriate configuration.

---

## Primary Question

### Q1: Purpose (Open-Ended)

**Ask**: "What do you want to accomplish with this project?"

Listen for signals that indicate:
- **Code output expected?** (build, create, implement, develop)
- **Investigation only?** (research, explore, understand, learn about)
- **Automation?** (run automatically, cron, scheduled, agent-managed)
- **Time-bounded?** (build X, ship Y, finish Z)
- **Ongoing?** (maintain, evolve, manage, track)
- **Collaboration?** (team, contributors, review)

### Archetype Inference

Based on the response, infer the primary archetype:

| Signals | Archetype | Default Setup |
|---------|-----------|---------------|
| "Build X", "Create Y", clear deliverable | **Build** | GSD + dev branch |
| "Maintain", "manage", "evolve over time" | **Maintain** | beads + beads-sync |
| "Research", "investigate", "understand" | **Research** | beads + research notes |
| "Run automatically", "cron", "scheduled" | **Automate** | beads + logs + config |
| "Learn", "experiment", "try out" | **Learn** | minimal |
| "Document", "wiki", "knowledge base" | **Document** | beads + docs structure |
| "Team", "contributors", "PR workflow" | **Collaborate** | beads + full docs + PR |
| Quick task, one-off, simple | **Quick** | CLAUDE.md only |

---

## Confirmation Question

### Q2: Confirm Inference

**Ask**: "Based on that, I'd suggest a [archetype] setup with [key features]. Does that sound right?"

Example responses:
- "This sounds like a **Build** project - I'll set up GSD for phase-based planning and a dev branch workflow. Sound good?"
- "This sounds like a **Research** project - I'll create a research notes structure and beads for tracking questions. Sound right?"
- "This sounds like an **Automate** project - I'll set up logging, config management, and beads for tracking issues. Correct?"

If user confirms → proceed with defaults
If user says no → ask Q3-Q5 as needed

---

## Refinement Questions (Conditional)

Only ask these if Q1 answer was ambiguous or user rejected Q2 suggestion.

### Q3: Task Tracking

**Ask**: "How do you want to track work?"

| Answer | When to Use | Creates |
|--------|-------------|---------|
| GSD | Phases and milestones, clear roadmap | .planning/ directory |
| bd (beads) | Discovered work, dependencies, ongoing | .beads/ directory |
| Both | Major features (GSD) + bugs/issues (bd) | Both directories |
| None | Very simple project, just git | Nothing |

### Q4: Git Workflow

**Ask**: "How should we handle git branches?"

| Answer | Branches | When to Use |
|--------|----------|-------------|
| Simple | master/main only | Solo dev, direct commits |
| Dev branch | main + dev | Want stable main, work on dev |
| Beads sync | main + beads-sync | Using beads, want issues off main |
| PR workflow | main + dev + beads-sync | Team, need code review |

### Q5: Documentation Level

**Ask**: "How much documentation structure do you need?"

| Answer | Creates | When to Use |
|--------|---------|-------------|
| Minimal | CLAUDE.md only | Simple projects, scripts |
| Standard | + .ai/architecture.md | Most projects |
| Full | + AGENTS.md + .claude/commands/ | Complex, multi-contributor |

### Q6: Claude Code Setup (if using Claude Code)

**Ask**: "Do you want Claude Code slash commands set up?"

| Answer | Creates |
|--------|---------|
| Yes | .claude/commands/ with commit, pr, release, status, wip, sync |
| No | Skip .claude/ directory |

---

## Archetype Defaults

Quick reference for default configurations:

### Build (Greenfield)
```
Task: GSD
Git: main + dev
Docs: CLAUDE.md + .planning/
CC: commands recommended
```

### Maintain (Ongoing)
```
Task: beads
Git: main + beads-sync
Docs: CLAUDE.md + .ai/
CC: commands recommended
```

### Research
```
Task: beads
Git: main + beads-sync
Docs: CLAUDE.md + .ai/research/
CC: optional
```

### Automate
```
Task: beads
Git: main + beads-sync
Docs: CLAUDE.md + .ai/automation/
CC: commands recommended
Structure: + logs/ + config/
```

### Learn
```
Task: none
Git: main only
Docs: CLAUDE.md only
CC: optional
```

### Document
```
Task: beads
Git: main + beads-sync
Docs: CLAUDE.md + .ai/ + docs/
CC: optional
```

### Collaborate
```
Task: beads
Git: main + dev + beads-sync
Docs: CLAUDE.md + AGENTS.md + .ai/ + .claude/commands/
CC: required
```

### Quick
```
Task: none
Git: main only
Docs: CLAUDE.md only
CC: no
```

---

## Fallback: Direct Selection

If purpose is unclear after Q1, offer direct archetype selection:

**Ask**: "Which of these best describes your project?"

1. **Build** - New feature/app with clear deliverable
2. **Maintain** - Ongoing system that evolves over time
3. **Research** - Investigation, no code output expected
4. **Automate** - Agent-managed system (cron, scheduled tasks)
5. **Learn** - Experimentation, tutorials, skill building
6. **Document** - Knowledge base, wiki, documentation
7. **Collaborate** - Multi-contributor, needs PR workflow
8. **Quick** - One-off task, minimal overhead

---

## Context Question (Always Ask)

### Project Description

**Ask**: "What's a one-sentence description of this project?"

Used to:
- Populate PROJECT.md / CLAUDE.md header
- Seed architecture docs if created
- Help future agents understand context

---

## Anti-Patterns

- Don't over-configure simple projects (Quick doesn't need .ai/)
- Don't under-configure complex projects (Collaborate needs full docs)
- Match git workflow to task system (beads usually wants beads-sync)
- Research projects don't need code scaffolding
- Automate projects need logs and config directories
