# Delegate Execution Flow

```mermaid
sequenceDiagram
    autonumber
    actor User
    participant Agent as Worker Profile Agent
    participant Policy as Interaction Policy
    participant Security as User and Worker Security
    participant Validation
    participant Tool
    participant Resource as Validated Workday Resource
    participant Audit
    User->>Agent: Request Delegate Skill
    Agent->>Policy: Check Skill availability
    alt Skill not available
        Policy-->>Agent: Denied
        Agent->>Audit: Record denial
        Agent-->>User: Access denied
    else Skill available
        Policy-->>Agent: Allowed
        Agent->>Security: Evaluate user, worker, and field or action scope
        alt Underlying permission denied
            Security-->>Agent: Denied
            Agent->>Audit: Record authorization failure
            Agent-->>User: Request not authorized
        else Underlying permission allowed
            Security-->>Agent: Allowed
            Agent->>Validation: Validate inputs and business purpose
            alt Validation fails
                Validation-->>Agent: Validation errors
                Agent->>Audit: Record validation failure
                Agent-->>User: Correct the request
            else Validation succeeds
                Validation-->>Agent: Valid
                alt Read-only retrieval
                    Agent->>Tool: Retrieve permitted fields
                    Tool->>Resource: Read authorized worker data
                    Resource-->>Tool: Permitted result
                    Tool-->>Agent: Minimized profile
                    Agent->>Audit: Record retrieval metadata
                    Agent-->>User: Return minimized response
                else Controlled title-change request
                    Agent-->>User: Present confirmation summary
                    User->>Agent: Confirm request
                    Agent->>Tool: Submit approved request
                    Tool->>Resource: Initiate configured business process
                    Resource-->>Tool: Request reference and status
                    Tool-->>Agent: Submission result
                    Agent->>Audit: Record confirmation and submission
                    Agent-->>User: Return request status
                end
            end
        end
    end
```

## Control Points

1. Skill availability
2. Target-worker authorization
3. Tool and resource permissions
4. Input and purpose validation
5. User confirmation for write requests
6. Configured approval routing
7. Minimized response
8. Audit record
