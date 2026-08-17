# Delegate Execution Flow

```mermaid
sequenceDiagram
&#x20;   autonumber
&#x20;   actor User
&#x20;   participant Agent as Worker Profile Agent
&#x20;   participant Policy as Interaction Policy
&#x20;   participant Security as User and Worker Security
&#x20;   participant Validation
&#x20;   participant Tool
&#x20;   participant Resource as Validated Workday Resource
&#x20;   participant Audit
&#x20;   User->>Agent: Request Delegate Skill
&#x20;   Agent->>Policy: Check Skill availability
&#x20;   alt Skill not available
&#x20;       Policy-->>Agent: Denied
&#x20;       Agent->>Audit: Record denial
&#x20;       Agent-->>User: Access denied
&#x20;   else Skill available
&#x20;       Policy-->>Agent: Allowed
&#x20;       Agent->>Security: Evaluate user, worker, and field or action scope
&#x20;       alt Underlying permission denied
&#x20;           Security-->>Agent: Denied
&#x20;           Agent->>Audit: Record authorization failure
&#x20;           Agent-->>User: Request not authorized
&#x20;       else Underlying permission allowed
&#x20;           Security-->>Agent: Allowed
&#x20;           Agent->>Validation: Validate inputs and business purpose
&#x20;           alt Validation fails
&#x20;               Validation-->>Agent: Validation errors
&#x20;               Agent->>Audit: Record validation failure
&#x20;               Agent-->>User: Correct the request
&#x20;           else Validation succeeds
&#x20;               Validation-->>Agent: Valid
&#x20;               alt Read-only retrieval
&#x20;                   Agent->>Tool: Retrieve permitted fields
&#x20;                   Tool->>Resource: Read authorized worker data
&#x20;                   Resource-->>Tool: Permitted result
&#x20;                   Tool-->>Agent: Minimized profile
&#x20;                   Agent->>Audit: Record retrieval metadata
&#x20;                   Agent-->>User: Return minimized response
&#x20;               else Controlled title-change request
&#x20;                   Agent-->>User: Present confirmation summary
&#x20;                   User->>Agent: Confirm request
&#x20;                   Agent->>Tool: Submit approved request
&#x20;                   Tool->>Resource: Initiate configured business process
&#x20;                   Resource-->>Tool: Request reference and status
&#x20;                   Tool-->>Agent: Submission result
&#x20;                   Agent->>Audit: Record confirmation and submission
&#x20;                   Agent-->>User: Return request status
&#x20;               end
&#x20;           end
&#x20;       end
&#x20;   end
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
