# Architecture

---

# Overview

The Verified First E Verify Integration establishes secure communication between Workday Recruiting and the Verified First background screening platform using Workday Web Services, OAuth 2.0 authentication, Background Check Connector, Document Delivery Services, and Webhooks.

The architecture enables automated background check ordering, secure data transmission, real-time status synchronization, and recruiter notifications while maintaining enterprise security standards.

---

# High Level Architecture

```mermaid
flowchart LR

A[Recruiter]

B[Workday Recruiting]

C[Background Check Business Process]

D[Core Connector Background Check]

E[Document Delivery Service]

F[Verified First]

G[OAuth 2.0]

H[Recruiting Web Services]

I[Webhook Callback]

J[Background Check Status]

K[Recruiter Notification]

A --> B

B --> C

C --> D

D --> E

E --> F

F --> G

G --> H

F --> I

I --> J

J --> B

B --> K
```

---

# Authentication Flow

```mermaid
sequenceDiagram

participant WD as Workday

participant OAuth as OAuth Server

participant VF as Verified First

WD->>OAuth: Client ID + Client Secret + Refresh Token

OAuth-->>WD: Access Token

WD->>VF: Background Check Request

VF-->>WD: Background Status Updates

VF->>WD: Webhook Callback

WD-->>Recruiter: Notification
```

---

# Major Components

## Workday Recruiting

Responsible for initiating candidate background verification and maintaining recruiting workflow.

---

## Background Check Business Process

Controls routing, approvals, notifications, integration execution, and candidate lifecycle.

---

## Integration System User (ISU)

Dedicated service account used by external integrations.

---

## Integration System Security Group (ISSG)

Provides secure access to Workday domains and APIs required by the integration.

---

## OAuth 2.0 API Client

Responsible for secure authentication between Workday and Verified First.

Configured using:

- Client ID
- Client Secret
- Refresh Token
- Access Token
- Token Endpoint
- Authorization Endpoint

---

## Recruiting Web Services

Provides SOAP-based Workday APIs used by Verified First.

---

## Background Check Connector

Generates XML payloads for candidate background verification requests.

---

## Document Delivery Service

Transfers outbound XML payloads securely to Verified First.

---

## Verified First Platform

Processes candidate verification requests and performs:

- Identity Verification
- Employment Verification
- Criminal Screening
- Background Investigation
- E Verify Processing

---

## Webhooks

Used for real-time callback events from Verified First to Workday.

Webhook events include:

- Pending
- Completed
- No Longer Applies

---

# Security Architecture

Security includes:

- Integration System User
- Integration System Security Group
- OAuth 2.0
- Domain Security Policies
- API Authentication
- Role-Based Access Control

---

# Data Flow

1. Recruiter initiates Background Check.

2. Workday Business Process starts.

3. Background Check Connector generates XML.

4. OAuth Access Token generated.

5. XML transmitted securely.

6. Verified First processes request.

7. Webhook callback received.

8. Candidate status updated.

9. Recruiter notified.

---

# Design Principles

- Secure authentication
- Minimal manual effort
- Enterprise scalability
- Standard Workday configuration
- Real-time synchronization
- Vendor interoperability

---

# Business Benefits

- Automated background verification
- Secure API authentication
- Faster hiring process
- Reduced manual effort
- Improved compliance
- Real-time status visibility
- Better recruiter experience

---

# Related Documents

- README.md
- Business_Flow.md
- Technical_Design.md
- Deployment_Guide.md
- Troubleshooting.md

