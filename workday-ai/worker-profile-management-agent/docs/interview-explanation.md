# Portfolio Interview Explanation

## One-Minute Summary

I designed a Worker Profile Management Agent portfolio blueprint to demonstrate how an enterprise AI agent can be governed in a Workday context.

The agent has three Skills:

1. Retrieve Worker Profile in Delegate mode
2. Update Worker Business Title in Delegate mode
3. Monitor Worker Profile Data Quality in Ambient mode

The design separates Skill access from the underlying Tool, domain, and business-process security. It also includes synthetic API examples, security matrices, audit records, Mermaid architecture diagrams, lifecycle controls, and a governance checklist.

The project is intentionally a design and governance demonstration. It does not claim to be an official Workday Agent Definition or a production deployment.

## Why This Scenario?

Worker-profile management demonstrates several important enterprise patterns in one project:

- Read versus write access
- User-initiated versus background execution
- Worker-population restrictions
- Field-level minimization
- Business-process approvals
- Ambient least privilege
- Auditability
- Data-quality monitoring

## Why Three Skills?

Each Skill represents a different control pattern.

### Retrieve Worker Profile

A read-only Delegate Skill demonstrating:

- User interaction access
- Underlying worker-data permission
- Target-worker restriction
- Field minimization

### Update Worker Business Title

A high-risk Delegate Skill demonstrating:

- Input validation
- User confirmation
- Domain and business-process security
- Approval routing
- Separation of duties
- Audit evidence

### Monitor Worker Profile Data Quality

A read-only Ambient Skill demonstrating:

- Scheduled or event-based execution
- Ambient agent identity
- Least-privilege worker access
- Versioned rules
- Exception reporting
- Operational monitoring

## Most Important Security Principle

```text
Skill access does not equal Tool or API access.
```

A user may be able to interact with a Skill but still lack permission to retrieve a worker or initiate a business process.

For Delegate execution, the design evaluates the requesting user’s access. For Ambient execution, the design limits the agent identity to the approved read-only scope.

## Key Design Decision

The Ambient Skill does not automatically correct worker records.

It produces a restricted exception report because automatic correction would introduce additional risk, validation, approval, and accountability requirements.

## How Is Data Protected?

- All repository data is synthetic.
- No live tenant connection exists.
- No credentials, secrets, tokens, or private keys are stored.
- Worker responses and reports are minimized.
- Audit records store metadata instead of complete worker profiles.
- Screenshots require sanitization and secondary review.

## How Would This Move Toward Production?

Before a real implementation:

1. Validate the official Agent Definition requirements.
2. Confirm the supported Workday Tools and resources.
3. Confirm authentication and identity behavior.
4. Map the required domain and business-process security.
5. Complete privacy and architecture reviews.
6. Build and test in an authorized non-production tenant.
7. Validate approvals, audit, monitoring, and rollback.
8. Obtain business, security, and operational approval.
9. Activate through controlled change management.

## Limitations

- The Agent Definition is illustrative.
- Tool names are conceptual.
- API payloads are synthetic.
- No Workday tenant execution is demonstrated.
- No production performance claim is made.
- Product behavior must be validated against authorized documentation.

## Interview Questions

### Why use Delegate mode for worker retrieval?

Because an identified user requests the information, and the result must respect that user’s permitted worker population and fields.

### Why is the title update high risk?

It changes a worker record and may require business-process security, approval routing, effective-date validation, and separation of duties.

### Why use Ambient mode for data quality?

The activity runs repeatedly from an approved schedule or event and does not require a user to initiate every execution.

### Can the Ambient Skill update worker records?

Not in this design. It is read only and produces exceptions for authorized review.

### What happens when audit logging fails?

High-risk execution should fail safely according to approved policy. The system must not silently perform an untraceable change.

### What is the project’s strongest feature?

It connects business Skills, Tools, execution modes, security, privacy, lifecycle, testing, audit, and operations in one coherent governance model.
