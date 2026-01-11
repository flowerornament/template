# Automation Schedule

When does this automation run?

## Schedule

### Primary Schedule

**Frequency**: [Cron expression or description]

**Timezone**: [e.g., UTC, America/Los_Angeles]

**Example cron**: `0 9 * * *` (daily at 9am)

### Schedule Explanation

| Field | Value | Meaning |
|-------|-------|---------|
| Minute | 0 | At minute 0 |
| Hour | 9 | At 9am |
| Day of Month | * | Every day |
| Month | * | Every month |
| Day of Week | * | Every day of week |

## Execution Windows

**Expected Duration**: [How long does a run typically take?]

**Timeout**: [Maximum allowed runtime]

**Retry Policy**: [What happens if it fails?]

## Dependencies

- [ ] Prerequisite 1 must complete first
- [ ] External service X must be available
- [ ] Data source Y must be updated

## Maintenance Windows

**Planned downtime**: [When maintenance might occur]

**Holiday handling**: [Does it run on holidays?]

## History

| Date | Change | Reason |
|------|--------|--------|
| {{DATE}} | Initial schedule | Project created |

## Notes

[Any additional scheduling context]
