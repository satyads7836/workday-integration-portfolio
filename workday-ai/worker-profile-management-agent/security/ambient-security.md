# Ambient Security Design

## Purpose

Ambient execution allows the Worker Profile Management Agent to perform an approved background activity without a user initiating each run.

This project uses Ambient mode only for:

- Monitor Worker Profile Data Quality

## Security Model

```text
Approved Schedule or Event
  -> Agent
  -> Ambient Agent System User
  -> Ambient Agent Security Group
  -> Read-Only Worker Scope
  -> Data-Quality Rules
  -> Restricted Exception Report
  -> Audit and Monitoring
```

The ASU and security-group names in this project are illustrative. Actual creation and activation behavior must be validated in an authorized Workday tenant.

## Least-Privilege Design

The Ambient identity should receive only the access required to:

- Read approved synthetic worker-profile field categories
- Evaluate approved data-quality rules
- Publish a minimized exception report
- Write operational and audit records

It must not receive permission to:

- Update worker records
- Change business titles
- Modify compensation
- Initiate unrelated business processes
- Access government identifiers
- Access banking or medical data
- Manage security
- Read unrestricted worker populations

## Population Restriction

The worker population must be explicitly defined.

Illustrative scope:

```text
Worker status: Active
Organization scope: Approved organizations only
Processing mode: Changed records since last successful watermark
Excluded populations: Restricted or confidential groups
```

A real implementation must use approved security and population controls rather than relying only on report filters.

## Schedule and Event Controls

- The trigger must be approved and documented.
- Overlapping runs must be prevented.
- A maximum record threshold must be configured.
- Failed runs must not advance the watermark.
- Trigger changes must follow change control.
- Emergency disablement must be available.
- Schedule and rule versions must be audited.

## Reporting Security

Exception reports must be minimized and delivered only to authorized recipients.

Permitted content:

- Synthetic worker reference
- Rule ID
- Field category
- Severity
- Detection timestamp
- Recommended owner role
- Review status

Prohibited content:

- Full worker profiles
- Credentials or security details
- Unrelated personal information
- Real tenant identifiers
- Sensitive fields not required for remediation

## Failure Behavior

| Failure | Required behavior |
|---|---|
| Ambient ASU disabled | Stop the run |
| Security scope invalid | Stop and notify security support |
| Rule version missing | Stop without evaluating records |
| Worker threshold exceeded | Stop and require review |
| Source read unavailable | Retry only according to policy |
| Report publication fails | Preserve minimized results securely and alert support |
| Audit write fails | Mark the run unsuccessful |
| Repeated failures | Disable or pause according to the runbook |

## Monitoring

Track:

- Run start and completion
- Records evaluated
- Exceptions by severity
- Records skipped
- Records quarantined
- Processing duration
- Source and publication failures
- Authorization failures
- Notification status
- Watermark status
- Consecutive failures

## Security Review Checklist

- [ ] Ambient Skill scope approved
- [ ] Ambient identity documented
- [ ] Security group is least privilege
- [ ] Worker population is restricted
- [ ] Field scope is minimized
- [ ] No worker-update permission exists
- [ ] Recipients are authorized
- [ ] Overlap prevention tested
- [ ] Failure and retry behavior tested
- [ ] Audit and monitoring verified
- [ ] Emergency disablement tested
