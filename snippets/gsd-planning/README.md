# GSD .planning Structure

The Get Shit Done (GSD) workflow uses a `.planning/` directory for structured project management across sessions.

## Structure

```
.planning/
├── PROJECT.md              # Core project context (what, why, how)
├── ROADMAP.md              # Milestones and phases overview
├── STATE.md                # Current position and recent activity
├── config.json             # GSD configuration
├── LEARNINGS.md            # Optional: accumulated learnings
├── MILESTONES.md           # Optional: milestone list (if many)
├── phases/
│   └── XX-phase-name/
│       ├── XX-RESEARCH.md  # Research notes (if needed)
│       ├── XX-01-PLAN.md   # Execution plan
│       └── XX-01-SUMMARY.md # Post-execution summary
└── milestones/
    └── vX.X-ROADMAP.md     # Archived milestone roadmaps
```

## File Purposes

| File | Purpose | When to Use |
|------|---------|-------------|
| PROJECT.md | Define the project's goal, approach, scope, decisions | Always - core context |
| ROADMAP.md | Track phases and milestones | Always - progress overview |
| STATE.md | Current position, what to do next | Always - session startup |
| config.json | GSD tool configuration | Always - minimal config |
| LEARNINGS.md | Accumulated insights and decisions | Optional - complex projects |
| XX-RESEARCH.md | Pre-planning investigation notes | When phase needs exploration |
| XX-01-PLAN.md | Concrete execution steps | Before implementing a phase |
| XX-01-SUMMARY.md | What was done, what was learned | After completing a plan |

## Workflow

1. **New project**: Create PROJECT.md with goals and approach
2. **Plan work**: Create ROADMAP.md with milestones and phases
3. **Start phase**: Update STATE.md, optionally create RESEARCH.md
4. **Plan phase**: Create XX-01-PLAN.md with tasks
5. **Execute**: Work through plan, update STATE.md
6. **Complete**: Create XX-01-SUMMARY.md, update ROADMAP.md progress
7. **Repeat**: Move to next phase or milestone

## GSD Commands

```bash
/gsd:new-project     # Initialize PROJECT.md with deep context gathering
/gsd:create-roadmap  # Create ROADMAP.md with phases
/gsd:plan-phase N    # Create detailed execution plan for phase N
/gsd:execute-plan    # Execute the current PLAN.md
/gsd:progress        # Check project status, route to next action
```

## When to Use GSD vs Beads

| Use Case | Tool |
|----------|------|
| Multi-phase project with clear milestones | GSD |
| Bug tracking, issue management | Beads |
| Both planning and issue tracking needed | GSD + Beads |
| Simple project, quick tasks | Neither - just CLAUDE.md |
