# Agent-Driven Development Workflows Research

Research into alternative and complementary agent development models for the project starter template.

---

## Executive Summary

The landscape of agent-driven development has evolved rapidly. Key patterns emerging:

1. **Parallel agent execution** is becoming standard (5-30+ simultaneous agents)
2. **Persistent state management** distinguishes advanced workflows from basic prompting
3. **Three distinct scales** of operation: inner loop (seconds), middle loop (hours), outer loop (weeks)
4. **Domain isolation** with explicit handoffs outperforms monolithic agent contexts

**Recommendation**: The template should support multiple workflow patterns, allowing users to choose based on project characteristics and personal preference.

---

## 1. Boris Cherny's Multi-Agent Workflow (Claude Code Creator)

### Overview
Run multiple Claude instances in parallel, treating AI as "capacity you schedule" rather than a tool you use.

### Key Patterns

| Pattern | Description |
|---------|-------------|
| **Parallel execution** | 5 terminal Claudes + 5-10 web Claudes running simultaneously |
| **Numbered tabs** | System notifications alert when Claude needs input |
| **Verification loops** | Give Claude a way to verify its work = 2-3x quality improvement |
| **CLAUDE.md memory** | Team maintains single file; add mistakes so Claude learns |
| **Subagents** | code-simplifier, verify-app automate common workflows |
| **Model choice** | Opus 4.5 with thinking for everything ("slower but faster in the end") |

### Philosophy
> "The bottleneck isn't generation; it's attention allocation."

Cherny sees this as "Starcraft-style" management—commanding autonomous units rather than typing syntax.

### When to Use
- High-velocity development with clear verification criteria
- Projects where parallel work streams don't conflict
- Teams comfortable with high context-switching

