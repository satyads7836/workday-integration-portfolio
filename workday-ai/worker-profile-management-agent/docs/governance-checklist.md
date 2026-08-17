# Governance Checklist

Use this checklist before approving any version of the Worker Profile Management Agent.

## Business Purpose

- \[ ] The business problem is clearly documented.
- \[ ] Each Skill has a named business owner.
- \[ ] Expected outcomes are measurable.
- \[ ] The agent does not duplicate an existing controlled process without justification.
- \[ ] Out-of-scope activities are documented.

## Agent Definition

- \[ ] Agent name, purpose, provider, version, and status are complete.
- \[ ] All Skills are listed.
- \[ ] Every Skill has one approved execution mode.
- \[ ] Capabilities are validated against authorized documentation.
- \[ ] The definition is marked illustrative until a real schema is confirmed.
- \[ ] Version history is maintained.

## Skill Design

- \[ ] Each Skill performs one narrowly scoped business function.
- \[ ] Inputs, outputs, validations, and errors are defined.
- \[ ] Risk level is assigned.
- \[ ] Example requests use synthetic data.
- \[ ] Acceptance criteria are testable.
- \[ ] High-risk actions require confirmation.
- \[ ] Automated correction is excluded from the Ambient Skill.

## Tool and Resource Mapping

- \[ ] Every Tool maps to a business need.
- \[ ] Tool names are identified as conceptual where appropriate.
- \[ ] Real Workday resources are validated before implementation.
- \[ ] Read and write behavior is clearly distinguished.
- \[ ] Resource versions and dependencies are recorded.
- \[ ] Failure and retry behavior is defined.
- \[ ] Unused Tools and permissions are removed.

## Delegate Security

- \[ ] Agent Interaction Policy is approved.
- \[ ] Intended user populations are defined.
- \[ ] Target-worker populations are restricted.
- \[ ] Underlying Tool permissions are validated.
- \[ ] Domain security is validated.
- \[ ] Business-process security is validated for update requests.
- \[ ] Approval routing is preserved.
- \[ ] Negative authorization testing is complete.

## Ambient Security

- \[ ] Ambient Skill scope is approved.
- \[ ] Ambient identity design is documented.
- \[ ] Ambient Agent Security Group is least privilege.
- \[ ] Worker access is read only.
- \[ ] Worker population and fields are limited.
- \[ ] No worker-update permissions are assigned.
- \[ ] Schedule or event is approved.
- \[ ] Report recipients are authorized.
- \[ ] Emergency disablement is tested.

## Privacy and Data Protection

- \[ ] Only necessary worker fields are used.
- \[ ] All repository data is synthetic.
- \[ ] No tenant identifiers are present.
- \[ ] No credentials, secrets, tokens, or private keys are present.
- \[ ] Logs and audit records are minimized.
- \[ ] Retention and deletion requirements are documented.
- \[ ] Screenshots have passed two-person sanitization review.
- \[ ] Privacy approval is recorded.

## Testing

- \[ ] Positive scenarios pass.
- \[ ] Invalid-input scenarios pass.
- \[ ] Authorization-denial scenarios pass.
- \[ ] Restricted-field tests pass.
- \[ ] Confirmation and cancellation are tested.
- \[ ] Approval routing is tested.
- \[ ] Ambient threshold and watermark behavior are tested.
- \[ ] Failure, retry, and recovery are tested.
- \[ ] Audit completeness is tested.
- \[ ] Sensitive-data exposure testing passes.
- \[ ] JSON and Markdown files validate.

## Monitoring and Support

- \[ ] Support owner is named.
- \[ ] Operational metrics are defined.
- \[ ] Security-denial metrics are defined.
- \[ ] Failure thresholds and alerts are configured.
- \[ ] Runbook and escalation path exist.
- \[ ] Rollback or disablement procedure is documented.
- \[ ] Incidents can be correlated end to end.
- \[ ] Periodic access review is scheduled.

## Activation Approval

- \[ ] Business owner approves.
- \[ ] Security reviewer approves.
- \[ ] Privacy reviewer approves.
- \[ ] Architecture reviewer approves.
- \[ ] Operations owner accepts support responsibility.
- \[ ] Test evidence is attached.
- \[ ] Approved version is recorded.
- \[ ] Activation and rollback windows are agreed.

## Portfolio Publication

- \[ ] README accurately describes implemented artifacts.
- \[ ] No unsupported production claims are made.
- \[ ] No customer or employer information is exposed.
- \[ ] Disclaimers are visible.
- \[ ] Mermaid diagrams render on GitHub.
- \[ ] All relative links work.
- \[ ] Empty or placeholder files are removed.
- \[ ] Final repository review is complete.
