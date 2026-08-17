# Execution Modes

## Overview

The project demonstrates both Delegate and Ambient execution.

| Mode | Trigger | Security context | Project Skills |
|---|---|---|---|
| Delegate | User request | User permissions combined with agent and Skill controls | Retrieve Worker Profile; Update Worker Business Title |
| Ambient | Approved schedule or event | Illustrative Ambient ASU and Ambient Agent Security Group | Monitor Worker Profile Data Quality |

## Delegate Mode

Delegate mode is appropriate when a user intentionally asks the agent to perform an action.

The project uses Delegate mode when:

- A worker or authorized HR user retrieves permitted profile information.
- An authorized user requests a business-title change.

### Delegate Decision Logic

```mermaid
flowchart TD
&#x20;   A\[User Request] --> B{Skill Available to User?}
&#x20;   B -- No --> X\[Deny and Audit]
&#x20;   B -- Yes --> C{Target Worker Authorized?}
&#x20;   C -- No --> X
&#x20;   C -- Yes --> D{Tool and Resource Permissions Valid?}
&#x20;   D -- No --> X
&#x20;   D -- Yes --> E{Input and Purpose Valid?}
&#x20;   E -- No --> Y\[Return Validation Error and Audit]
&#x20;   E -- Yes --> F{Write Request?}
&#x20;   F -- No --> G\[Return Minimized Read Result]
&#x20;   F -- Yes --> H\[Present Confirmation]
&#x20;   H --> I{User Confirms?}
&#x20;   I -- No --> Z\[Cancel and Audit]
&#x20;   I -- Yes --> J\[Submit Through Approval Process]
&#x20;   G --> K\[Write Audit Record]
&#x20;   J --> K
```

## Ambient Mode

Ambient mode is appropriate for an approved background activity that is not initiated by a user for every run.

The project uses Ambient mode to identify worker-profile data-quality exceptions.

### Ambient Decision Logic

```mermaid
flowchart TD
&#x20;   A\[Approved Schedule or Event] --> B{Skill Active?}
&#x20;   B -- No --> X\[Stop and Audit]
&#x20;   B -- Yes --> C{Ambient Identity Enabled?}
&#x20;   C -- No --> X
&#x20;   C -- Yes --> D{Security Scope Matches Approval?}
&#x20;   D -- No --> Y\[Stop and Alert Security]
&#x20;   D -- Yes --> E{Rule Version Available?}
&#x20;   E -- No --> Z\[Stop and Alert Support]
&#x20;   E -- Yes --> F\[Read Approved Population]
&#x20;   F --> G{Threshold Exceeded?}
&#x20;   G -- Yes --> W\[Stop Without Advancing Watermark]
&#x20;   G -- No --> H\[Evaluate Rules]
&#x20;   H --> I\[Publish Minimized Exceptions]
&#x20;   I --> J\[Record Metrics and Audit]
&#x20;   J --> K\[Advance Watermark After Success]
```

## Comparison

| Area | Delegate | Ambient |
|---|---|---|
| Immediate user involved | Yes | No |
| Trigger | User request | Schedule or event |
| Interaction policy | Required | Not the primary access mechanism |
| Underlying security | User and resource permissions | Ambient identity permissions |
| Confirmation | Required for high-risk write requests | Not applicable to the read-only monitoring run |
| Write permission in this project | Controlled request only | None |
| Primary audit subject | User request and agent action | Run, identity, scope, and exceptions |
| Emergency control | Disable Skill or access | Disable or pause Ambient execution |

## Selection Rationale

### Retrieve Worker Profile

Selected mode: Delegate

Reason: A user requests worker information for an immediate business purpose. The result must be evaluated against that user’s permissions.

### Update Worker Business Title

Selected mode: Delegate

Reason: A user intentionally initiates a high-risk worker-data change that requires confirmation and approval routing.

### Monitor Worker Profile Data Quality

Selected mode: Ambient

Reason: The activity runs repeatedly against an approved scope and produces a read-only exception report without changing worker records.

## Governance Requirement

A change in execution mode requires a new security, privacy, testing, monitoring, and business-owner review. Delegate and Ambient modes must not be treated as interchangeable.
