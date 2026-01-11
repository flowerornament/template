# Project Name

> One-sentence description of what this project does.

## Quick Start

```bash
# Install dependencies
npm install  # or: pip install -e . / cargo build / etc

# Run development
npm run dev

# Run tests
npm test
```

## Project Structure

```
src/           # Source code
tests/         # Test files
docs/          # Documentation
.planning/     # GSD planning files
```

## Development Workflow

### Branching
- `main` - Stable releases
- `dev` - Active development

### Making Changes
1. Work on `dev` branch
2. Small changes: commit directly
3. Large changes (>10 files): create PR

### Commits
- Use conventional prefixes: `feat:`, `fix:`, `chore:`, `docs:`
- Run tests before committing
- Include meaningful commit messages

## Key Files

| File | Purpose |
|------|---------|
| `src/index.ts` | Entry point |
| `package.json` | Dependencies |
| `.planning/PROJECT.md` | Project context |

## Testing

```bash
npm test           # Run all tests
npm test -- --watch  # Watch mode
```

## Commands

| Command | Purpose |
|---------|---------|
| `/commit` | Stage, commit, and push |
| `/pr` | Create pull request |
| `/status` | Git and beads status |

## Context

This project uses:
- GSD for planning (`.planning/`)
- Beads for issue tracking (`.beads/`)
- Conventional commits

See `.planning/PROJECT.md` for full project context.
