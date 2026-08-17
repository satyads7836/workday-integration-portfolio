# Skill: Monitor Worker Profile Data Quality

## Summary

| Attribute | Value |
|---|---|
| Skill ID | `monitor-worker-profile-data-quality` |
| Execution mode | Ambient |
| Risk level | Medium |
| Trigger | Approved schedule or event |
| Data access | Read only |
| Output | Data-quality exception report |

## Business Purpose

This Skill identifies incomplete, inconsistent, or invalid worker-profile information and produces an exception report for authorized review.

It is intentionally read only. The Skill does not automatically change worker records.

## Illustrative Trigger

```text
Schedule: Daily at 02:00 tenant-local time
Scope: Active workers in approved organizations
Mode: Incremental records changed since the previous successful run
```

The schedule is illustrative and must be adjusted to operational requirements.

## Illustrative Identity

The design uses an illustrative:

- Ambient Agent System User
- Ambient Agent Security Group
- Read-only worker-profile security scope

Actual identity creation, OAuth configuration, activation behavior, and security assignment must be validated in an authorized Workday tenant.

## Inputs

| Input | Required | Validation |
|---|---:|---|
| Approved worker population | Yes | Must be explicitly limited |
| Data-quality rule set | Yes | Must use an approved version |
| Schedule or event | Yes | Must be authorized |
| Previous-run watermark | Yes | Must be valid and traceable |
| Correlation ID | Yes | Must be unique |
| Report recipients | Yes | Must be authorized to view exceptions |

## Illustrative Tools

1. `read-worker-profile-scope`
2. `evaluate-profile-data-quality`
3. `publish-exception-report`
4. `write-audit-record`

These are conceptual Tool names and not official Workday resource names.

## Example Data-Quality Rules

| Rule ID | Rule | Severity |
|---|---|---|
| `DQ-001` | Business title is missing | High |
| `DQ-002` | Location is missing | Medium |
| `DQ-003` | Worker type is inconsistent with the approved values | High |
| `DQ-004` | Supervisory organization is missing | Critical |
| `DQ-005` | Worker status and termination date are inconsistent | Critical |
| `DQ-006` | Profile has not been reviewed within the defined period | Low |

The portfolio uses synthetic fields and results.

## Processing Flow

1. Receive the approved schedule or event.
2. Validate that the Ambient Skill is active.
3. Validate the Ambient identity and security scope.
4. Load the approved data-quality rule version.
5. Read only the authorized worker population.
6. Evaluate each record against the rules.
7. Classify exceptions by severity.
8. Produce a minimized exception report.
9. Notify authorized recipients.
10. Record run metrics, watermark, and audit results.

## Security Requirements

- Ambient Agent Security Group
- Read-only access to approved worker fields
- Restricted worker population
- Approved report recipients
- No worker update permission
- No compensation, government ID, banking, or medical-data access
- Audit and monitoring access

The Ambient identity must not inherit unnecessary permissions from an administrator or integration account.

## Output Requirements

The exception report should contain only:

- Synthetic worker reference
- Rule ID
- Field category
- Exception description
- Severity
- Detected timestamp
- Recommended owner role
- Review status

It should not reproduce a complete worker profile.

## Operational Controls

- Prevent overlapping runs.
- Stop when the approved record threshold is exceeded.
- Retain the previous successful watermark.
- Retry only transient failures.
- Quarantine malformed records.
- Alert support when failure thresholds are reached.
- Record rule-set and agent-definition versions.
- Permit a controlled disable or rollback.

## Error Handling

| Condition | Response |
|---|---|
| Ambient identity is disabled | Stop the run |
| Security scope is invalid | Stop and alert security support |
| Rule set is missing | Stop without evaluating records |
| Source read fails | Retry according to policy |
| Threshold is exceeded | Stop and require review |
| Report publication fails | Preserve results securely and alert support |
| Audit write fails | Mark the run unsuccessful |

## Audit and Metrics

Record:

- Correlation and run IDs
- Start and completion timestamps
- Agent and Skill versions
- Rule-set version
- Worker population category
- Records evaluated
- Exceptions by severity
- Records skipped or quarantined
- Previous and new watermarks
- Notification status
- Final run status
- Error category

## Acceptance Criteria

- Only the approved worker population is evaluated.
- The Skill has no worker-update permission.
- Every exception maps to an approved rule.
- Reports are visible only to authorized recipients.
- Runs cannot overlap.
- Failed runs do not advance the watermark.
- Every run produces audit and operational metrics.
- All portfolio data is synthetic.
