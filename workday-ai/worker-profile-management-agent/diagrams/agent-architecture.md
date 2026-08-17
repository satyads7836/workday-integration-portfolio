# Worker Profile Management Agent Architecture

```mermaid
flowchart TB
&#x20;   subgraph Triggers
&#x20;       U\[Authorized Worker or HR User]
&#x20;       E\[Approved Schedule or Event]
&#x20;   end
&#x20;   subgraph Agent_Governance\["Agent Governance"]
&#x20;       A\[Worker Profile Management Agent]
&#x20;       AD\[Illustrative Agent Definition]
&#x20;       LC\[Lifecycle and Approvals]
&#x20;   end
&#x20;   subgraph Skills
&#x20;       S1\[Retrieve Worker Profile]
&#x20;       S2\[Update Worker Business Title]
&#x20;       S3\[Monitor Profile Data Quality]
&#x20;   end
&#x20;   subgraph Security
&#x20;       DS\[Delegate Security Context]
&#x20;       ASU\[Illustrative Ambient ASU]
&#x20;       AASG\[Illustrative Ambient Agent Security Group]
&#x20;   end
&#x20;   subgraph Tools_and_Resources\["Tools and Validated Resources"]
&#x20;       T1\[Authorization and Worker Read]
&#x20;       T2\[Validation and Change Request]
&#x20;       T3\[Read-Only Quality Evaluation]
&#x20;   end
&#x20;   subgraph Outcomes
&#x20;       O1\[Minimized Worker Response]
&#x20;       O2\[Controlled Change Request]
&#x20;       O3\[Restricted Exception Report]
&#x20;       AU\[Audit and Monitoring]
&#x20;   end
&#x20;   U --> A
&#x20;   E --> A
&#x20;   A --> AD
&#x20;   LC --> AD
&#x20;   AD --> S1
&#x20;   AD --> S2
&#x20;   AD --> S3
&#x20;   S1 --> DS
&#x20;   S2 --> DS
&#x20;   S3 --> ASU
&#x20;   ASU --> AASG
&#x20;   DS --> T1
&#x20;   DS --> T2
&#x20;   AASG --> T3
&#x20;   T1 --> O1
&#x20;   T2 --> O2
&#x20;   T3 --> O3
&#x20;   O1 --> AU
&#x20;   O2 --> AU
&#x20;   O3 --> AU
```

## Design Boundaries

- Delegate Skills cannot expand the requesting user’s access.
- The title update preserves validation, confirmation, and approval routing.
- Ambient monitoring is read only.
- All resources and payloads are illustrative until validated.
- All portfolio worker records are synthetic.
