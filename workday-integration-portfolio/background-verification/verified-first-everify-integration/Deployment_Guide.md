# Deployment Guide

---

# Overview

This document provides the deployment procedure for the Verified First E Verify Integration with Workday Recruiting.

The deployment ensures that authentication, security, integration components, and business process configurations are migrated and validated in a controlled manner before production deployment.

---

# Deployment Prerequisites

Verify the following before deployment:

- Workday tenant is available.
- Verified First tenant is provisioned.
- Integration System User (ISU) is created.
- Integration System Security Group (ISSG) is configured.
- Domain Security Policies are assigned.
- Recruiting Business Process is configured.
- OAuth API Client is registered.
- Client ID and Client Secret are available.
- Refresh Token has been generated.
- Recruiting WSDL endpoint is verified.
- Background Check Connector is configured.
- Document Delivery Service is configured.
- Webhook endpoint is available.

---

# Deployment Components

Deploy the following components:

- Integration System User
- Integration System Security Group
- Domain Security Policies
- OAuth API Client
- Refresh Token
- Recruiting Web Services
- Background Check Connector
- Document Delivery Service
- Webhook Configuration
- Recruiting Business Process

---

# Deployment Sequence

## Step 1

Create Integration System User.

Verify service account configuration.

---

## Step 2

Configure Integration System Security Group.

Assign required security domains.

---

## Step 3

Activate Domain Security Policies.

Validate access to:

- Recruiting
- Worker Data
- Background Check
- Job Requisitions
- Integration Events

---

## Step 4

Register OAuth API Client.

Configure:

- Client Name
- Client ID
- Client Secret
- Authorized Scopes

---

## Step 5

Generate Refresh Token.

Validate token generation.

Store credentials securely.

---

## Step 6

Validate Recruiting WSDL.

Confirm API accessibility.

Verify endpoint connectivity.

---

## Step 7

Configure Background Check Connector.

Validate:

- XML generation
- Candidate mapping
- Background package configuration

---

## Step 8

Configure Document Delivery Service.

Validate secure outbound communication.

---

## Step 9

Register Webhooks.

Configure callback events for:

- Pending
- Completed
- No Longer Applies

---

## Step 10

Configure Business Process.

Validate:

- Routing
- Notifications
- Integration Step
- Completion Rules

---

# Validation Checklist

Verify:

? OAuth authentication successful

? Access Token generated

? Recruiting WSDL accessible

? Background Check Connector active

? XML payload generated

? Document Delivery successful

? Webhook received

? Candidate status updated

? Recruiter notifications delivered

? Security validation successful

---

# Smoke Test

Execute the following validation:

1. Create candidate.

2. Submit candidate.

3. Launch Background Check.

4. Authenticate using OAuth.

5. Generate XML payload.

6. Send request to Verified First.

7. Receive webhook callback.

8. Update candidate status.

9. Verify recruiter notification.

10. Complete hiring workflow.

---

# Rollback Plan

If deployment fails:

- Disable Business Process.
- Disable API Client.
- Revoke Refresh Token.
- Restore previous security configuration.
- Disable Webhook configuration.
- Restore previous connector configuration.
- Notify stakeholders.
- Schedule redeployment.

---

# Post Deployment Activities

Monitor:

- OAuth authentication
- API response times
- Webhook callbacks
- Integration Events
- Background Check status updates
- Business Process history
- Security events
- Recruiter notifications

---

# Production Monitoring

Review daily:

- Authentication failures
- Token generation failures
- Webhook failures
- XML validation errors
- Background Check failures
- Security authorization errors
- API response latency
- Integration runtime

---

# Success Criteria

Deployment is considered successful when:

- OAuth authentication succeeds.
- API communication is established.
- Background Check requests are generated.
- Verified First receives candidate information.
- Webhook callbacks update Workday.
- Candidate status is synchronized.
- Recruiters receive notifications.
- End-to-end process completes successfully.

---

# Related Documents

- README.md
- Architecture.md
- Business_Flow.md
- Technical_Design.md
- Troubleshooting.md
- Lessons_Learned.md
- Interview_Questions.md

