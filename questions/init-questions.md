# Project Initialization Questions

Questions to ask when initializing a new project. Adapt phrasing to feel natural in conversation.

---

## Core Questions

### 1. Project Type

**Ask**: "What kind of project is this?"

| Answer | Description | Typical Setup |
|--------|-------------|---------------|
| Greenfield | New build with clear end goal | GSD + master only |
| Maintenance | Ongoing system, evolves over time | beads + beads-sync |
| Complex | Multiple contributors, needs coordination | beads + PR workflow |
| Script | Quick utility, ship and done | minimal, no tracking |

**Default**: Greenfield (most common for new projects)

---

### 2. Task Management System

**Ask**: "How do you want to track work?"

| Answer | When to Use | Creates |
|--------|-------------|---------|
| GSD | Phases and milestones, clear roadmap | .planning/ directory |
| bd (beads) | Discovered work, dependencies, long-term | .beads/ directory |
| Both | Major features (GSD) + bugs/issues (bd) | Both directories |
| None | Very simple project, just git | Nothing |

**Default**: GSD for greenfield, beads for maintenance

---

### 3. Git Workflow

**Ask**: "How should we handle git branches?"

| Answer | Branches | When to Use |
|--------|----------|-------------|
| Simple | master/main only | Solo dev, direct commits OK |
| Beads sync | main + beads-sync | Using beads, want issues off main |
| PR workflow | main + dev + beads-sync | Team, need code review |

**Default**: Match task system (GSD → simple, beads → beads sync)

---

### 4. Documentation Level

**Ask**: "How much documentation structure do you need?"

| Answer | Creates | When to Use |
|--------|---------|-------------|
| Minimal | CLAUDE.md only | Simple projects, scripts |
| Standard | + .ai/architecture.md | Most projects |
| Full | + AGENTS.md + .claude/commands/ | Complex, multi-contributor |

**Default**: Standard (good balance)

---

### 5. Project Context

**Ask**: "What are you building? (one sentence)"

Used to:
- Populate PROJECT.md description
- Customize CLAUDE.md header
- Seed architecture.md if created

**Example answers**:
- "A CLI tool for managing music torrents"
- "My nix-darwin system configuration"
- "A Zed extension for SuperCollider"

---

## Decision Matrix

| Type | Task | Git | Docs |
|------|------|-----|------|
| Greenfield | GSD | simple | minimal/standard |
| Maintenance | beads | beads-sync | standard |
| Complex | beads | PR workflow | full |
| Script | none | simple | minimal |

---

## Follow-up Questions (If Needed)

### Tech Stack
"What languages/frameworks? (helps with conventions)"

### Team Size
"Solo or team?" (affects git workflow recommendation)

### Timeline
"Quick project or long-term?" (affects documentation level)

---

## Anti-Patterns to Avoid

- Don't over-engineer simple projects (script doesn't need .ai/)
- Don't under-document complex projects (multi-file changes need architecture docs)
- Don't mix conflicting workflows (GSD phases + beads milestones = confusion)
