# Testing Strategy

## Objective

Validate that the portfolio design behaves consistently with its documented business, security, privacy, governance, and operational requirements.

This project uses synthetic data and does not execute against a live Workday tenant.

## Test Levels

| Level | Purpose |
|---|---|
| Artifact validation | Confirm JSON, Markdown, links, and Mermaid syntax |
| Skill testing | Validate inputs, processing rules, outputs, and errors |
| Security testing | Validate allowed and denied access paths |
| Workflow testing | Validate confirmation, submission, and approval behavior |
| Ambient testing | Validate scope, thresholds, watermark, retry, and reports |
| Audit testing | Confirm traceability and data minimization |
| Portfolio QA | Confirm accuracy, readability, sanitization, and completeness |

## Retrieve Worker Profile Tests

| ID | Scenario | Expected result |
|---|---|---|
| `RWP-001` | Authorized worker requests own approved fields | Return minimized profile |
| `RWP-002` | Authorized HR user requests an in-scope worker | Return permitted fields |
| `RWP-003` | User requests an out-of-scope worker | Deny and audit |
| `RWP-004` | User requests a restricted field | Omit or deny according to policy |
| `RWP-005` | Invalid synthetic worker ID | Return validation error |
| `RWP-006` | Worker is not found | Return generic not-found result |
| `RWP-007` | Audit service fails | Fail safely according to policy |

## Update Business Title Tests

| ID | Scenario | Expected result |
|---|---|---|
| `UBT-001` | Authorized valid request | Present confirmation and submit |
| `UBT-002` | User declines confirmation | Cancel without submission |
| `UBT-003` | Proposed title is blank | Reject during validation |
| `UBT-004` | Proposed title matches current title | Reject as no change |
| `UBT-005` | Effective date violates policy | Reject during validation |
| `UBT-006` | Duplicate request exists | Return existing-request reference |
| `UBT-007` | User lacks business-process permission | Deny and audit |
| `UBT-008` | Current title changed during processing | Stop and require review |
| `UBT-009` | Approval service is unavailable | Do not apply a direct update |
| `UBT-010` | Audit service fails | Fail safely before submission where required |

## Ambient Data-Quality Tests

| ID | Scenario | Expected result |
|---|---|---|
| `DQM-001` | Valid scheduled run | Evaluate approved population |
| `DQM-002` | Ambient identity disabled | Stop before reading data |
| `DQM-003` | Security scope is broader than approved | Stop and alert |
| `DQM-004` | Rule version is unavailable | Stop without processing |
| `DQM-005` | Worker threshold is exceeded | Stop and retain previous watermark |
| `DQM-006` | Missing business title | Create `DQ-001` exception |
| `DQM-007` | Valid worker record | Create no exception |
| `DQM-008` | Report publication fails | Preserve minimized result and alert |
| `DQM-009` | Run fails midway | Do not advance watermark |
| `DQM-010` | Second run overlaps | Reject or queue according to policy |

## Security Tests

- User can invoke a Skill but lacks underlying worker permission.
- User has worker permission but cannot invoke the Skill.
- User attempts to access a worker outside the authorized population.
- User requests restricted field categories.
- User attempts to bypass confirmation.
- User attempts to submit an unrelated worker change.
- Ambient identity has an accidental write permission.
- Unauthorized recipient attempts to access an exception report.
- Error response is inspected for data leakage.

## Data-Protection Tests

Scan the project for:

- Real names
- Email addresses
- Tenant URLs
- Customer names
- Credentials
- Tokens
- Secrets
- Private keys
- Certificates
- Real worker IDs
- Unmasked screenshots

Only the synthetic names and identifiers intentionally documented by the project are allowed.

## Audit Validation

For each scenario, confirm:

- Correlation ID exists.
- Timestamp exists.
- Agent and Skill versions are recorded.
- Authorization decision is recorded.
- Final status is recorded.
- Error category is recorded when applicable.
- Complete worker profiles are not logged.
- Credentials and secrets are never logged.

## Exit Criteria

Testing is complete when:

- All critical and high-priority tests pass.
- No unresolved security or privacy defect remains.
- JSON parses successfully.
- Markdown headings and code fences are balanced.
- Mermaid diagrams render on GitHub.
- Relative links work.
- Sample data is synthetic.
- Required governance approvals are recorded.
