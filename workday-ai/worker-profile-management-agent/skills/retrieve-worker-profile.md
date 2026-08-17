# Skill: Retrieve Worker Profile

## Summary

| Attribute | Value |
|---|---|
| Skill ID | `retrieve-worker-profile` |
| Execution mode | Delegate |
| Risk level | Medium |
| Primary actor | Authorized worker or HR user |
| Data access | Read only |
| Output | Minimized worker-profile response |

## Business Purpose

This Skill allows an authorized user to retrieve permitted worker-profile information through the Worker Profile Management Agent.

The response must be limited by the requesting user’s security context and business purpose. Access to the Agent or Skill does not automatically grant access to the underlying worker data.

## Example Requests

```text
Show my worker profile.
Show the business title and organization for worker SYN-W-1002.
Summarize the permitted profile information for worker SYN-W-1003.
```

All worker identifiers in this repository are synthetic.

## Inputs

| Input | Required | Validation |
|---|---:|---|
| Requesting user context | Yes | Must be authenticated and authorized |
| Target worker ID | Yes | Must match the synthetic identifier format |
| Requested fields | No | Must be restricted to approved fields |
| Business purpose | Yes | Must match an approved retrieval purpose |
| Correlation ID | Yes | Must be unique and traceable |

## Illustrative Tools

1. `internal-authorization-check`
2. `get-worker-profile`
3. `write-audit-record`

These are conceptual Tool names and not official Workday resource names.

## Processing Flow

1. Receive the user’s request.
2. Confirm that the Skill is available to the user.
3. Validate the target worker identifier.
4. evaluate the user’s underlying worker-data permissions.
5. Determine the fields the user is permitted to view.
6. Retrieve only the permitted fields.
7. Remove fields that are unnecessary for the stated purpose.
8. Return the minimized response.
9. Write an audit record.

## Security Requirements

The Skill requires both:

```text
Agent interaction access
+
Underlying worker-data permissions
```

Security controls include:

- Agent Interaction Policy
- User-permission evaluation
- Worker-population restrictions
- Field-level data minimization
- Read-only access
- Audit logging

The Skill must not return a broader result simply because the agent’s technical identity can access it.

## Approved Illustrative Fields

Depending on the user’s authorization, a response may contain:

- Synthetic worker ID
- Preferred display name
- Business title
- Supervisory organization
- Worker type
- Location
- Worker status

The following fields are excluded from the portfolio scenario:

- Government identifiers
- Bank information
- Compensation
- Medical information
- Personal contact details
- Authentication or security data

## Error Handling

| Condition | Response |
|---|---|
| User lacks interaction access | Deny the Skill request |
| User lacks worker-data permission | Return an authorization failure |
| Invalid worker ID | Return a validation error |
| Worker not found | Return a generic not-found result |
| Requested field is restricted | Omit the field and record the decision |
| Resource unavailable | Return a controlled service error |
| Audit write fails | Fail safely and alert support |

Error messages must not reveal restricted worker information.

## Audit Requirements

The audit record should include:

- Correlation ID
- Timestamp
- Skill ID
- Requesting actor reference
- Synthetic target-worker reference
- Requested field categories
- Authorization outcome
- Returned field categories
- Final status
- Error category, if applicable

Do not store complete worker-profile responses in an audit record.

## Acceptance Criteria

- Unauthorized users cannot invoke the Skill.
- Authorized users receive only permitted fields.
- Restricted fields are never returned.
- The response uses synthetic data in this portfolio.
- Every request produces a traceable audit result.
- Errors do not disclose protected information.
- No worker record is modified.
