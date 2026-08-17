# Architecture

## Architecture Objective

The Worker Profile Management Agent is a portfolio blueprint for governed worker-data retrieval, controlled profile-change requests, and automated data-quality monitoring.

The design separates:

- User interaction
- Agent metadata
- Skills
- Tools
- Workday resources
- Security evaluation
- Business processes
- Reporting
- Audit and monitoring

## Logical Architecture

```mermaid
flowchart TD
    U[Authorized User] --> A[Worker Profile Management Agent]
    T[Approved Schedule or Event] --> A
    A --> AD[Illustrative Agent Definition]
    AD --> S1[Retrieve Worker Profile]
    AD --> S2[Update Worker Business Title]
    AD --> S3[Monitor Profile Data Quality]
    S1 --> C1[Delegate Security Context]
    S2 --> C1
    S3 --> C2[Ambient Security Context]
    C1 --> TL[Illustrative Tools]
    C2 --> TL
    TL --> WR[Validated Workday Resources]
    WR --> BP[Read, Business Process, or Reporting Action]
    BP --> AU[Audit and Monitoring]
```

## Components

| Component | Responsibility |
|---|---|
| User or trigger | Initiates Delegate execution or starts an Ambient run |
| Agent | Coordinates the approved business interaction |
| Agent Definition | Describes metadata, capabilities, Skills, Tools, and governance |
| Skill | Defines a narrowly scoped business function |
| Tool | Provides the conceptual mechanism used by a Skill |
| Security context | Evaluates Delegate user access or Ambient identity permissions |
| Workday resource | Provides the validated read, business-process, or reporting operation |
| Audit service | Records decisions, outcomes, errors, and correlation metadata |
| Monitoring | Tracks operational health and control effectiveness |

## Delegate Architecture

```mermaid
sequenceDiagram
    actor User
    participant Agent
    participant Policy as Interaction Policy
    participant Security
    participant Tool
    participant Resource as Workday Resource
    participant Audit
    User->>Agent: Request Skill
    Agent->>Policy: Check Skill availability
    Policy-->>Agent: Allow or deny
    Agent->>Security: Evaluate user and worker scope
    Security-->>Agent: Authorized or denied
    Agent->>Tool: Invoke approved operation
    Tool->>Resource: Read or submit controlled request
    Resource-->>Tool: Result
    Tool-->>Agent: Minimized result
    Agent->>Audit: Record decision and outcome
    Agent-->>User: Controlled response
```

## Ambient Architecture

```mermaid
sequenceDiagram
    participant Trigger as Schedule or Event
    participant Agent
    participant ASU as Ambient ASU
    participant Security as Ambient Security Group
    participant Rules as Data-Quality Rules
    participant Report
    participant Audit
    Trigger->>Agent: Start approved run
    Agent->>ASU: Establish Ambient identity
    ASU->>Security: Evaluate read-only scope
    Security-->>Agent: Authorized population
    Agent->>Rules: Evaluate permitted records
    Rules-->>Agent: Minimized exceptions
    Agent->>Report: Publish to authorized recipients
    Agent->>Audit: Record metrics and outcome
```

## Trust Boundaries

| Boundary | Required control |
|---|---|
| User to agent | Authentication and interaction policy |
| Agent to Tool | Approved Skill-to-Tool mapping |
| Tool to resource | Domain or business-process security |
| Ambient identity to worker data | Least privilege and restricted population |
| Agent to report recipient | Recipient authorization and data minimization |
| All components to audit | Integrity, retention, and sensitive-data exclusion |

## Data Flow

### Retrieval

```text
User request
\-> authorization
\-> permitted field retrieval
\-> field minimization
\-> response
\-> audit metadata
```

### Title Update

```text
User request
\-> authorization
\-> validation
\-> confirmation
\-> business-process submission
\-> approval routing
\-> status response
\-> audit metadata
```

### Data-Quality Monitoring

```text
Schedule or event
\-> Ambient authorization
\-> restricted worker read
\-> rule evaluation
\-> exception minimization
\-> restricted report
\-> run metrics and audit
```

## Architecture Constraints

- No live Workday connection is included.
- No official Workday endpoint or schema is asserted.
- All worker records are synthetic.
- No credentials or secrets are stored.
- Ambient execution is read only.
- High-risk changes preserve validation and approvals.
- Existing repository content remains unchanged.
