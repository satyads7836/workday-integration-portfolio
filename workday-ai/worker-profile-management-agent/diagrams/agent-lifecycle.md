# Agent Lifecycle Diagram

```mermaid
stateDiagram-v2
    [\*] --> Idea
    Idea --> Define: Business purpose accepted
    Define --> Review: Design artifacts complete
    Review --> Define: Changes required
    Review --> Test: Reviews accepted
    Test --> Define: Defect or control gap
    Test --> Approve: Exit criteria satisfied
    Approve --> Test: Evidence rejected
    Approve --> Activate: Required approvals recorded
    Activate --> Monitor: Smoke test successful
    Activate --> Deactivate: Activation failure
    Monitor --> Define: Controlled change
    Monitor --> Deactivate: Retirement or unacceptable risk
    Deactivate --> Archive: Execution disabled
    Archive --> [\*]
```

## Lifecycle Evidence

| State | Required evidence |
|---|---|
| Idea | Business problem, sponsor, and initial risk |
| Define | Agent Definition, Skills, Tools, security, privacy, and architecture |
| Review | Business, security, privacy, architecture, and operational review |
| Test | Functional, negative, security, audit, and recovery evidence |
| Approve | Recorded owner and reviewer approvals |
| Activate | Approved version, activation record, and smoke-test result |
| Monitor | Metrics, incidents, access reviews, and change history |
| Deactivate | Disablement decision and execution evidence |
| Archive | Final design, approvals, tests, incidents, and lessons learned |

## Version Rule

A material change to a Skill, Tool, execution mode, worker-data scope, identity, recipient, or security policy returns the agent to the Define state.
