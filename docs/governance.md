# RALF Governance

RALF governance defines how work remains accountable, traceable, and controlled when humans, software systems, and AI agents collaborate.

Governance in RALF is not only a checklist and not only a prompt instruction. It is a dynamic layer that connects policies, risks, controls, roles, gates, evidence, and runtime constraints.

RALF can help structure governance, but it does not automatically make an organization compliant with any law, regulation, or standard. Compliance depends on correct implementation, human review, organizational process, legal interpretation, and evidence quality.

---

## Governance principles

1. **Humans remain accountable.** AI agents may assist, draft, inspect, summarize, or recommend, but organizational accountability remains human-owned.
2. **Governance is dynamic.** Policies, risks, controls, and evidence requirements should be versioned and reviewed over time.
3. **High-risk actions require gates.** Approval, validation, or evidence checks must exist before sensitive actions.
4. **Knowledge must have owners.** Policies, standards, and domain knowledge should have responsible maintainers.
5. **Tools follow least privilege.** Actors receive only the permissions required for the task.
6. **Artifacts are evidence.** Outputs and decisions should be stored as artifacts with provenance.
7. **Every important action is traceable.** Tool calls, decisions, approvals, and artifacts should be recorded.
8. **Automation must be reversible or reviewable where possible.** Risky actions should have rollback, review, or escalation paths.
9. **Governance should be testable.** A RALF model should expose which controls, gates, evidence requirements, and decision rights apply to a task.

---

## Governance objects

### Governance profile

A governance profile defines the governance boundary for a project, domain pack, lifecycle, phase, task type, context packet, or runtime adapter.

A governance profile may reference internal policy, quality standards, security controls, risk frameworks, or regulation-related obligations.

```yaml
governance_profile:
  id: software-delivery-basic-governance
  version: "0.1.0"
  owner_role: governance-owner
  scope:
    applies_to:
      - software-delivery
      - release-management
  risk_model:
    default_level: medium
    levels:
      - low
      - medium
      - high
      - critical
  required_controls:
    - human-review-for-release
    - trace-tool-actions
    - preserve-review-evidence
  review_cycle:
    frequency: quarterly
    owner_role: governance-owner
```

### Policy

A policy is a rule, constraint, or requirement that affects work execution.

```yaml
policy:
  id: no-production-release-without-approval
  name: No production release without approval
  enforcement_level: blocking
  owner_role: release-manager
  applies_to:
    - release
  description: Production releases require approval by the release manager.
```

### Control

A control is a concrete governance requirement mapped to RALF objects.

Controls should be specific enough to test.

```yaml
control:
  id: human-review-for-release
  type: approval-control
  applies_to:
    lifecycle_phase: release
    artifact: release-notes
  required_gate: release-approval
  required_evidence:
    - review-record
    - approval-record
```

### Gate

A gate is a control point.

```yaml
gate:
  id: production-release-approval
  risk_level: high
  approver_role: release-manager
  automated_checks:
    - tests_passed
    - security_scan_completed
    - rollback_plan_exists
  pass_criteria:
    - reviewer_approved
    - release_notes_complete
    - trace_record_created
```

### Evidence requirement

An evidence requirement defines what must be produced or preserved to support trust, audit, review, or improvement.

```yaml
evidence_requirement:
  id: release-approval-record
  artifact_type: approval-record
  required_for:
    - production-release-approval
  must_capture:
    - approver
    - decision
    - reason
    - timestamp
    - linked_artifacts
```

### Runtime enforcement rule

A runtime enforcement rule describes how governance should affect execution.

In early RALF versions, this may be advisory or manually checked. Later, adapters may enforce it directly.

```yaml
runtime_enforcement:
  id: restrict-release-tools
  applies_to:
    phase: release
    role: ai-assistant
  tool_rules:
    allowed:
      - docs.read
      - repo.read
    denied:
      - deployment.trigger
      - secrets.read
  decision:
    deployment.trigger: manual_review_required
```

---

## Risk levels

Suggested early risk levels:

| Level | Description | Typical control |
|---|---|---|
| Low | Drafting, summarization, internal suggestions | Trace only |
| Medium | Artifact generation or workflow updates | Human review |
| High | Production-impacting, compliance, financial, safety, or customer-facing actions | Explicit approval gate |
| Critical | Safety-critical or legally binding actions | Human authority only unless formally validated |

Risk level should not be inferred only from the actor. A human, software service, or AI agent can all perform low-risk or high-risk work depending on context.

---

## Autonomy levels

Suggested early autonomy levels:

| Level | Name | Meaning |
|---|---|---|
| 0 | Observe | Can read and summarize only |
| 1 | Draft | Can create draft artifacts |
| 2 | Recommend | Can propose actions for approval |
| 3 | Execute with approval | Can execute after a gate passes |
| 4 | Execute within policy | Can execute bounded low-risk actions under policy |
| 5 | Autonomous critical action | Not recommended for early RALF use |

Early RALF examples should avoid level 5. High-impact decisions should pass through explicit gates.

---

## Gate design checklist

Every gate should define:

- purpose
- risk level
- triggering condition
- required evidence
- automated checks
- human approver role
- pass criteria
- reject criteria
- escalation path
- trace requirements
- validity period, if approval can expire

---

## Governance and context packets

The governance profile should affect context packet compilation.

For example, a high-risk task should produce a context packet with:

- narrower tool permissions
- stricter output contract
- mandatory gate
- mandatory trace events
- explicit human approver
- restricted autonomy level
- required evidence
- policy references
- runtime enforcement expectations

A context packet should not silently grant approval authority, production access, customer communication authority, financial approval authority, compliance sign-off authority, or safety-critical decision authority.

---

## Runtime governance

During runtime, governance should sit between the actor and the action.

```text
Task context → proposed action → governance check → allow / deny / require approval → trace
```

A RALF-compatible runtime adapter should be able to evaluate:

- Who or what is acting?
- Which role is active?
- Which lifecycle phase is active?
- Which governance profile applies?
- What tool or artifact is being accessed?
- What action is proposed?
- What risk level applies?
- Is approval required?
- What evidence must be recorded?

Runtime governance may start as a manual pattern in early versions and later become middleware, filters, policy-as-code, or adapter-level enforcement.

---

## Evidence model

Evidence should connect:

```text
Task → Context Packet → Input Artifacts → Actions → Output Artifacts → Gate Decision → Trace
```

This chain allows teams to inspect what happened, why it happened, who or what performed it, what evidence was used, and who approved it.

---

## Human control examples

### Software release

AI may draft release notes, summarize changes, and check test evidence.

A human release manager approves the release.

### Predictive maintenance

AI may detect anomalies and recommend inspection.

A maintenance planner approves the work order.

### Compliance workflow

AI may gather evidence and draft a control response.

A compliance officer approves the final submission.

---

## Compliance note

RALF governance may help organizations represent controls related to standards, internal policies, or regulation-related requirements.

However:

- a governance profile is not a legal opinion
- a passing gate is not proof of legal compliance
- a schema-valid model is not proof of operational compliance
- runtime logs are useful evidence, but not sufficient by themselves
- human review and domain/legal expertise remain necessary

RALF should therefore use careful language:

> RALF helps structure governance controls and evidence.

It should avoid overclaiming:

> RALF makes your system compliant.
