# {{PROJECT_NAME}}

{{PROJECT_DESCRIPTION}}

## Task Tracking

This project uses **GSD** (Get Shit Done) for phase-based development.

### Workflow
```bash
/gsd:progress         # Check current state
/gsd:research-phase N # Research before planning (if needed)
/gsd:plan-phase N     # Create execution plan
/gsd:execute-plan     # Execute the plan
```

### Key Files
- `.planning/PROJECT.md` - Project context and goals
- `.planning/ROADMAP.md` - Phases and milestones
- `.planning/STATE.md` - Current position and decisions

### Research-First Pattern
Check ROADMAP.md for phases marked "Research: Likely" - run `/gsd:research-phase` before `/gsd:plan-phase` for those.

## Build/Run

```bash
# Project-specific commands here
```

## Project Knowledge

When you learn something significant about this project, document it in `.ai/`:
- `architecture.md` - System structure, component relationships, data flow
- `decisions.md` - Key choices and rationale
- `learnings.md` - Discoveries, gotchas, patterns

Create these files when there's real content, not before. Update them as the project evolves.

## Structure

Key directories and files.
