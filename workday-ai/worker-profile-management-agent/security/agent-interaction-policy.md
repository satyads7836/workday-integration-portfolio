# Agent Interaction Policy

## Purpose

This policy defines who may interact with the Delegate Skills of the Worker Profile Management Agent and under what conditions.

It is an illustrative portfolio policy, not a tenant security configuration.

## Scope

The policy applies to:

- Retrieve Worker Profile
- Update Worker Business Title

The Ambient data-quality Skill is governed separately through its Ambient identity and security design.

## Access Principles

- Deny access by default.
- Grant access through approved role-based populations.
- Separate Skill availability from Tool and API authorization.
- Restrict target-worker populations.
- Apply least privilege.
- Require additional controls for write requests.
- Review access regularly.
- Audit all invocation attempts.

## Illustrative Access Matrix

| User population | Retrieve Worker Profile | Update Worker Business Title |
|---|---:|---:|
| Worker viewing self | Allow | Deny |
| Manager viewing permitted team | Limited | Conditional |
| HR partner for assigned population | Allow | Conditional |
| HR administrator | Conditional | Conditional |
| Integration support | Troubleshooting only | Deny |
| Security administrator | Security review only | Deny |
| Unauthenticated user | Deny | Deny |
| User outside approved population | Deny | Deny |

`Conditional` means that Skill availability and all underlying permissions, validations, and approvals must succeed.

## Runtime Checks

For every Delegate request, evaluate:

1. Is the user authenticated?
2. Is the Skill available to the user?
3. Is the target worker within the user’s authorized population?
4. Does the user have the required Tool and resource permissions?
5. Is the requested purpose approved?
6. Are the requested fields or action within scope?
7. Have required confirmation and approvals been satisfied?
8. Can the result be audited safely?

If any required check fails, execution must stop.

## Self-Service Retrieval

A worker may retrieve approved fields from their own synthetic profile.

The policy must still restrict sensitive fields and must not assume that self-service permits access to every worker-data category.

## Manager and HR Retrieval

Manager and HR access must be limited by the applicable authorized worker population.

The agent must not use a broad technical identity to return records that the requesting user cannot access directly.

## Business-Title Updates

Business-title requests require:

- Approved initiator population
- Target-worker authorization
- Current-value validation
- Proposed-value validation
- Effective-date validation
- Business reason
- User confirmation
- Applicable approval routing
- Audit record

Interaction access does not permit direct approval or bypass configured business processes.

## Access Review

Review the policy:

- Before initial activation
- After a Skill or Tool change
- After a security-policy change
- When the target population changes
- Following a security incident
- At the organization’s defined periodic interval

## Audit Events

Record:

- Allowed and denied invocation attempts
- Skill ID
- Actor role category
- Target-worker category
- Authorization decision
- Decision reason category
- Confirmation result
- Final outcome
- Correlation ID and timestamp

Do not record unnecessary worker information in access logs.

## Policy Owner

Illustrative owner: HR Technology Product Owner

Required reviewers:

- Workday Security Administrator
- Privacy Reviewer
- Workday Integration Lead
- Applicable business-process owner
