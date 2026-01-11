# {{PROJECT_NAME}}

{{PROJECT_DESCRIPTION}}

## Purpose

This is a **research project** - the goal is investigation and understanding, not code output.

## Task Tracking

This project uses **bd** (beads) for tracking research tasks.

### Quick Reference
```bash
bd ready              # See available research tasks
bd show <id>          # View task details
bd create --title="Research: <topic>" --type=task
bd update <id> --status=in_progress
bd close <id>         # Mark investigation complete
bd sync               # Sync with remote
```

## Research Structure

Investigation notes are organized in `.ai/research/`:

- **questions.md** - What we're trying to understand
- **findings.md** - What we've learned
- **sources.md** - References and links

## Workflow

1. **Define questions** - Add research questions to questions.md
2. **Create tasks** - Use bd to track investigation work
3. **Document findings** - Record discoveries in findings.md
4. **Cite sources** - Keep references in sources.md
5. **Close tasks** - Mark questions as answered

## Output Expectations

- This project produces **knowledge**, not code
- Findings should be clear enough for future reference
- Sources should be properly cited
- Questions should have definitive answers or documented blockers

## Session End

Before ending any session:
1. Update findings.md with new discoveries
2. Close completed research tasks: `bd close <id>`
3. Sync task state: `bd sync`
4. Push changes: `git push`
