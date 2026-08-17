# Agent Definition Explained

## Important Notice

The accompanying `agent-definition.json` is an illustrative portfolio model. It is not an official Workday schema and must not be imported into a tenant without validating it against authorized Workday documentation.

## Purpose

The Agent Definition provides a structured description of the Worker Profile Management Agent, including:

- Business purpose
- Provider and platform context
- Supported Skills
- Execution modes
- Tools used by each Skill
- Security controls
- Data-protection requirements
- Governance ownership
- Activation criteria

## Core Fields

| Field | Purpose |
|---|---|
| `id` | Provides a stable project identifier for the agent |
| `displayName` | Gives the agent a human-readable name |
| `description` | Explains the agent’s business purpose |
| `version` | Tracks changes to the illustrative definition |
| `lifecycleStatus` | Shows the current governance stage |
| `provider` | Identifies the agent as a self-built portfolio example |
| `platformContext` | Records the Workday context and synthetic-data restriction |
| `capabilities` | Describes supported behavioral features |
| `skills` | Defines the three business functions modeled by the agent |
| `dataProtection` | Separates allowed synthetic data from prohibited information |
| `governance` | Defines ownership, reviews, and activation conditions |

## Skill 1: Retrieve Worker Profile

Execution mode: Delegate<br>

Risk level: Medium

This Skill retrieves only the worker information that the requesting user is authorized to view.

The design requires:

1. Agent interaction access
2. An internal authorization check
3. Underlying worker-data permissions
4. Field-level data minimization
5. An audit record

Access to the Skill does not automatically provide access to the underlying worker information.

## Skill 2: Update Worker Business Title

Execution mode: Delegate<br>

Risk level: High

This Skill submits a controlled request to change a worker’s business title.

The design requires:

1. Agent interaction access
2. Domain and business-process security
3. Input validation
4. Approval routing
5. Duplicate-request prevention
6. Audit logging

The Skill does not directly bypass an approval process. A real implementation must use the applicable configured Workday business process and security model.

## Skill 3: Monitor Worker Profile Data Quality

Execution mode: Ambient<br>

Risk level: Medium

This Skill evaluates worker-profile completeness from an approved schedule or event.

The design uses an illustrative:

- Ambient Agent System User
- Ambient Agent Security Group
- Read-only worker-data scope
- Data-quality rules
- Exception report
- Audit record

The Skill identifies exceptions but does not automatically modify worker records.

## Capabilities

The illustrative definition includes:

| Capability | Value | Design purpose |
|---|---:|---|
| State transition history | `true` | Preserve lifecycle and status changes |
| Streaming | `false` | No streaming behavior is required |
| Push notifications | `true` | Support exception or workflow notifications |
| Audit trail | `true` | Record requests, decisions, results, and errors |

Capability names and availability must be validated before any real implementation.

## Data Protection

Only synthetic worker records and sanitized configuration examples are allowed in this project.

The following information is prohibited:

- Real worker data
- Tenant identifiers
- Credentials
- OAuth tokens
- Client secrets
- Private keys
- Confidential implementation exports

## Governance Roles

| Role | Responsibility |
|---|---|
| HR Technology Product Owner | Owns the business purpose and approved scope |
| Workday Integration Lead | Owns the technical design and Tool mapping |
| Workday Security Administrator | Reviews least privilege and security policies |
| Privacy Reviewer | Reviews worker-data usage and minimization |
| Architecture Reviewer | Reviews integration and lifecycle design |

## Activation Criteria

The design cannot move from review to activation until:

- Skill scope is approved
- Tool security is validated
- Test evidence is approved
- Monitoring is enabled
- Audit requirements are satisfied
- A rollback plan is approved

## Portfolio Interpretation

This file demonstrates how agent metadata, Skills, Tools, security, execution modes, data protection, and governance can be represented together.

It is a technical design artifact, not proof that the agent has been deployed in a Workday tenant.
