# Delegate Security Design

## Purpose

Delegate execution occurs when a user asks the Worker Profile Management Agent to perform an action on the user’s behalf.

This project uses Delegate mode for:

- Retrieve Worker Profile
- Update Worker Business Title

## Security Model

```text
Authenticated User
&#x20; -> Agent Interaction Policy
&#x20; -> Skill Availability
&#x20; -> User and Target-Worker Authorization
&#x20; -> Tool Security
&#x20; -> Domain or Business-Process Security
&#x20; -> Runtime Validation
&#x20; -> Controlled Result
&#x20; -> Audit Record
```

The agent must not provide permissions that the user does not already have for the underlying operation.

## Interaction Access

The Agent Interaction Policy defines which approved user populations may interact with each Delegate Skill.

Illustrative access:

| Skill | Intended population |
|---|---|
| Retrieve Worker Profile | Workers viewing themselves and authorized HR users |
| Update Worker Business Title | Authorized HR or management roles |

This table is a design example, not a tenant security assignment.

## Retrieve Worker Profile

Required checks:

1. User is authenticated.
2. User can invoke the Skill.
3. Target worker is in the user’s authorized population.
4. User can access every requested field category.
5. Response is minimized to the approved purpose.
6. Retrieval is audited.

The agent must not return a full worker profile when only a business title is requested.

## Update Worker Business Title

Required checks:

1. User is authenticated.
2. User can invoke the Skill.
3. User can view the target worker.
4. User can initiate the applicable worker change.
5. Current business title matches the latest permitted record.
6. Proposed title and effective date are valid.
7. User confirms the request.
8. Configured approval routing is preserved.
9. Submission and outcome are audited.

The agent must not directly update the worker record when a configured business process or approval is required.

## Confirmation Pattern

Before submitting a change, present:

```text
Target worker: SYN-W-1002
Current title: Integration Consultant
Proposed title: Senior Integration Consultant
Effective date: 2026-09-01
Business reason: Approved role progression
Approval required: Yes
```

The user must explicitly confirm the request.

## Failure Behavior

| Failure | Required behavior |
|---|---|
| Skill access denied | Stop without calling the worker resource |
| Worker access denied | Return a generic authorization result |
| Restricted field requested | Omit the field and audit the decision |
| Current value changed | Require the request to be reviewed again |
| Input validation failed | Do not submit |
| Approval service unavailable | Do not apply a direct update |
| Audit unavailable | Fail safely for the high-risk update |

## Privacy Controls

- Retrieve only necessary fields.
- Do not expose sensitive data in prompts or errors.
- Do not retain complete worker responses in logs.
- Use synthetic records in this portfolio.
- Apply approved retention periods in a real implementation.

## Audit Events

Record:

- Interaction attempt
- Authorization decision
- Validation outcome
- Confirmation
- Submission
- Approval status
- Completion or failure
- Security-policy denial
- Tool or service error

## Review Checklist

- \[ ] Skill population approved
- \[ ] Target-worker restrictions validated
- \[ ] Required domains identified
- \[ ] Required business-process policies identified
- \[ ] Confirmation tested
- \[ ] Approval routing tested
- \[ ] Negative security tests passed
- \[ ] Audit records verified
- \[ ] Sensitive-data exposure tests passed
