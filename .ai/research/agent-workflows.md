# Agent Workflow Patterns

Research into workflow patterns for agent-driven development. Focus on **patterns**, not tools—the tools will change, but the approaches persist.

---

## The 5 Workflow Patterns

### 1. Phase-Based (GSD)

**Already in template.**

Define roadmap upfront, work through milestones sequentially.

| Aspect | Detail |
|--------|--------|
| **When** | Greenfield with clear destination |
| **Pattern** | Spec → Plan → Execute in atomic chunks → Commit per task |
| **Key files** | `.planning/PROJECT.md`, `ROADMAP.md`, `STATE.md` |
| **Strength** | Traceable commits, bisectable history, clear progress |
| **Weakness** | Requires knowing destination upfront |

**Core commands**: `/gsd:create-roadmap`, `/gsd:plan-phase`, `/gsd:execute-plan`

---

### 2. Issue-Based (Beads)

**Already in template.**

Track work as you discover it, manage dependencies.

| Aspect | Detail |
|--------|--------|
| **When** | Maintenance, ongoing projects, emerging scope |
| **Pattern** | Discover → Create issue → Work → Close → Sync |
| **Key files** | `.beads/` directory |
| **Strength** | Handles discovered work, tracks blockers |
| **Weakness** | No inherent roadmap or milestones |

**Core commands**: `bd ready`, `bd create`, `bd close`, `bd sync`

---

### 3. Parallel Execution

Run multiple isolated agent contexts simultaneously.

| Aspect | Detail |
|--------|--------|
| **When** | Tasks are independent, you can context-switch between outputs |
| **Pattern** | Numbered contexts + notifications when attention needed |
| **Strength** | Massive throughput increase |
| **Weakness** | Requires attention management skill |

**Key insight**: The bottleneck isn't generation—it's attention allocation.

**Variations**:
- **Boris pattern**: 5+ numbered terminal tabs, system notifications, "Starcraft-style" management
- **Panopticon pattern**: 8 domain directories (~/nox, ~/email, ~/trades, etc.), explicit filesystem handoffs

**How to apply**:
1. Open multiple terminal tabs/sessions
2. Number them for quick reference
3. Enable system notifications for completion
4. Context-switch when notified, not continuously

---

### 4. Async with Checkpoints

Long-running work that survives restarts, with notification on completion.

| Aspect | Detail |
|--------|--------|
| **When** | Tasks take hours, you want to do other things |
| **Pattern** | Start → Checkpoint state → Notify on complete → Resume |
| **Strength** | Work continues without your attention |
| **Weakness** | Requires infrastructure for persistence/notification |

**Key insight**: Agent work should be resumable, not ephemeral.

**Variations**:
- **Caffeinate + SMS**: Keep system awake, text on completion, reply to continue (Panopticon)
- **Background agents**: Spawn async, monitor status, take over mid-flight
- **Git-backed state**: Persist work state in hooks, survives agent restarts (Gas Town)

**How to apply**:
1. Use `caffeinate -i` to prevent sleep during long runs
2. Set up notification on completion (native notifications, SMS, webhook)
3. Design for checkpoint/resume rather than single-shot execution

---

### 5. Reflexive Learning

Store lessons learned, feed into future attempts.

| Aspect | Detail |
|--------|--------|
| **When** | You keep hitting the same issues, want to accumulate knowledge |
| **Pattern** | Work → Reflect → Store lesson → Future agents read lessons |
| **Key files** | `CLAUDE.md`, `.ai/learnings.md`, `.ai/decisions.md` |
| **Strength** | Agents get smarter over time |
| **Weakness** | Requires discipline to capture learnings |

**Key insight**: "95-99% of agent interactions could be handled by a properly briefed model." (Yegge)

**Variations**:
- **CLAUDE.md as memory**: Add mistakes so agents learn not to repeat them (Boris)
- **learnings.md**: Document discoveries, gotchas, patterns (already in template)
- **Reflexion pattern**: Verbal reinforcement via stored reflections after failures (academic)

**How to apply**:
1. After any significant failure or discovery, document it
2. Keep CLAUDE.md updated with project-specific guidance
3. Review and prune accumulated knowledge periodically

