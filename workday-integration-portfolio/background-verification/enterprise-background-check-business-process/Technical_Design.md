# Technical Design

---

# Document Overview

This document describes the technical implementation of the Enterprise Background Check Business Process Automation solution in Workday.

The design focuses on configuration, integration orchestration, security, routing logic, notifications, and operational considerations.

---

# Solution Overview

The solution automates candidate background verification using Workday Recruiting Business Processes integrated with the Core Connector Background Check Order Outbound integration.

The implementation minimizes manual intervention while maintaining security, auditability, and recruiter visibility throughout the hiring lifecycle.

---

# Workday Modules

* Recruiting
* Staffing
* Security
* Business Process Framework
* Integration Framework

---

# Integration Type

* Core Connector
* Outbound Integration
* XML Message
* Business Process Integration

---

# Integration Pattern

Recruiter

?

Background Check Business Process

?

Core Connector Background Check Order

?

Document Delivery Service

?

Background Verification Vendor

?

Document Retrieval Service

?

Recruiter Review

---

# Business Process Configuration

Configured business process includes:

* Background Check Initiation
* Routing Rules
* Notifications
* Integration Step
* Decision Step
* Review Step
* Completion Step

---

# Integration Components

The implementation uses:

* Core Connector Background Check Order
* XML Message Generation
* Integration Event
* Document Delivery Service
* Document Retrieval Service

---

# Security Configuration

Configured security includes:

* Integration System User (ISU)
* Integration System Security Group (ISSG)
* Domain Security Policies
* Business Process Security Policies
* Role Based Security

---

# Roles

Typical roles include:

* Recruiter
* HR Partner
* HR Administrator
* Integration Administrator
* Security Administrator

---

# Notifications

Configured notifications include:

* Background Check Submitted
* Background Check Completed
* Background Check Failed
* Candidate Cleared
* Candidate Hold
* Recruiter Reminder

---

# Routing Logic

Routing decisions are based on:

* Candidate Stage
* Business Process Status
* Recruiter Assignment
* Hiring Organization
* Security Access

---

# XML Payload

Outbound XML typically contains:

* Candidate Identifier
* Worker Information
* Personal Information
* Position Details
* Job Requisition
* Organization
* Contact Details

---

# Validation Rules

Validation includes:

* Required fields
* Duplicate request prevention
* Candidate status validation
* Security validation
* Business process status validation

---

# Error Handling

Possible failures include:

* Missing worker information
* Missing requisition
* Security access denied
* XML validation failure
* Vendor endpoint unavailable
* Integration timeout

---

# Retry Strategy

Recommended retry approach:

* Retry transient failures
* Log integration events
* Notify administrator
* Escalate repeated failures
* Preserve audit history

---

# Performance Considerations

Recommendations:

* Schedule integrations during low usage periods.
* Monitor integration events.
* Archive completed transactions.
* Review integration logs regularly.
* Optimize XML payload size.

---

# Audit & Compliance

The solution supports:

* Complete audit trail
* Business Process history
* Integration event history
* Security audit
* Notification tracking

---

# Deployment Checklist

? Business Process configured

? Integration configured

? Security assigned

? Notifications configured

? Routing validated

? Integration tested

? Production deployment completed

---

# Assumptions

* Vendor endpoint is available.
* Security roles are assigned.
* Required domains are configured.
* Business Process is active.
* Recruiting module is enabled.

---

# Related Documents

* README.md
* Architecture.md
* Business_Flow.md
* Deployment_Guide.md
* Troubleshooting.md

