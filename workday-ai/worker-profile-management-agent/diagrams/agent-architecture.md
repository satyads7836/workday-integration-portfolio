# Worker Profile Management Agent Architecture

```mermaid
flowchart TB
    subgraph Triggers
        U[Authorized Worker or HR User]
        E[Approved Schedule or Event]
    end
    subgraph Agent_Governance["Agent Governance"]
        A[Worker Profile Management Agent]
        AD[Illustrative Agent Definition]
        LC[Lifecycle and Approvals]
    end
    subgraph Skills
        S1[Retrieve Worker Profile]
        S2[Update Worker Business Title]
        S3[Monitor Profile Data Quality]
    end
    subgraph Security
        DS[Delegate Security Context]
        ASU[Illustrative Ambient ASU]
        AASG[Illustrative Ambient Agent Security Group]
    end
    subgraph Tools_and_Resources["Tools and Validated Resources"]
        T1[Authorization and Worker Read]
        T2[Validation and Change Request]
        T3[Read-Only Quality Evaluation]
    end
    subgraph Outcomes
        O1[Minimized Worker Response]
        O2[Controlled Change Request]
        O3[Restricted Exception Report]
        AU[Audit and Monitoring]
    end
    U --> A
    E --> A
    A --> AD
    LC --> AD
    AD --> S1
    AD --> S2
    AD --> S3
    S1 --> DS
    S2 --> DS
    S3 --> ASU
    ASU --> AASG
    DS --> T1
    DS --> T2
    AASG --> T3
    T1 --> O1
    T2 --> O2
    T3 --> O3
    O1 --> AU
    O2 --> AU
    O3 --> AU
```

## Design Boundaries

- Delegate Skills cannot expand the requesting user’s access.
- The title update preserves validation, confirmation, and approval routing.
- Ambient monitoring is read only.
- All resources and payloads are illustrative until validated.
- All portfolio worker records are synthetic.
