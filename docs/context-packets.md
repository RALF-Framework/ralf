# RALF Context Packets

A **context packet** is a bounded bundle of task-specific information.

It is compiled from the RALF model for a specific task, actor, lifecycle phase, and governance boundary.

Context packets are one of the main bridges between the RALF framework and real execution by humans, software systems, or AI agents.

---

## Why context packets exist

AI systems, software automations, and even human workers often fail when context is either missing or too broad.

RALF avoids two extremes:

1. **Too little context** — the actor cannot perform the task reliably.
2. **Too much context** — the actor receives irrelevant knowledge, excessive permissions, or unsafe authority.

The context packet provides the minimum useful context for a bounded task.

---

## Core principle

> Context is compiled, not dumped.

A context packet should be constructed from the model according to task needs, role permissions, lifecycle phase, artifact requirements, governance rules, and evidence requirements.

---

## Minimal context packet structure

```yaml
context_packet:
  id: cp-001
  version: "0.1"
  task:
    id: draft-solution-design
    objective: Draft a solution design from an approved problem brief.

  lifecycle:
    id: software-delivery
    phase: design

  role_binding:
    role: solution-architect
    authority: draft_only
    accountable_role: product-owner

  inputs:
    artifacts:
      - problem-brief

  knowledge_refs:
    - architecture-guideline
    - secure-design-checklist

  governance:
    profile_id: software-delivery-basic-governance
    profile_version: "0.1.0"
    risk_level: medium
    policy_refs:
      - secure-design-review
      - human-approval-for-release
    required_controls:
      - design-review
      - trace-output-artifact
    evidence_required:
      - solution-design-draft
      - design-risk-notes
    runtime_enforcement:
      tool_calls: policy_checked
      artifact_writes: trace_required
      approval_required_for:
        - release-approval
        - production-deployment

  tools:
    allowed:
      - docs.read
      - repo.read
    forbidden:
      - repo.write
      - deployment.trigger

  outputs:
    required:
      - solution-design

  gates:
    required:
      - design-approval

  trace:
    required_events:
      - context_packet_created
      - input_artifact_read
      - output_artifact_created
      - gate_submitted
```

---

## Required sections

### 1. Task contract

Defines what must be done.

Should include:

- task id
- objective
- expected result
- out-of-scope actions
- failure condition
- success criteria

### 2. Lifecycle binding

Places the task in the lifecycle.

Should include:

- lifecycle id
- phase id
- previous phase
- next phase
- phase inputs
- phase outputs

### 3. Role binding

Defines authority and responsibility.

Should include:

- acting role
- accountability owner
- permissions
- approval limits
- escalation path

### 4. Governance binding

Defines which policies, risks, controls, evidence requirements, and runtime restrictions apply.

Should include:

- governance profile id
- governance profile version
- risk level
- policy references
- required controls
- evidence requirements
- prohibited actions
- restricted actions
- approval rules
- runtime enforcement expectations

Governance binding prevents the context packet from becoming only a prompt or instruction bundle. It makes the control boundary explicit.

### 5. Knowledge references

Lists only the knowledge needed for this task.

Should include:

- policies
- standards
- examples
- manuals
- prior decisions
- domain-specific references

### 6. Tool permissions

Defines what systems or operations are allowed.

Should include:

- allowed tools
- allowed operations
- forbidden operations
- required authentication level
- audit requirements
- approval requirements for sensitive operations

### 7. Output contract

Defines what must be produced.

Should include:

- artifact type
- required fields
- validation rules
- format
- destination
- evidence classification

### 8. Gate requirements

Defines review or approval requirements.

Should include:

- automated checks
- human approver role
- pass criteria
- reject criteria
- evidence requirements
- validity period
- escalation path

### 9. Trace requirements

Defines what must be recorded.

Should include:

- task start
- context source
- governance profile used
- input use
- tool calls
- output creation
- gate submission
- approval decision
- denied or escalated actions

---

## Context packet lifecycle

```mermaid
flowchart LR
    A[Select Task] --> B[Resolve Lifecycle Phase]
    B --> C[Resolve Role]
    C --> D[Resolve Governance Profile]
    D --> E[Classify Risk]
    E --> F[Select Knowledge]
    F --> G[Restrict Tools]
    G --> H[Define Output Contract]
    H --> I[Attach Gates and Evidence]
    I --> J[Create Context Packet]
    J --> K[Execute Task]
    K --> L[Record Trace]
```

---

## Runtime use

A context packet should guide execution but should not be the only control mechanism.

For AI-assisted or automated work, the runtime should evaluate proposed actions before execution:

```text
Context packet → proposed action → governance check → allow / deny / require approval → trace
```

Examples:

| Proposed action | Governance result |
|---|---|
| Read approved problem brief | Allow |
| Draft solution design | Allow |
| Write directly to production repository | Deny or require approval |
| Trigger deployment | Require explicit human gate |
| Send customer-facing message | Require approval unless policy allows it |

---

## Safety rules

A context packet should never silently grant:

- production write access
- deployment permission
- customer communication authority
- financial approval authority
- compliance sign-off authority
- safety-critical decision authority
- authority to approve its own output
- authority to bypass a required gate

Those actions require explicit governance rules, gates, and human accountability.

---

## Good context packet design

A good context packet is:

- **bounded** — only includes what is needed for the task
- **role-aware** — reflects the actor's responsibility and authority
- **governed** — includes policies, risks, controls, and required evidence
- **traceable** — records how it was created and used
- **portable** — can be interpreted by different tools or runtimes
- **reviewable** — can be inspected by a human before execution
- **expirable** — can include freshness or validity rules when stale context could cause harm
