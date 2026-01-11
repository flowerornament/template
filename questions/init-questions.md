# Project Initialization Questions

A purpose-first approach to project setup. Start with understanding what the user wants to accomplish, then let them choose how to manage work.

---

## Q1: Purpose (Required)

**Ask**: "What do you want to accomplish with this project?"

Listen for signals that indicate project type:
- **Code output expected?** (build, create, implement, develop)
- **Investigation only?** (research, explore, understand, learn about)
- **Automation?** (run automatically, cron, scheduled, agent-managed)
- **Time-bounded?** (build X, ship Y, finish Z)
- **Ongoing?** (maintain, evolve, manage, track)
- **Collaboration?** (team, contributors, review)

### Project Type Inference

| Signals | Project Type | What It Means |
|---------|--------------|---------------|
| "Build X", "Create Y", clear deliverable | **Build** | New thing with defined end state |
| "Maintain", "manage", "evolve over time" | **Maintain** | Existing system needing ongoing care |
| "Research", "investigate", "understand" | **Research** | Investigation, learning, no code output |
| "Run automatically", "cron", "scheduled" | **Automate** | Agent-managed, runs on schedule |
| "Learn", "experiment", "try out" | **Learn** | Skill building, experimentation |
| "Document", "wiki", "knowledge base" | **Document** | Knowledge capture and organization |
| "Team", "contributors", "PR workflow" | **Collaborate** | Multi-person, needs review process |
| Quick task, one-off, simple | **Quick** | Minimal overhead, get it done |

---

## Q2: Project Description (Required)

**Ask**: "What's a one-sentence description of this project?"

Used to:
- Populate CLAUDE.md header
- Seed architecture docs if created
- Help future agents understand context

---

## Q3: Task Management (Required)

**Always ask**: "How do you want to manage work on this project?"

| Option | Description |
|--------|-------------|
| **GSD** | Phase-based roadmap. Define milestones upfront, work through them sequentially. |
| **beads** | Issue tracking. Create tasks as you discover them, track dependencies and blockers. |
| **Minimal** | Just git commits. No formal tracking system. |
| **Help me decide** | Let's discuss your project to find the best fit. |

### If "Help me decide"

Ask these questions to research the best fit:

**Q3a**: "Do you have a clear picture of the end result, or will the scope emerge as you work?"
- Clear end state → leans **GSD**
- Scope will emerge → leans **beads**

**Q3b**: "Is this a one-time build, or something you'll maintain over time?"
- One-time build → leans **GSD** or **Minimal**
- Ongoing maintenance → leans **beads**

**Q3c**: "Do you expect to discover bugs, issues, or follow-up work along the way?"
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

After determining recommendation, confirm with user before proceeding.

---

## Q4: Confirm Setup (Required)

**Ask**: "I'll set up a [project type] project with [task system]. Sound right?"

- If yes → proceed to configuration
- If no → ask what they'd prefer

---

## Optional Refinement Questions

Only ask these if needed for clarity.

### Git Workflow

**Ask**: "How should we handle git branches?"

| Answer | Branches | When to Use |
|--------|----------|-------------|
| Simple | main only | Solo dev, direct commits |
| Dev branch | main + dev | Want stable main, work on dev |
| PR workflow | main + dev | Team, need code review |

Note: beads-sync branch is added automatically if using beads.

### Documentation Level

**Ask**: "How much documentation structure do you need?"

| Answer | Creates | When to Use |
|--------|---------|-------------|
| Minimal | CLAUDE.md only | Simple projects, scripts |
| Standard | + .ai/architecture.md | Most projects |
| Full | + AGENTS.md + .claude/commands/ | Complex, multi-contributor |

### Claude Code Setup

**Ask**: "Do you want Claude Code slash commands set up?"

| Answer | Creates |
|--------|---------|
| Yes | .claude/commands/ with commit, pr, release, status, wip, sync |
| No | Skip .claude/ directory |

---

## Fallback: Direct Selection

If purpose is unclear after Q1, offer direct project type selection:

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

## Anti-Patterns

- Don't assume task system from project type - always ask
- Don't over-configure simple projects (Quick doesn't need .ai/)
- Don't under-configure complex projects (Collaborate needs full docs)
- Match git workflow to task system (beads usually wants beads-sync)
- Research projects don't need code scaffolding
- Automate projects need logs and config directories
