# Tool and Resource Mapping

## Important Notice

The Tool names and resource mappings in this document are illustrative. They are not official Workday API names, endpoints, or deployable configurations.

An authorized implementation team must validate the available Workday REST, SOAP, Report-as-a-Service, business-process, Orchestrate, Extend, or other supported resources for its tenant and release.

## Mapping Overview

| Tool | Skill | Mode | Operation | Illustrative resource requirement |
|---|---|---|---|---|
| Internal Authorization Check | Retrieve Worker Profile | Delegate | Evaluate | Agent interaction and user authorization context |
| Get Worker Profile | Retrieve Worker Profile | Delegate | Read | Permitted worker-profile retrieval resource |
| Internal Authorization Check | Update Worker Business Title | Delegate | Evaluate | Agent interaction and user authorization context |
| Validate Business Title | Update Worker Business Title | Delegate | Validate | Current worker data and configured validation rules |
| Request Business Title Change | Update Worker Business Title | Delegate | Submit | Applicable worker-change business process |
| Read Worker Profile Scope | Monitor Worker Profile Data Quality | Ambient | Read | Approved read-only worker-profile source |
| Evaluate Profile Data Quality | Monitor Worker Profile Data Quality | Ambient | Evaluate | Versioned data-quality rule engine |
| Publish Exception Report | Monitor Worker Profile Data Quality | Ambient | Publish | Restricted report or notification destination |
| Write Audit Record | All Skills | Both | Record | Append-only audit and monitoring destination |

## Delegate Mapping

### Retrieve Worker Profile

```text
User request
&#x20; -> Agent Interaction Policy
&#x20; -> Internal Authorization Check
&#x20; -> Permitted Worker Profile Resource
&#x20; -> Field Minimization
&#x20; -> Response
&#x20; -> Audit Record
```

Required validation:

- The user can invoke the Skill.
- The user can access the target worker.
- The user can access each returned field category.
- The requested purpose is approved.
- The response contains only necessary fields.

### Update Worker Business Title

```text
User request
&#x20; -> Agent Interaction Policy
&#x20; -> Internal Authorization Check
&#x20; -> Current-Value Validation
&#x20; -> Business-Title Validation
&#x20; -> User Confirmation
&#x20; -> Applicable Business Process
&#x20; -> Approval Routing
&#x20; -> Audit Record
```

Required validation:

- The user can invoke the Skill.
- The user can view the target worker.
- The user can initiate the applicable change.
- Domain and business-process permissions are satisfied.
- The target worker is in the authorized population.
- The configured approval process is preserved.
- The request does not update unrelated worker information.

## Ambient Mapping

### Monitor Worker Profile Data Quality

```text
Approved schedule or event
&#x20; -> Ambient Agent System User
&#x20; -> Ambient Agent Security Group
&#x20; -> Read-Only Worker Profile Source
&#x20; -> Data-Quality Rules
&#x20; -> Minimized Exception Report
&#x20; -> Authorized Recipients
&#x20; -> Audit and Run Metrics
```

Required validation:

- The Ambient Skill is activated through the approved lifecycle.
- The Ambient identity has only the required read permissions.
- Worker population and field scope are explicitly limited.
- No worker-update resource is assigned.
- Report recipients are authorized.
- Failed runs do not advance the processing watermark.

## Data Mapping

| Portfolio field | Purpose | Classification | Included in audit |
|---|---|---|---:|
| Synthetic worker ID | Correlate sample records | Synthetic identifier | Yes |
| Display name | Demonstrate profile retrieval | Synthetic personal data | No |
| Business title | Retrieve, validate, and update | Synthetic worker data | Previous and proposed values |
| Supervisory organization | Data-quality validation | Synthetic organization data | Category only |
| Location | Data-quality validation | Synthetic organization data | Category only |
| Worker type | Data-quality validation | Synthetic worker data | Category only |
| Worker status | Eligibility and consistency checks | Synthetic worker data | Category only |
| Correlation ID | End-to-end traceability | Operational metadata | Yes |

## Authentication and Secrets

This repository does not contain an authentication implementation.

A real design must use an approved authentication mechanism and secure secret storage. Never store OAuth secrets, tokens, passwords, certificates, or private keys in GitHub.

## Versioning

Each real implementation should record:

- Agent Definition version
- Skill version
- Tool mapping version
- API or service version
- Data-quality rule version
- Security-review date
- Test-evidence version
- Deployment or activation reference
