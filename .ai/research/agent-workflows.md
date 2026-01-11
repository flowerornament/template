# Agent Workflow Patterns: A Comprehensive Research Report

Research into workflow patterns for agent-driven development. Focus on **patterns**, not tools—the tools will change, but the approaches persist.

---

## Executive Summary

This research identifies 5 core workflow patterns and 4 new processes worth adopting. The key insight across all sources: **the bottleneck is no longer generation—it's attention allocation and accumulated knowledge**.

The most successful practitioners (Boris Cherny, Steve Yegge, Molly Cantillon) share common traits:
- They run many agents in parallel
- They persist state across sessions
- They accumulate learnings that make future agents more effective
- They treat AI as "capacity you schedule" rather than a tool you use

---

## Part 1: The 5 Core Workflow Patterns

### Pattern 1: Phase-Based Development (GSD)

**Already in template.**

**Origin**: TÂCHES (glittercowboy) - used by engineers at Amazon, Google, Shopify, Webflow.

**Core Philosophy**: Handle complexity behind the scenes—context engineering, XML formatting, subagent orchestration—while keeping the user interface simple. "Describe what you want and have it built correctly."

**How It Works**:

1. **Capture** (`/gsd:new-project`): Interactive questioning extracts complete project vision into PROJECT.md
2. **Plan** (`/gsd:create-roadmap`): System generates phased roadmap with persistent state tracking in ROADMAP.md
3. **Execute** (`/gsd:plan-phase`, `/gsd:execute-plan`): Break phases into atomic tasks, run each in fresh 200k-token subagent context with 2-3 tasks maximum
4. **Iterate** (`/gsd:complete-milestone`, `/gsd:add-phase`, `/gsd:insert-phase`): Ship, add features, insert hotfixes modularly

**Key Technical Details**:
- Each plan runs in a **fresh context window** with 2-3 atomic tasks—prevents quality degradation that occurs when context fills up
- **XML-structured plans** remove ambiguity in task specifications
- **Atomic git commits** per task—supports bisecting failures and reverting individual work units
- State persists in `.planning/` directory: PROJECT.md, ROADMAP.md, STATE.md

**When to Use**:
- Greenfield projects with clear destination
- When you can write a roadmap upfront
- When you want traceable, atomic commit history

**Strengths**: Bisectable history, clear progress visibility, structured planning
**Weaknesses**: Requires knowing destination upfront; overhead for small tasks

