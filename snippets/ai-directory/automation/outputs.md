# Automation Outputs

What does this automation produce?

## Output Summary

| Output | Type | Location | Frequency |
|--------|------|----------|-----------|
| [Output 1] | [file/api/notification] | [where] | [when] |

## Detailed Outputs

### Output 1: {{OUTPUT_NAME}}

**Type**: File | API Call | Notification | Database | Other

**Location**: [Where output goes]

**Format**: [JSON, CSV, text, etc.]

**Schema/Structure**:
```
[Example output structure]
```

**Retention**: [How long outputs are kept]

**Consumers**: [Who/what uses this output]

---

## Logs

### Execution Logs

**Location**: `logs/`

**Format**: [Log format description]

**Retention**: [How long logs are kept]

**Log Levels**:
- ERROR: Failures requiring attention
- WARN: Potential issues
- INFO: Normal operation
- DEBUG: Detailed troubleshooting

### Sample Log Entry

```
[timestamp] [level] [message]
```

## Notifications

### Success

**Channel**: [email, slack, etc.]

**Recipients**: [who gets notified]

**Content**: [what the notification contains]

### Failure

**Channel**: [email, slack, etc.]

**Recipients**: [who gets notified]

**Escalation**: [what happens if not acknowledged]

## Artifacts

### Temporary Files

**Location**: [where temp files go]

**Cleanup**: [when/how they're removed]

### Persistent Artifacts

**Location**: [where artifacts are stored]

**Versioning**: [how versions are tracked]

## Output Validation

**How to verify outputs are correct**:
1. [Validation step 1]
2. [Validation step 2]

**Known good output example**:
```
[Example of correct output]
```

## Notes

[Additional output context]
