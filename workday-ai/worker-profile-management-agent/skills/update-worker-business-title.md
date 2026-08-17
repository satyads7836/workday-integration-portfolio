# Skill: Update Worker Business Title

## Summary

| Attribute | Value |
|---|---|
| Skill ID | `update-worker-business-title` |
| Execution mode | Delegate |
| Risk level | High |
| Primary actor | Authorized HR or management user |
| Data access | Controlled update request |
| Output | Submitted change request and audit result |

## Business Purpose

This Skill allows an authorized user to request a worker business-title change through a controlled process.

The Skill does not bypass Workday security or approval routing. A real implementation must use the applicable configured business process, domain security, validation rules, and approvals.

## Example Request

```text
Change worker SYN-W-1002 from Integration Consultant to Senior Integration Consultant effective 2026-09-01.
```

All identifiers and values in this repository are synthetic.

## Inputs

| Input | Required | Validation |
|---|---:|---|
| Requesting user context | Yes | Must be authenticated and authorized |
| Target worker ID | Yes | Must match the synthetic identifier format |
| Current business title | Yes | Must match the current permitted record |
| Proposed business title | Yes | Must meet naming and policy rules |
| Effective date | Yes | Must be a valid approved date |
| Business reason | Yes | Must be meaningful and within the approved purpose |
| Correlation ID | Yes | Must be unique and traceable |

## Illustrative Tools

1. `internal-authorization-check`
2. `validate-business-title`
3. `request-business-title-change`
4. `write-audit-record`

These are conceptual Tool names and not official Workday resource names.

## Processing Flow

1. Receive the user’s requested title change.
2. Confirm that the Skill is available to the user.
3. Evaluate the user’s underlying permissions.
4. Validate the worker identifier and current title.
5. Validate the proposed title, effective date, and business reason.
6. Check for a duplicate or conflicting open request.
7. Present a confirmation summary to the user.
8. Submit the request through the configured approval process.
9. Return the request reference and status.
10. Write an audit record.

## Confirmation Requirement

Before submission, the agent must clearly present:

```text
Target worker
Current business title
Proposed business title
Effective date
Business reason
Approval process required
```

The request must not be submitted until the authorized user confirms the details.

## Security Requirements

The Skill requires:

- Agent Interaction Policy access
- Permission to view the target worker
- Permission to initiate the applicable change
- Required domain security
- Required business-process security
- Approval routing
- Audit access

Skill availability alone is insufficient.

## Validation Rules

- Worker must be active on the proposed effective date.
- Proposed title must not be blank.
- Proposed title must differ from the current title.
- Title must comply with the approved naming standard.
- Effective date must follow configured policy.
- Business reason must be provided.
- Duplicate open requests must be rejected.
- Target worker must be within the user’s authorized population.

## Separation of Duties

The same person should not automatically initiate and approve a high-risk change when organizational policy requires independent approval.

The agent must not:

- Grant additional security
- Alter approval routing
- Approve its own request
- Modify compensation
- Change a job profile
- Change supervisory organization
- Update unrelated worker information

## Error Handling

| Condition | Response |
|---|---|
| User lacks Skill access | Deny the request |
| User lacks update permission | Return an authorization failure |
| Current value mismatch | Stop and request refreshed information |
| Invalid proposed title | Return a validation error |
| Duplicate request exists | Stop and return the existing request reference |
| Approval process unavailable | Do not apply a direct update |
| Submission fails | Return a controlled error and audit the failure |
| Audit write fails | Fail safely and alert support |

## Audit Requirements

The audit record should include:

- Correlation ID
- Timestamp
- Skill ID
- Requesting actor reference
- Synthetic target-worker reference
- Previous business title
- Proposed business title
- Effective date
- Business reason category
- Confirmation timestamp
- Submitted request reference
- Approval status
- Final outcome
- Error category, if applicable

## Acceptance Criteria

- Only authorized users can initiate the Skill.
- All inputs are validated before submission.
- User confirmation is captured.
- The configured approval process is preserved.
- Duplicate requests are prevented.
- No unrelated worker fields are modified.
- Every attempt produces a traceable audit result.
- All portfolio examples use synthetic data.
