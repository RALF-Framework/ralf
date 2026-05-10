# RALF Context Packets

A **context packet** is a bounded bundle of task-specific information.

It is compiled from the RALF model for a specific task, actor, lifecycle phase, and governance boundary.

## Why context packets exist

AI systems, software automations, and even human workers often fail when context is either missing or too broad.

RALF avoids two extremes:

1. **Too little context** — the actor cannot perform the task reliably.
2. **Too much context** — the actor receives irrelevant knowledge, excessive permissions, or unsafe authority.

The context packet provides the minimum useful context for a bounded task.

## Core principle

> Context is compiled, not dumped.

A context packet should be constructed from the model according to task needs, role permissions, lifecycle phase, artifact requirements, and governance rules.

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
  inputs:
    artifacts:
      - problem-brief
  knowledge_refs:
    - architecture-guideline
    - secure-design-checklist
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

## Required sections

### 1. Task contract

Defines what must be done.

Should include:

- task id
- objective
- expected result
- out-of-scope actions
- failure condition

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

### 4. Knowledge references

Lists only the knowledge needed for this task.

Should include:

- policies
- standards
- examples
- manuals
- prior decisions
- domain-specific references

### 5. Tool permissions

Defines what systems or operations are allowed.

Should include:

- allowed tools
- allowed operations
- forbidden operations
- required authentication level
- audit requirements

### 6. Output contract

Defines what must be produced.

Should include:

- artifact type
- required fields
- validation rules
- format
- destination

### 7. Gate requirements

Defines review or approval requirements.

Should include:

- automated checks
- human approver role
- pass criteria
- reject criteria
- evidence requirements

### 8. Trace requirements

Defines what must be recorded.

Should include:

- task start
- context source
- input use
- tool calls
- output creation
- gate submission
- approval decision

## Context packet lifecycle

```mermaid
flowchart LR
    A[Select Task] --> B[Resolve Lifecycle Phase]
    B --> C[Resolve Role]
    C --> D[Select Knowledge]
    D --> E[Restrict Tools]
    E --> F[Define Output Contract]
    F --> G[Attach Gates]
    G --> H[Create Context Packet]
    H --> I[Execute Task]
    I --> J[Record Trace]
```

## Safety rules

A context packet should never silently grant:

- production write access
- deployment permission
- customer communication authority
- financial approval authority
- compliance sign-off authority
- safety-critical decision authority

Those actions require explicit gates and human accountability.
