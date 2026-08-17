# Ambient Execution Flow

```mermaid
sequenceDiagram
&#x20;   autonumber
&#x20;   participant Trigger as Approved Schedule or Event
&#x20;   participant Agent as Worker Profile Agent
&#x20;   participant ASU as Illustrative Ambient ASU
&#x20;   participant Security as Ambient Security Group
&#x20;   participant Source as Read-Only Worker Source
&#x20;   participant Rules as Data-Quality Rules
&#x20;   participant Report as Exception Report
&#x20;   participant Audit
&#x20;   Trigger->>Agent: Start approved monitoring run
&#x20;   Agent->>ASU: Establish Ambient execution identity
&#x20;   alt Ambient identity disabled
&#x20;       ASU-->>Agent: Disabled
&#x20;       Agent->>Audit: Record stopped run
&#x20;   else Ambient identity enabled
&#x20;       ASU->>Security: Evaluate approved scope
&#x20;       alt Scope invalid or excessive
&#x20;           Security-->>Agent: Denied
&#x20;           Agent->>Audit: Record security failure
&#x20;       else Scope approved
&#x20;           Security-->>Agent: Approved population and fields
&#x20;           Agent->>Rules: Load approved rule version
&#x20;           alt Rule version unavailable
&#x20;               Rules-->>Agent: Missing or invalid
&#x20;               Agent->>Audit: Record configuration failure
&#x20;           else Rule version available
&#x20;               Rules-->>Agent: Ready
&#x20;               Agent->>Source: Read changed records from previous watermark
&#x20;               Source-->>Agent: Authorized synthetic records
&#x20;               alt Record threshold exceeded
&#x20;                   Agent->>Audit: Stop without advancing watermark
&#x20;               else Threshold acceptable
&#x20;                   Agent->>Rules: Evaluate records
&#x20;                   Rules-->>Agent: Minimized exceptions
&#x20;                   Agent->>Report: Publish to authorized recipients
&#x20;                   alt Publication fails
&#x20;                       Report-->>Agent: Failure
&#x20;                       Agent->>Audit: Record unsuccessful run
&#x20;                   else Publication succeeds
&#x20;                       Report-->>Agent: Published
&#x20;                       Agent->>Audit: Record metrics and success
&#x20;                       Agent->>Agent: Advance watermark
&#x20;                   end
&#x20;               end
&#x20;           end
&#x20;       end
&#x20;   end
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
