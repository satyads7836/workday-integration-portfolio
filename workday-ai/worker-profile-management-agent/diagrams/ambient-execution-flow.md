# Ambient Execution Flow

```mermaid
sequenceDiagram
    autonumber
    participant Trigger as Approved Schedule or Event
    participant Agent as Worker Profile Agent
    participant ASU as Illustrative Ambient ASU
    participant Security as Ambient Security Group
    participant Source as Read-Only Worker Source
    participant Rules as Data-Quality Rules
    participant Report as Exception Report
    participant Audit
    Trigger->>Agent: Start approved monitoring run
    Agent->>ASU: Establish Ambient execution identity
    alt Ambient identity disabled
        ASU-->>Agent: Disabled
        Agent->>Audit: Record stopped run
    else Ambient identity enabled
        ASU->>Security: Evaluate approved scope
        alt Scope invalid or excessive
            Security-->>Agent: Denied
            Agent->>Audit: Record security failure
        else Scope approved
            Security-->>Agent: Approved population and fields
            Agent->>Rules: Load approved rule version
            alt Rule version unavailable
                Rules-->>Agent: Missing or invalid
                Agent->>Audit: Record configuration failure
            else Rule version available
                Rules-->>Agent: Ready
                Agent->>Source: Read changed records from previous watermark
                Source-->>Agent: Authorized synthetic records
                alt Record threshold exceeded
                    Agent->>Audit: Stop without advancing watermark
                else Threshold acceptable
                    Agent->>Rules: Evaluate records
                    Rules-->>Agent: Minimized exceptions
                    Agent->>Report: Publish to authorized recipients
                    alt Publication fails
                        Report-->>Agent: Failure
                        Agent->>Audit: Record unsuccessful run
                    else Publication succeeds
                        Report-->>Agent: Published
                        Agent->>Audit: Record metrics and success
                        Agent->>Agent: Advance watermark
                    end
                end
            end
        end
    end
```

## Control Points

1. Approved trigger
2. Ambient identity state
3. Least-privilege security scope
4. Approved rule version
5. Restricted worker population
6. Maximum record threshold
7. Read-only evaluation
8. Authorized report recipients
9. Watermark advancement only after success
10. Complete audit and run metrics