### Source
[VentureBeat: Claude Code Creator Workflow](https://venturebeat.com/technology/the-creator-of-claude-code-just-revealed-his-workflow-and-developers-are)

---

## 2. Steve Yegge's Orchestration Ecosystem

### Overview
A suite of interconnected tools representing 4 complete orchestrator attempts in 2025.

### Tools

#### Beads (Already in Template)
- Agent memory/issue tracking system
- Git-native storage with dependency tracking
- Focus: discovered work, cross-session continuity

#### Gas Town
- Multi-agent workspace manager
- Persists state in git-backed hooks (survives agent restarts)
- Key components:
  - **Mayor**: Primary AI coordinator with workspace context
  - **Rigs**: Project containers wrapping git repos + agents
  - **Hooks**: Git worktree-based storage
  - **Convoys**: Work tracking units bundling issues
  - **Polecats**: Ephemeral worker agents spawned for tasks
- Scales comfortably to 20-30 agents

#### VC (AI-Orchestrated Coding Agent Colony)
- Higher-level orchestration layer
- Multiple levels of agents supervising other agents
- Vision: "Kubernetes for agents"

### 8-Stage Developer Evolution
1. Near-zero AI usage
2. Basic prompting
3. Regular AI assistance
4. ...
5. ...
6. Stage 6-7: Running 10+ parallel agents, pushing hand-management limits
7. ...
8. Building your own orchestrator

### When to Use
- **Beads**: Ongoing maintenance, discovered work, dependency tracking
- **Gas Town**: Large-scale parallel work, need state persistence across restarts
- **VC**: Complex projects requiring hierarchical agent supervision

### Sources
- [GitHub: gastown](https://github.com/steveyegge/gastown)
- [GitHub: vc](https://github.com/steveyegge/vc)
- [Welcome to Gas Town](https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04)

---

## 3. TÂCHES (glittercowboy) - GSD System

### Overview
Meta-prompting, context engineering, and spec-driven development. Already partially integrated into template.

### Core Philosophy
Handle complexity behind the scenes—context engineering, XML formatting, subagent orchestration—while keeping the interface simple.

### Key Features

| Feature | Description |
|---------|-------------|
| **Context Engineering** | Structured docs (PROJECT.md, ROADMAP.md, STATE.md) always available |
| **Subagent Execution** | Each plan runs in fresh 200k-token context with 2-3 atomic tasks |
| **XML-Structured Plans** | Precise formatting removes ambiguity |
| **Atomic Git Commits** | Each task = one commit, supports bisecting and reverting |

### Workflow Pattern
1. **Capture** (`/gsd:new-project`): Extract complete project vision
2. **Plan** (`/gsd:create-roadmap`): Generate phased roadmap
3. **Execute** (`/gsd:plan-phase`, `/gsd:execute-plan`): Atomic tasks in fresh contexts
4. **Iterate** (`/gsd:complete-milestone`, `/gsd:add-phase`): Ship and extend

### Additional Resources
- **taches-cc-resources**: Meta-prompts, slash commands, subagents, hooks
- **taches-cc-prompts**: Parallel subagent orchestration with dependency detection
- **Subagent auditors**: skill-auditor, slash-command-auditor, subagent-auditor

### When to Use
- Greenfield projects with clear milestones
- When you need traceable, atomic commits
- Projects requiring structured planning before execution

### Sources
- [GitHub: get-shit-done](https://github.com/glittercowboy/get-shit-done)
- [GitHub: taches-cc-resources](https://github.com/glittercowboy/taches-cc-resources)

---

## 4. Three Developer Loops Framework (Kim & Yegge)

### Overview
From *Vibe Coding* book—organizes AI-assisted development across three timeframes.

### The Loops

| Loop | Timeframe | Focus | Key Strategies |
|------|-----------|-------|----------------|
| **Inner** | Seconds-minutes | Immediate AI collaboration | Decompose tasks, checkpoint via VCS, write specs/tests first, verify claims |
| **Middle** | Hours-days | Context between sessions | External memory systems, project guidelines, design for AI, monitor drift |
| **Outer** | Weeks-months | Strategic architecture | Preserve APIs, partition workspaces, enhanced CI/CD, recovery procedures |

### Core Principle
Each loop operates on: **prevent problems → detect issues early → correct quickly**

### Key Insight
AI generates code faster than humans can write it, requiring systematic management across different timescales.

### When to Use
- Framework for thinking about any agent workflow
- Helps identify gaps in current approach
- Useful for team training and process design

### Source
[IT Revolution: Three Developer Loops](https://itrevolution.com/articles/the-three-developer-loops-a-new-framework-for-ai-assisted-coding/)

---

## 5. Personal Panopticon Model (Molly Cantillon)

### Overview
Running life out of Claude Code as central orchestration point. "The tower belongs to you."

### Architecture

**8 Isolated Agent Instances:**
```
~/nox      - Product (pulls Amplitude, cross-refs GitHub)
~/metrics  - Analytics
~/email    - Inbox zero, auto-drafted replies
~/growth   - Marketing/growth
~/trades   - Personal finance (overnight briefs)
~/health   - Workouts, sleep
~/writing  - Content creation
~/personal - Life admin
```

### Key Patterns

| Pattern | Description |
|---------|-------------|
| **Isolation** | Each domain operates independently |
| **Explicit handoffs** | Context exchange through filesystem, not shared memory |
| **Desktop automation** | When APIs absent, injects mouse/keystroke events |
| **Cron-driven** | Ongoing tasks run on schedule |
| **Caffeinate** | Keeps system awake on runs (airports, sleeping) |
| **SMS checkpoints** | Texts on completion, reply to continue |
| **Trace logging** | All thought traces logged for recursive self-improvement |

### Philosophy
> "Surveilling yourself with the attention span of a thousand clones."

Build personal "legibility infrastructure" for self-governance.

### When to Use
- Life/work integration beyond just coding
- When you need ongoing automation across domains
- Personal productivity optimization

### Source
`research-ephemeral/panopticon.md` (local file)

---

## 6. Multi-Agent Frameworks

### Claude-Flow
Enterprise-grade platform with swarm intelligence.

| Feature | Description |
|---------|-------------|
| **Orchestration modes** | Swarm (quick/temporary) or Hive-Mind (persistent/complex) |
| **Queen-led model** | Specialized workers coordinate under intelligent supervision |
| **AgentDB** | 96x-164x faster semantic vector search |
| **MCP tools** | 100+ tools for comprehensive automation |
| **Performance** | 84.8% SWE-Bench solve rate, 2.8-4.4x speed improvement |

**When to Use**: Enterprise deployments, complex persistent projects, need for swarm coordination.

**Source**: [GitHub: claude-flow](https://github.com/ruvnet/claude-flow)

### CrewAI
Role-based multi-agent orchestration platform.

| Feature | Description |
|---------|-------------|
| **Abstraction level** | Focus on agent objectives, not implementation |
| **Integrations** | Gmail, Teams, Notion, HubSpot, Salesforce, Slack |
| **Observation** | Real-time workflow tracing, every agent step visible |
| **Deployment** | Serverless containers, cloud or on-premises |

**When to Use**: Enterprise teams, need for pre-built integrations, visual development preferred.

**Source**: [CrewAI](https://www.crewai.com/)

### Anthropic Agent Skills
Official Anthropic framework for composable agent capabilities.

| Feature | Description |
|---------|-------------|
| **Progressive disclosure** | Load information only when needed |
| **Structure** | `SKILL.md` with YAML frontmatter, bundled reference files |
| **Platform support** | Claude.ai, Claude Code, Agent SDK, Developer Platform |

**When to Use**: Want official Anthropic patterns, need portable skills across platforms.

**Source**: [Anthropic: Agent Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)

---

## 7. Comparison Matrix

| Workflow | Best For | Complexity | State Management | Parallel Agents |
|----------|----------|------------|------------------|-----------------|
| **Boris's Pattern** | High-velocity dev | Medium | CLAUDE.md | 10-15 |
| **GSD (TÂCHES)** | Greenfield, milestones | Low | .planning/ files | Subagents |
| **Beads** | Maintenance, discovered work | Low | .beads/ + git | Single + subagents |
| **Gas Town** | Large-scale parallel | High | Git hooks | 20-30 |
| **Panopticon** | Life automation | High | Filesystem | 8 domains |
| **Claude-Flow** | Enterprise swarms | High | AgentDB | Many |
| **CrewAI** | Enterprise integrations | Medium | Platform | Team-based |

---

## 8. Recommendations for Template

### Immediate Additions

1. **Add Boris's verification loop pattern** to CLAUDE.md snippets
   - Prompt agents to create verification methods for their work

2. **Document the Three Loops framework** in a reference file
   - Helps users think systematically about their workflow

3. **Add "Help me decide" for workflow selection** during init
   - Ask about parallel agents, state persistence needs, project scale

### Future Considerations

1. **Gas Town integration** for users needing large-scale parallel work
   - Could be an optional add-on workflow

2. **Panopticon-style domain isolation** as an archetype
   - For users wanting life/work automation beyond coding

3. **Agent Skills structure** for portable capabilities
   - Align with Anthropic's official patterns

### Workflow Selection Guide

| If You Need... | Use |
|----------------|-----|
| Simple project, clear milestones | GSD |
| Ongoing maintenance, discovered work | Beads |
| High parallelism, rapid iteration | Boris's pattern |
| Large-scale, state persistence | Gas Town |
| Life automation, multiple domains | Panopticon model |
| Enterprise, integrations | CrewAI or Claude-Flow |

---

## Sources

- [VentureBeat: Claude Code Creator Workflow](https://venturebeat.com/technology/the-creator-of-claude-code-just-revealed-his-workflow-and-developers-are)
- [GitHub: gastown](https://github.com/steveyegge/gastown)
- [GitHub: vc](https://github.com/steveyegge/vc)
- [GitHub: get-shit-done](https://github.com/glittercowboy/get-shit-done)
- [GitHub: taches-cc-resources](https://github.com/glittercowboy/taches-cc-resources)
- [GitHub: claude-flow](https://github.com/ruvnet/claude-flow)
- [CrewAI](https://www.crewai.com/)
- [Anthropic: Agent Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
- [IT Revolution: Three Developer Loops](https://itrevolution.com/articles/the-three-developer-loops-a-new-framework-for-ai-assisted-coding/)
- Local: `research-ephemeral/panopticon.md`
