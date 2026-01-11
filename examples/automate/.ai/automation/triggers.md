# Automation Triggers

## Trigger Types

### Scheduled (Cron)
Tasks that run on a fixed schedule.

| Task | Cron | Description |
|------|------|-------------|
| [name] | `0 * * * *` | Runs every hour |
| [name] | `0 0 * * *` | Runs daily at midnight |

### Event-Based
Tasks triggered by external events.

| Task | Event | Source |
|------|-------|--------|
| [name] | [event type] | [where it comes from] |

### Manual
Tasks that are triggered manually.

| Task | Command | When to use |
|------|---------|-------------|
| [name] | `[command]` | [scenario] |

---

## Trigger Configuration

### [Task Name]

**Type:** [Cron/Event/Manual]

**Configuration:**
```json
{
  "type": "cron",
  "schedule": "0 * * * *",
  "timezone": "UTC"
}
```

**Conditions:**
- [When should this NOT run]
- [Prerequisites that must be met]

---

## Error Handling

**If trigger fails:**
1. [First action]
2. [Retry logic]
3. [Escalation]

**Retry policy:**
- Max retries: [N]
- Backoff: [Strategy]
- Give up after: [Time/attempts]

---
*Last updated: [DATE]*
