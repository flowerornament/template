# Automation: [Name]

> [What this automation does, one sentence]

## Purpose

[Why this automation exists and what problem it solves]

## Schedule

| Trigger | Frequency | Description |
|---------|-----------|-------------|
| [Cron/Event] | [When] | [What happens] |

See `.ai/automation/schedule.md` for full schedule details.

## How It Works

```
[Trigger event]
    ↓
[Step 1]
    ↓
[Step 2]
    ↓
[Output/Result]
```

## Structure

```
.ai/automation/
├── schedule.md    # When this runs
├── triggers.md    # What triggers execution
└── outputs.md     # What gets produced

logs/              # Execution history
config/            # Runtime configuration
```

## Running Manually

```bash
# Trigger the automation manually
[command to run]

# Check last execution
cat logs/latest.log
```

## Monitoring

### Success Indicators
- [What indicates success]
- [Expected outputs]

### Failure Indicators
- [What indicates failure]
- [Error patterns to watch]

## Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| [setting] | [value] | [what it controls] |

See `config/` for configuration files.

## Troubleshooting

### [Common issue]
**Symptoms:** [What you see]
**Solution:** [How to fix]

### [Common issue]
**Symptoms:** [What you see]
**Solution:** [How to fix]

## Commands

| Command | Purpose |
|---------|---------|
| `bd ready` | Check pending issues |
| `bd create` | Report problem |
| `bd close` | Mark issue resolved |

## Context

This is an agent-managed automation. Claude may:
- Monitor execution logs
- Fix issues that arise
- Update configuration as needed
- Report problems via beads
