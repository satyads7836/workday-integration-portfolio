# Agent Lifecycle

## Lifecycle Model

```mermaid
flowchart LR
&#x20;   A\[Idea] --> B\[Define]
&#x20;   B --> C\[Review]
&#x20;   C --> D\[Test]
&#x20;   D --> E\[Approve]
&#x20;   E --> F\[Activate]
&#x20;   F --> G\[Monitor]
&#x20;   G --> H{Change Needed?}
&#x20;   H -- Yes --> B
&#x20;   H -- No --> I{Retire?}
&#x20;   I -- No --> G
&#x20;   I -- Yes --> J\[Deactivate]
&#x20;   J --> K\[Archive Evidence]
```

## 1. Idea

Define the business problem before designing the agent.

Required outputs:

- Business problem
- Intended users
- Expected value
- Initial risk classification
- Executive or business sponsor

## 2. Define

Create the design artifacts:

- Agent Definition
- Skill descriptions
- Tool mappings
- Execution-mode decisions
- Security model
- Data classification
- Audit requirements
- Testing strategy
- Monitoring plan

The initial project lifecycle status is `design`.

## 3. Review

Required reviewers:

| Review | Focus |
|---|---|
| Business | Purpose, scope, and expected outcomes |
| Security | Least privilege, domains, business processes, and identities |
| Privacy | Worker-data necessity, minimization, and retention |
| Architecture | Skills, Tools, resources, dependencies, and failure behavior |
| Operations | Monitoring, support, retry, rollback, and recovery |

A rejected review returns the project to Define.

## 4. Test

Testing must include:

- Positive functional scenarios
- Authorization failures
- Target-population restrictions
- Restricted-field requests
- Invalid and conflicting inputs
- User-confirmation behavior
- Approval routing
- Ambient scope validation
- Failure and retry handling
- Audit-record validation
- Sensitive-data exposure tests
- Mermaid and Markdown rendering
- JSON validation

## 5. Approve

Activation approval requires:

- Approved Skill scope
- Approved Tool mapping
- Security validation
- Privacy validation
- Test evidence
- Monitoring readiness
- Support ownership
- Rollback plan
- Business-owner approval

Approval evidence must be traceable to the Agent Definition version.

## 6. Activate

Activation should follow controlled change management.

Illustrative activation checklist:

- Confirm approved version.
- Confirm required security.
- Confirm identities are in the expected state.
- Enable only approved Skills.
- Validate monitoring.
- Perform a limited smoke test.
- Record activation timestamp and approver.
- Start enhanced monitoring.

This portfolio does not perform a real tenant activation.

## 7. Monitor

Monitor:

- Skill invocations
- Authorization denials
- Successful and failed actions
- Ambient run health
- Data-quality exception trends
- Tool and resource errors
- Approval failures
- Audit-record completeness
- Security changes
- Unusual volume or population access

## 8. Change

Changes that require lifecycle review include:

- New Skill
- New Tool
- New worker fields
- Execution-mode change
- Security-group change
- Worker-population expansion
- New recipient
- API or resource change
- Data-quality rule change
- New automated write action

Update the version and repeat the applicable reviews and testing.

## 9. Deactivate

Deactivate when:

- Business purpose ends
- Security risk is unacceptable
- Required resources are unavailable
- Monitoring indicates unsafe behavior
- Ownership is missing
- A replacement solution is activated

Disable execution before removing evidence or configuration.

## 10. Archive

Retain according to approved policy:

- Final Agent Definition
- Approval evidence
- Security design
- Test results
- Activation and deactivation records
- Incident history
- Audit and monitoring summaries
- Lessons learned

Never archive credentials, secrets, or unnecessary worker data in the repository.
