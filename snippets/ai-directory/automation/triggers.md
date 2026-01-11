# Automation Triggers

What causes this automation to execute?

## Trigger Types

### Scheduled (Cron)

Primary trigger - see schedule.md for timing details.

### Manual

**Command**: `[how to trigger manually]`

**When to use**: [circumstances for manual runs]

### Event-Based

| Event | Source | Action |
|-------|--------|--------|
| [Event name] | [Where it comes from] | [What happens] |

### Webhook (if applicable)

**Endpoint**: [URL]

**Method**: POST

**Payload format**:
```json
{
  "trigger": "webhook",
  "data": {}
}
```

## Trigger Conditions

### Prerequisites

Before any trigger can fire:
- [ ] Condition 1
- [ ] Condition 2

### Guards

Execution will be skipped if:
- [ ] Guard condition 1
- [ ] Guard condition 2

## Trigger Priority

If multiple triggers fire simultaneously:

1. [Highest priority trigger]
2. [Next priority]
3. [Lowest priority]

## Debouncing

**Minimum interval**: [time between runs]

**Behavior**: [queue, skip, or replace]

## Monitoring

**How to check trigger status**: [command or dashboard]

**Alert on missed triggers**: [yes/no, how]

## Notes

[Additional trigger context]
