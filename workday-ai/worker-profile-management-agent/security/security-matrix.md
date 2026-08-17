# Agent Security Matrix

## Security Principle

Successful execution requires more than access to an Agent or Skill.

```text
Skill availability
+
Execution identity
+
Tool authorization
+
Domain or business-process security
+
Runtime validation
=
Permitted execution
```

## Skill Security Matrix

| Skill | Mode | Actor or identity | Data action | Risk | Required controls |
|---|---|---|---|---|---|
| Retrieve Worker Profile | Delegate | Authorized user with agent context | Read | Medium | Interaction policy, worker-population restriction, domain security, field minimization, audit |
| Update Worker Business Title | Delegate | Authorized HR or management user with agent context | Controlled change request | High | Interaction policy, domain security, business-process security, validation, confirmation, approvals, separation of duties, audit |
| Monitor Worker Profile Data Quality | Ambient | Illustrative Ambient ASU | Read and report | Medium | Ambient security group, read-only domain access, limited population, approved schedule, restricted recipients, audit |

## Tool Security Matrix

| Tool | Read | Write | Delegate | Ambient | Primary security concern |
|---|---:|---:|---:|---:|---|
| Internal Authorization Check | Yes | No | Yes | No | Correct evaluation of user and worker scope |
| Get Worker Profile | Yes | No | Yes | No | Restricted worker fields and populations |
| Validate Business Title | Yes | No | Yes | No | Current-value and policy validation |
| Request Business Title Change | Yes | Request | Yes | No | Business-process initiation and approval routing |
| Read Worker Profile Scope | Yes | No | No | Yes | Least-privilege Ambient access |
| Evaluate Profile Data Quality | Yes | No | No | Yes | Approved rules and no automatic correction |
| Publish Exception Report | Yes | Report | No | Yes | Recipient authorization and minimization |
| Write Audit Record | Yes | Append | Yes | Yes | Integrity, minimization, and retention |

## Delegate Security Evaluation

For Delegate execution, validate:

1. The user can interact with the Skill.
2. The user can access the target worker population.
3. The user has the permissions required by the Tool.
4. The requested action is within the Skill’s approved scope.
5. Runtime validation succeeds.
6. Required approval routing is preserved.
7. The action and outcome are audited.

The agent must not expand the user’s access.

## Ambient Security Evaluation

For Ambient execution, validate:

1. The Ambient Skill is approved and active.
2. The Ambient ASU is enabled only when required.
3. The Ambient Agent Security Group has least-privilege access.
4. The worker population and fields are restricted.
5. No worker-update permission is assigned.
6. The schedule or event is approved.
7. Report recipients are authorized.
8. Runs, exceptions, and failures are audited.

## Data Classification

| Data category | Portfolio treatment |
|---|---|
| Worker records | Synthetic only |
| Worker identifiers | Synthetic format only |
| Tenant and customer information | Prohibited |
| Credentials and secrets | Prohibited |
| Screenshots | Sanitized and reviewed |
| Audit records | Synthetic and minimized |
| API payloads | Illustrative, with no real endpoints or IDs |

## Separation of Duties

| Activity | Recommended owner |
|---|---|
| Approve business purpose | HR Technology Product Owner |
| Design Skills and Tools | Workday Integration Lead |
| Assign security | Workday Security Administrator |
| Review worker-data usage | Privacy Reviewer |
| Approve architecture | Architecture Reviewer |
| Execute testing | Independent test role |
| Approve activation | Business owner and security approver |
| Review production monitoring | Operations or support role |

## Deny-by-Default Conditions

Execution must stop when:

- The actor cannot be authenticated.
- Skill availability cannot be confirmed.
- Worker scope cannot be evaluated.
- Required domain or business-process access is missing.
- Input validation fails.
- The user declines the confirmation.
- The Ambient security scope is broader than approved.
- Audit recording is unavailable for a high-risk action.
- A credential, token, or real worker record is detected in a portfolio artifact.
