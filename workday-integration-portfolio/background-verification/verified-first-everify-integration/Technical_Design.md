# Technical Design

---

# Document Overview

This document describes the technical implementation of the Verified First E Verify Integration with Workday Recruiting.

The solution enables secure communication between Workday and the Verified First platform using Workday Web Services, OAuth 2.0 authentication, API Clients, Webhooks, and the Background Check Connector.

---

# Solution Overview

The implementation automates the end-to-end background verification process by securely exchanging candidate information between Workday Recruiting and Verified First.

The integration provides:

- Secure OAuth 2.0 authentication
- Automated background check ordering
- Real-time webhook callbacks
- Candidate status synchronization
- Background check status mapping
- Enterprise-grade security controls

---

# Workday Modules

- Recruiting
- Staffing
- Security
- Business Process Framework
- Integration Framework
- Public Web Services

---

# Integration Components

The implementation consists of:

- Integration System User (ISU)
- Integration System Security Group (ISSG)
- Domain Security Policies
- OAuth 2.0 API Client
- Client ID
- Client Secret
- Refresh Token
- Access Token
- Recruiting Web Service (WSDL)
- Background Check Connector
- Document Delivery Service
- Webhooks

---

# Authentication Design

Authentication uses OAuth 2.0.

Configuration includes:

- Client Registration
- Client ID
- Client Secret
- Refresh Token
- Token Endpoint
- Authorization Endpoint
- Access Token Generation

The Access Token is used for secure communication between Workday and Verified First.

---

# Security Configuration

The following security components are configured:

## Integration System User

Dedicated service account used by external integrations.

## Integration System Security Group

Provides secure access to Workday APIs.

## Domain Security Policies

Configured to allow:

- Recruiting
- Integration Events
- Background Check
- Job Requisitions
- Worker Data
- Personal Data

## API Security

OAuth authentication protects API communication.

---

# API Client Configuration

The API Client configuration includes:

- Client Name
- Client ID
- Client Secret
- Refresh Token
- Functional Areas
- Authorized Scopes

---

# Refresh Token Management

The integration uses non-expiring refresh tokens to minimize operational maintenance while maintaining secure access.

Refresh tokens are exchanged for short-lived access tokens before API communication.

---

# Recruiting Web Services

The Recruiting WSDL exposes the SOAP APIs required for candidate background verification.

The integration consumes Workday Recruiting web services for secure data exchange.

---

# Background Check Connector

The connector is responsible for:

- Building outbound XML payloads
- Sending candidate information
- Initiating background verification
- Supporting webhook callbacks

---

# Webhook Configuration

Webhook events are configured for:

- Background Check Created
- Pending
- Completed
- No Longer Applies

Webhook callbacks automatically synchronize candidate status with Workday.

---

# Document Delivery Service

The Document Delivery Service securely transmits XML payloads to the Verified First platform using configured authentication.

---

# Status Mapping

Supported statuses include:

- Pending
- Completed
- No Longer Applies

These statuses are mapped to the corresponding recruiting workflow.

---

# XML Payload

Typical payload includes:

- Candidate Information
- Worker Details
- Job Requisition
- Position
- Organization
- Contact Information
- Background Package
- Background Status

---

# Validation Rules

Validation includes:

- Candidate eligibility
- Required fields
- OAuth authentication
- Security permissions
- Duplicate request prevention
- Background status validation

---

# Error Handling

Possible failures include:

- OAuth authentication failure
- Invalid Client ID
- Invalid Client Secret
- Expired Access Token
- Missing Refresh Token
- WSDL connectivity issues
- Webhook delivery failure
- XML validation failure
- Security authorization failure

---

# Performance Considerations

Recommendations:

- Reuse refresh tokens securely
- Monitor API response times
- Monitor webhook delivery
- Archive completed events
- Review authentication logs
- Monitor integration runtime

---

# Deployment Checklist

? ISU Created

? ISSG Configured

? Domain Security Assigned

? Security Activated

? API Client Registered

? Refresh Token Generated

? WSDL Verified

? Background Check Connector Configured

? Document Delivery Configured

? Webhooks Configured

? Status Mapping Validated

? End-to-End Testing Completed

---

# Related Documents

- README.md
- Architecture.md
- Business_Flow.md
- Deployment_Guide.md
- Troubleshooting.md
- Lessons_Learned.md
- Interview_Questions.md

