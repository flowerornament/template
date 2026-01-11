# Automation Outputs

## Output Types

### Logs
**Location:** `logs/`
**Format:** [JSON/Plain text/etc]
**Retention:** [How long kept]

Example:
```
[example log format]
```

### Reports
**Location:** [Where generated]
**Format:** [Format]
**Frequency:** [When produced]

### Notifications
**Channels:** [Where notifications go]
**Conditions:** [What triggers notifications]

---

## Output Details

### [Output Name]

**Type:** [Log/Report/Notification/File]
**Location:** `[path]`
**Format:** [Format]

**Contents:**
- [What's included]
- [Key fields/sections]

**Example:**
```
[example output]
```

---

### [Output Name]

**Type:** [Type]
**Location:** `[path]`

**Contents:**
- [What's included]

---

## Success Outputs

What to expect when automation succeeds:

1. [Expected output 1]
2. [Expected output 2]
3. [Status update]

## Failure Outputs

What to expect when automation fails:

1. [Error log]
2. [Notification]
3. [Beads issue created]

---

## Cleanup

**Log rotation:**
- Keep last [N] logs
- Archive after [time]
- Delete after [time]

**Temporary files:**
- Location: [path]
- Cleanup: [When/how]

---
*Last updated: [DATE]*
