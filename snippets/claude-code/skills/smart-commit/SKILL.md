---
name: smart-commit
description: Intelligently decide whether to create a PR or commit directly based on change significance. Analyzes file count, line changes, and core files to recommend the best workflow. Use when completing work and need to commit/push changes.
allowed-tools: Bash, Read
---

# Smart Commit - Intelligent PR vs Direct Commit Decision

Automatically analyzes your staged changes and decides whether to:
1. **Create a Pull Request** (for significant changes requiring review)
2. **Commit and push directly** (for minor changes)

## Decision Criteria

This skill checks if **ANY** of these conditions are met (configurable in `.claude-pr-policy.json`):

- **Files changed** >= threshold (default: 10 files)
- **Lines changed** >= threshold (default: 100 lines)
- **Core files modified** - Critical files defined in policy

## How to Use

When you complete work and need to commit:

**Step 1: Stage your changes**
```bash
git add <files>
```

**Step 2: Run this skill**
```
/smart-commit
```

**Step 3: Claude will:**
1. Analyze changes (files, lines, core files)
2. Load policy from `.claude-pr-policy.json`
3. Display analysis and decision reasoning
4. Execute either `/pr` or `/commit`

## Configuration

Edit `.claude-pr-policy.json` to customize:

```json
{
  "thresholds": {
    "files_changed": 10,
    "lines_changed": 100,
    "core_files": [
      "src/main.ts",
      "package.json",
      "CLAUDE.md"
    ]
  },
  "pr_required_if": "any"
}
```

## Implementation Steps

When invoked, follow these steps:

### 1. Analyze Changes

Run in parallel:
```bash
git status --short
git diff --stat
```

Calculate:
- **files_changed**: Count lines from `git status --short`
- **lines_changed**: Sum additions + deletions from `--stat`

### 2. Load Policy

Read `.claude-pr-policy.json`. If missing, use defaults:
- files_changed: 10
- lines_changed: 100
- core_files: []

### 3. Check Core Files

For each file in `core_files[]`, check if it appears in `git status` output.

### 4. Evaluate & Decide

**If `pr_required_if` is "any":**
- ANY condition true -> Execute `/pr`
- ALL conditions false -> Execute `/commit`

**If `pr_required_if` is "all":**
- ALL conditions true -> Execute `/pr`
- Otherwise -> Execute `/commit`

### 5. Report & Execute

Show user:
- Analysis summary
- Which thresholds exceeded
- Clear decision with reasoning

Then execute `/pr` or `/commit`.

## Manual Override

Force a specific workflow:
```
/pr         # Always create PR
/commit     # Always commit directly
/wip        # Quick WIP commit
```

## Error Handling

- **Missing policy file**: Use defaults
- **Git command fails**: Default to PR (safe)
- **No changes staged**: Inform user, exit
- **Not in git repo**: Error and exit

## Safety Rules

1. Always show reasoning
2. When in doubt, create a PR
3. Verify staged changes exist
4. Use `/pr` and `/commit` as-is