---

## New Processes to Try

### Verification Loops

**Source**: Boris Cherny

Give agents a way to verify their work = 2-3x quality improvement.

**Implementation**:
- Before execution, ask: "How will you know this worked?"
- Include verification steps in task definitions
- Create subagents specifically for verification (e.g., `verify-app`)

**Example prompt addition**:
```
Before completing this task, verify:
1. Tests pass
2. App builds successfully
3. Feature works as specified
```

---

### Domain Isolation

**Source**: Panopticon (Molly Cantillon)

Separate life/work into isolated agent directories that don't share context.

**Implementation**:
- Create separate project directories per domain
- Each operates independently, spawns its own subagents
- Exchange context through filesystem writes, not shared memory

**Potential domains**:
```
~/code/       # Development work
~/email/      # Inbox processing
~/trades/     # Finance/investment
~/health/     # Fitness, sleep, nutrition
~/writing/    # Content creation
~/personal/   # Life admin
```

**Key principle**: Isolation prevents cross-contamination and keeps token usage minimal.

---

### Tree of Thoughts

**Source**: Academic (Yao et al.)

For complex architectural decisions, explore multiple approaches before committing.

**Implementation**:
1. Generate 2-3 candidate approaches
2. Evaluate each against explicit criteria
3. Select best path forward
4. Document decision in `.ai/decisions.md`

**When to use**:
- Choosing between frameworks/libraries
- Designing system architecture
- Refactoring approaches
- Any decision with multiple viable paths

---

### Cron-Driven Automation

**Source**: Panopticon, Continue Mission Control

Recurring agent tasks on schedule, not just interactive sessions.

**Implementation**:
- Set up cron jobs that invoke agent workflows
- Use hooks for event-driven triggers
- Log all executions for review

**Potential automations**:
- Daily metric briefs
- Inbox processing
- Dependency updates
- Test suite runs
- Documentation freshness checks

**Example cron**:
```bash
# Every morning at 6am, generate daily brief
0 6 * * * cd ~/trades && claude "Generate today's brief" >> logs/brief.log 2>&1
```

---

## Pattern Selection Guide

| Situation | Pattern |
|-----------|---------|
| Building something new with clear scope | **Phase-Based (GSD)** |
| Maintaining existing system | **Issue-Based (Beads)** |
| Multiple independent tasks | **Parallel Execution** |
| Tasks take hours | **Async with Checkpoints** |
| Keep making same mistakes | **Reflexive Learning** |
| Need higher quality output | **Verification Loops** |
| Life automation beyond coding | **Domain Isolation** |
| Complex architectural decisions | **Tree of Thoughts** |
| Recurring tasks | **Cron-Driven Automation** |

---

## Three Developer Loops (Framework)

From Kim & Yegge's *Vibe Coding*—useful mental model for where each pattern fits.

| Loop | Timeframe | Focus | Patterns That Fit |
|------|-----------|-------|-------------------|
| **Inner** | Seconds-minutes | Immediate work | Parallel Execution, Verification Loops |
| **Middle** | Hours-days | Session continuity | Async with Checkpoints, Reflexive Learning |
| **Outer** | Weeks-months | Strategic direction | Phase-Based (GSD), Domain Isolation |

---

## Sources

**Primary**:
- Boris Cherny workflow: [VentureBeat](https://venturebeat.com/technology/the-creator-of-claude-code-just-revealed-his-workflow-and-developers-are)
- Steve Yegge: [Beads](https://steve-yegge.medium.com/introducing-beads-a-coding-agent-memory-system-637d7d92514a), [Gas Town](https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04)
- TÂCHES/GSD: [GitHub](https://github.com/glittercowboy/get-shit-done)
- Three Developer Loops: [IT Revolution](https://itrevolution.com/articles/the-three-developer-loops-a-new-framework-for-ai-assisted-coding/)
- Panopticon: `research-ephemeral/panopticon.md`

**Academic**:
- Reflexion: Shinn et al. (verbal reinforcement via reflective text)
- Tree of Thoughts: Yao et al. (search over candidate thought branches)
- ReAct: Yao et al. (interleave reasoning traces with tool actions)