**Source**: [GitHub: get-shit-done](https://github.com/glittercowboy/get-shit-done)

---

### Pattern 2: Issue-Based Development (Beads)

**Already in template.**

**Origin**: Steve Yegge's vision for automating the agentic workflow: "95-99% of the interactions we have with coding agents could be handled by a properly briefed model."

**Core Philosophy**: Track work as you discover it. Unlike GSD's upfront planning, Beads handles **emergent scope**—bugs found, features requested, dependencies identified.

**How It Works**:

1. **Discover** work through normal development
2. **Create** issues with `bd create --title="..." --type=task|bug|feature --priority=2`
3. **Track dependencies** with `bd dep add <issue> <blocker>`
4. **Work** on issues, updating status as you go
5. **Close** and sync: `bd close <id>` then `bd sync`

**Key Technical Details**:
- Git-native storage in `.beads/` directory
- Syncs to `beads-sync` branch to keep issues off main
- Priority scale: 0=critical, 1=high, 2=medium, 3=low, 4=backlog
- Dependency tracking prevents working on blocked issues

**When to Use**:
- Maintenance of existing systems
- Ongoing projects where scope emerges over time
- When you need dependency tracking between tasks

**Strengths**: Handles discovered work, tracks blockers, git-native
**Weaknesses**: No inherent roadmap or milestone structure

**Yegge's Observation**: "Vibe coding involves doing the same old shit, over and over. These agents are incredibly powerful and productive, but they require constant monitoring, most of it mundane." Beads automates the mundane.

**Source**: [Introducing Beads](https://steve-yegge.medium.com/introducing-beads-a-coding-agent-memory-system-637d7d92514a)

---

### Pattern 3: Parallel Execution

**Core Insight**: The bottleneck isn't generation—it's attention allocation. Run multiple isolated agent contexts simultaneously and context-switch between them.

#### Variation A: Boris Cherny's Pattern (Claude Code Creator)

**Setup**:
- 5 Claude instances in terminal, numbered tabs 1-5
- 5-10 additional instances on claude.ai/code
- System notifications alert when any Claude needs input
- Sometimes starts sessions from phone, checks in later

**Key Practices**:

1. **Model Choice**: Uses Opus 4.5 with thinking for everything. "Even though it's bigger and slower than Sonnet, since you have to steer it less and it's better at tool use, it is almost always faster in the end."

2. **Subagents for Common Workflows**:
   - `code-simplifier`: Simplifies code after Claude finishes working
   - `verify-app`: Detailed instructions for testing end-to-end
   - Think of subagents as "automating the most common workflows for most PRs"

3. **Verification Loops**: "The most important thing to get great results out of Claude Code is to give Claude a way to verify its work. If Claude has that feedback loop, it will 2-3x the quality of the final result."

4. **CLAUDE.md as Team Memory**: "Anytime we see Claude do something incorrectly we add it to the CLAUDE.md, so Claude knows not to do it next time."

5. **Slash Commands for Inner Loops**: Boris uses `/commit-push-pr` dozens of times daily.

**Philosophy**: "I don't see AI as a tool you use, but as a capacity you schedule. I'm distributing cognition like compute: allocate it, queue it, keep it hot, switch contexts only when value is ready."

**User Feedback**: After implementing this setup, one user noted the experience "feels more like Starcraft" than traditional coding—a shift from typing syntax to commanding autonomous units.

**Source**: [VentureBeat](https://venturebeat.com/technology/the-creator-of-claude-code-just-revealed-his-workflow-and-developers-are)

#### Variation B: Panopticon Pattern (Molly Cantillon)

**The Philosophy**:

> "Before a king can tax, he must count. Before he can conscript, he must locate. Before he can rule, he must see. Legibility is the precondition for governance."
>
> "States built legibility infrastructure to govern. Corporations built it to sell. Neither gave you the keys to the tower."
>
> "A panopticon still, but the tower belongs to you."

**The Setup**: 8 isolated agent instances, each a separate directory:

```
~/nox        # Product: pulls Amplitude, cross-references GitHub, points to what needs building
~/metrics    # Analytics and measurement
~/email      # Inbox zero, auto-drafted replies for everything inbound
~/growth     # Marketing and growth
~/trades     # Finance: overnight pulls congressional/hedge fund disclosures, Polymarket, sentiment, 10-Ks
~/health     # Workouts accommodating erratic travel, sleep optimization
~/writing    # Content creation
~/personal   # Life admin: subscriptions, citations, procrastinated action items
```

**Key Technical Details**:
- Each domain **operates in isolation**, spawns short-lived subagents
- Context exchange through **explicit filesystem handoffs**, not shared memory
- When APIs are absent, agents **operate the desktop directly**, injecting mouse and keystroke events
- `caffeinate -i` keeps system awake during runs (airports, sleeping)
- **SMS checkpoint**: On completion, texts notification; reply to continue
- **All thought traces logged** and artifacted for recursive self-improvement

**Concrete Examples**:
- "Found and returned $2000 I didn't know I was paying" (subscriptions)
- "The dozen SFMTA citations I'd ignored, the action items I'd procrastinated into oblivion"
- Finance: "Last month it flagged Rep. Fields buying NFLX shares. Three weeks later, the Warner Bros deal."
- Epstein files: "Thousands of documents parsed into a searchable index... By 7am we shipped Jmail. 18 million people have since searched an inbox that belonged to a dead man. A decade ago this would have taken a team and a quarter of runway. We did it in one night."

**The Feeling**: "It is the violent gap between how blind you were and how obvious everything feels now with an observer that reads all the feeds, catches what you've unconsciously dropped, notices patterns across domains you'd kept stubbornly separate, and—crucially—tells you what to do about it."

**The Warning**: "There is a case for productive illegibility. For forgetting, for serendipity, for negative capability... Goodhart says optimize for a metric and you game your way to hollow victory... There's a meta-level outside the system, self-authored and continuously revised, that argues with the brief for days, notices when a metric has become a game, that can delete ~/health tomorrow if it stops serving."

**Source**: `research-ephemeral/panopticon.md`

---

### Pattern 4: Async with Checkpoints

**Core Insight**: Agent work should be resumable, not ephemeral. Long-running tasks need to survive restarts and run while you do other things.

#### The Problem

Traditional agent sessions are ephemeral. Close the terminal, lose the context. This limits you to tasks that complete in one sitting.

#### Solutions

**A. Caffeinate + SMS (Panopticon)**
```bash
caffeinate -i  # Keep system awake
# Agent runs for hours...
# On completion, texts you
# Reply to checkpoint and continue
```

**B. Git-Backed State (Gas Town - Steve Yegge)**

Gas Town is a workspace manager enabling coordination of multiple Claude Code agents while maintaining persistent work state through git-backed hooks.

**Architecture**:
- **The Mayor**: Your primary AI coordinator with workspace context. Describe goals, it orchestrates other agents.
- **Rigs**: Project containers wrapping git repositories and their associated agents
- **Hooks**: Git worktree-based storage—"work survives agent restarts"
- **Convoys**: Work tracking units bundling multiple issues assigned to agents
- **Polecats**: Ephemeral worker agents spawned for specific tasks, then removed

**Workflow (MEOW)**:
1. Describe your goal to the Mayor
2. Mayor analyzes and creates a convoy with issues
3. Spawns appropriate agents
4. Distributes work through hooks
5. Monitors progress
6. Summarizes results

**Scale**: "Scales comfortably to 20-30 agents through persistent state management rather than relying on agent memory alone."

**C. Background Agents (Cursor Pattern)**
- Spawn background agents in remote environment
- Monitor status from IDE
- Take over mid-flight when needed
- Work continues while you do other things

**When to Use**:
- Tasks that take hours
- When you want to do other work while agent runs
- When you need recoverability from failures

**Source**: [GitHub: gastown](https://github.com/steveyegge/gastown)

---

### Pattern 5: Reflexive Learning

**Core Insight**: "95-99% of agent interactions could be handled by a properly briefed model." The key is accumulating knowledge that makes briefing automatic.

#### The Academic Foundation: Reflexion

Reflexion (Shinn et al.) introduced "verbal reinforcement"—storing reflective text in episodic memory to improve iterative attempts. After failures, the agent writes what went wrong in natural language. Future attempts read this memory and avoid the same mistakes.

This is more powerful than it sounds: it converts repeated failures into durable heuristics.

#### Practical Implementations

**A. CLAUDE.md as Team Memory (Boris)**

"Anytime we see Claude do something incorrectly we add it to the CLAUDE.md, so Claude knows not to do it next time."

This is simple but effective: a single file that accumulates project-specific guidance.

**B. Structured Knowledge in .ai/ (Current Template)**

```
.ai/
├── architecture.md    # System structure (create when there's real content)
├── decisions.md       # Key choices and rationale
└── learnings.md       # Discoveries, gotchas, patterns
```

**C. Trace Logging for Self-Improvement (Panopticon)**

"All thought traces logged and artifacted for recursive self-improvement."

Every agent run produces traces. Reviewing these surfaces patterns in failures and successes.

#### Industry Convergence on Repo-Native Guidance

Multiple tools are converging on the same pattern:
- **CLAUDE.md** (Claude Code)
- **AGENTS.md** (OpenAI Codex, emerging standard)
- **Cursor Rules** (Cursor)
- **Continue Rules** (Continue)

This suggests repo-native instruction files are becoming the standard for agent memory.

**When to Use**:
- When you keep hitting the same issues
- When you want agents to get smarter over time
- When onboarding new agents to a project

---

## Part 2: The Three Developer Loops Framework

From Gene Kim and Steve Yegge's book *Vibe Coding*—a framework for organizing AI-assisted development across three timeframes.

### Inner Loop (Seconds to Minutes)

**Focus**: Immediate collaboration with AI assistants. "Request-output-verify" cycles happen rapidly.

**Key Strategies**:
- Decompose tasks into small steps
- Checkpoint frequently through version control
- Write specifications and tests before coding
- Verify AI claims independently

**Patterns That Fit**: Parallel Execution, Verification Loops

### Middle Loop (Hours to Days)

**Focus**: Context management between coding sessions. AI assistants lose memory between interactions.

**Key Strategies**:
- Create external memory systems (CLAUDE.md, .ai/ files)
- Establish project guidelines
- Design code for AI capabilities
- Monitor for architectural drift

**Patterns That Fit**: Async with Checkpoints, Reflexive Learning

### Outer Loop (Weeks to Months)

**Focus**: Strategic architecture and long-term system design.

**Key Strategies**:
- Preserve existing APIs
- Partition workspaces to prevent conflicts
- Implement enhanced CI/CD monitoring
- Develop recovery procedures for complex merge conflicts

**Patterns That Fit**: Phase-Based (GSD), Domain Isolation

### Core Principle

Each loop operates on the same foundation: **prevent problems → detect issues early → correct quickly**. AI generates code faster than humans can write it, requiring systematic management across different timescales.

**Source**: [IT Revolution: Three Developer Loops](https://itrevolution.com/articles/the-three-developer-loops-a-new-framework-for-ai-assisted-coding/)

---

## Part 3: Steve Yegge's 8-Stage Developer Evolution

Yegge outlined an evolution for developers working with AI agents:

| Stage | Description |
|-------|-------------|
| 1 | Near-zero AI usage |
| 2 | Basic prompting, occasional help |
| 3 | Regular AI assistance |
| 4 | AI as primary coding partner |
| 5 | Running multiple agents |
| 6-7 | Running 10+ parallel agent instances, pushing limits of hand-management |
| 8 | Building your own orchestrator |

**Key Observation**: Advanced developers are using Claude Code with Beads as a workflow accelerator, with some "burning $60k/year on tokens while achieving the maximum speeds you can get with coding agents."

**The Vision**: "It will be like kubernetes, but for agents—multiple levels of agents supervising other agents."

**Source**: [Six New Tips for Better Coding With Agents](https://steve-yegge.medium.com/six-new-tips-for-better-coding-with-agents-d4e9c86e42a9)

---

## Part 4: New Processes to Try

### Process 1: Verification Loops

**Source**: Boris Cherny

**The Claim**: Giving agents a way to verify their work = 2-3x quality improvement.

**Implementation**:

1. Before execution, ask: "How will you know this worked?"
2. Include explicit verification steps in task definitions
3. Create subagents specifically for verification (e.g., `verify-app`)

**Example Prompt Addition**:
```
Before marking this task complete:
1. Run the test suite: all tests must pass
2. Build the application: must complete without errors
3. Manually verify the feature works as specified
4. Document any edge cases discovered
```

**Why It Works**: Without verification, agents often declare success prematurely. A verification step forces the agent to actually check its work before moving on.

---

### Process 2: Domain Isolation

**Source**: Panopticon (Molly Cantillon)

**The Principle**: Separate life/work into isolated agent directories that don't share context. Each domain operates independently, spawns its own subagents, and exchanges context through filesystem writes rather than shared memory.

**Benefits**:
- Prevents cross-contamination between domains
- Keeps token usage minimal per domain
- Allows domain-specific customization
- Failures in one domain don't affect others

**Potential Domains**:
```
~/code/       # Development work (could further subdivide by project)
~/email/      # Inbox processing, auto-drafted replies
~/trades/     # Finance, investment research
~/health/     # Fitness tracking, workout planning
~/writing/    # Content creation, drafts
~/personal/   # Life admin, subscriptions, todo lists
```

**Starting Point**: Don't try to set up all domains at once. Start with one non-coding domain where you feel "catastrophically blind" and build from there.

---

### Process 3: Tree of Thoughts

**Source**: Academic (Yao et al.)

**The Idea**: For complex architectural decisions, explore multiple approaches before committing. Instead of the agent picking one path immediately, generate 2-3 candidate approaches and evaluate each.

**Implementation**:

1. Generate 2-3 candidate approaches
2. For each, outline:
   - Pros and cons
   - Implementation complexity
   - Risk factors
   - Long-term implications
3. Evaluate against explicit criteria
4. Select best path forward
5. Document decision in `.ai/decisions.md`

**When to Use**:
- Choosing between frameworks/libraries
- Designing system architecture
- Significant refactoring decisions
- Any decision with multiple viable paths

**Related Pattern**: ReAct (Yao et al.) interleaves "reasoning traces" with tool actions. The agent thinks out loud, acts, observes results, thinks again. This reduces hallucination by continuously re-grounding on external state.

---

### Process 4: Cron-Driven Automation

**Source**: Panopticon, Continue Mission Control

**The Shift**: Move from purely interactive sessions to recurring agent tasks on schedule. Not every agent interaction needs to start with you typing a prompt.

**Implementation**:
- Set up cron jobs that invoke agent workflows
- Use hooks for event-driven triggers
- Log all executions for review

**Potential Automations**:
- **Daily briefs**: Morning summary of what needs attention
- **Inbox processing**: Auto-draft replies, flag important messages
- **Dependency updates**: Check for outdated packages, propose PRs
- **Test suite monitoring**: Run tests nightly, alert on failures
- **Documentation freshness**: Flag docs that are out of sync with code
- **Metric pulls**: Aggregate data from various sources into daily reports

**Example Cron**:
```bash
# Every morning at 6am, generate daily brief
0 6 * * * cd ~/trades && claude "Generate today's brief based on overnight data" >> logs/brief.log 2>&1

# Every Sunday, check for outdated dependencies
0 10 * * 0 cd ~/code/myproject && claude "Check for outdated dependencies and create issues for updates" 2>&1
```

**The Vision** (from Panopticon): "NOX now runs on a cron job: pulling Amplitude, cross-referencing GitHub, and pointing me to what needs building. It handles A/B testing, generates winning copy, and has turned customer support into a fully autonomous department."

---

## Part 5: Memory and Context Persistence Patterns

From the broader research, several patterns emerged for how to persist knowledge across sessions:

### Repo-Native Memory (Preferred)

Store instructions and knowledge with the code. Survives tool churn, can be code reviewed.

- **CLAUDE.md / AGENTS.md**: Agent runbook at project level
- **Tool-specific files**: Gemini uses GEMINI.md with modular imports
- **Spec artifacts**: Durable alignment documents that guide agent behavior
- **Git history as memory**: Agents that auto-commit create searchable history of decisions

### Durable Execution State

Resume exactly where the agent left off.

- **LangGraph checkpointers**: Store graph state per step, enable resume and human-in-the-loop
- **Git worktree hooks** (Gas Town): State survives agent restarts

### Episodic Reflection Memory

Behavioral improvements, not just factual recall.

- **Reflexion-style buffers**: Store "lessons learned" after failures, feed into subsequent attempts
- **Use when**: Main risk is repeating the same category of mistake

### External Long-Term Memory

Cross-session recall and personalization.

- **Mem0**: Explicit memory layer for user preference recall and long-horizon personalization
- **Zep**: Context engineering and relationship-aware context assembly
- **Use when**: Want the agent to remember across sessions and products, not just within one repo

---

## Part 6: Pattern Selection Guide

| Situation | Primary Pattern | Supporting Patterns |
|-----------|----------------|---------------------|
| Building something new with clear scope | Phase-Based (GSD) | Verification Loops |
| Maintaining existing system | Issue-Based (Beads) | Reflexive Learning |
| Multiple independent tasks | Parallel Execution | - |
| Tasks take hours | Async with Checkpoints | Parallel Execution |
| Keep making same mistakes | Reflexive Learning | - |
| Need higher quality output | Verification Loops | - |
| Life automation beyond coding | Domain Isolation | Cron-Driven Automation |
| Complex architectural decisions | Tree of Thoughts | - |
| Recurring tasks | Cron-Driven Automation | Domain Isolation |

---

## Part 7: Key Quotes to Remember

**On attention as the bottleneck**:
> "The bottleneck is no longer ability. The bottleneck is activation energy: who has the nerve to try, and the stubbornness to finish." — Molly Cantillon

**On properly briefed models**:
> "95-99% of the interactions we have with coding agents could be handled by a properly briefed model." — Steve Yegge

**On verification**:
> "The most important thing to get great results out of Claude Code is to give Claude a way to verify its work. If Claude has that feedback loop, it will 2-3x the quality of the final result." — Boris Cherny

**On the experience of parallel agents**:
> "It feels more like Starcraft than traditional coding—a shift from typing syntax to commanding autonomous units." — User feedback on Boris's workflow

**On legibility infrastructure**:
> "States built legibility infrastructure to govern. Corporations built it to sell. Neither gave you the keys to the tower." — Molly Cantillon

**On the current moment**:
> "Failing to claim the boost now feels decidedly like a skill issue." — Andrej Karpathy (quoted in Panopticon)

---

## Sources

### Primary Sources
- **Boris Cherny**: [VentureBeat](https://venturebeat.com/technology/the-creator-of-claude-code-just-revealed-his-workflow-and-developers-are), [How Boris Cherny Uses Claude Code](https://karozieminski.substack.com/p/boris-cherny-claude-code-workflow)
- **Steve Yegge**: [Beads](https://steve-yegge.medium.com/introducing-beads-a-coding-agent-memory-system-637d7d92514a), [Gas Town](https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04), [Six New Tips](https://steve-yegge.medium.com/six-new-tips-for-better-coding-with-agents-d4e9c86e42a9)
- **TÂCHES/GSD**: [GitHub](https://github.com/glittercowboy/get-shit-done), [taches-cc-resources](https://github.com/glittercowboy/taches-cc-resources)
- **Three Developer Loops**: [IT Revolution](https://itrevolution.com/articles/the-three-developer-loops-a-new-framework-for-ai-assisted-coding/)
- **Panopticon**: `research-ephemeral/panopticon.md`
- **Anthropic Agent Skills**: [Anthropic Engineering](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)

### Academic Sources
- **Reflexion**: Shinn et al. — Verbal reinforcement via reflective text stored in episodic memory
- **Tree of Thoughts**: Yao et al. — Search over candidate thought branches for complex planning
- **ReAct**: Yao et al. — Interleave reasoning traces with tool actions to reduce hallucination

### Industry Context
- **Convergence on repo-native guidance**: AGENTS.md, CLAUDE.md, Cursor Rules, Continue Rules
- **MCP (Model Context Protocol)**: Standard protocol for connecting agents to external tools/data
- **Background/async agents**: Becoming default in IDEs (Cursor, others)
