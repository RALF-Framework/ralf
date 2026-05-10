# RALF Governance

RALF governance defines how work remains accountable, traceable, and controlled when humans, software systems, and AI agents collaborate.

## Governance principles

1. **Humans remain accountable.** AI agents may assist, draft, inspect, summarize, or recommend, but organizational accountability remains human-owned.
2. **High-risk actions require gates.** Approval, validation, or evidence checks must exist before sensitive actions.
3. **Knowledge must have owners.** Policies, standards, and domain knowledge should have responsible maintainers.
4. **Tools follow least privilege.** Actors receive only the permissions required for the task.
5. **Artifacts are evidence.** Outputs and decisions should be stored as artifacts with provenance.
6. **Every important action is traceable.** Tool calls, decisions, approvals, and artifacts should be recorded.
7. **Automation must be reversible or reviewable where possible.** Risky actions should have rollback, review, or escalation paths.

## Governance objects

### Governance profile

A governance profile defines the control level for a project, domain pack, lifecycle, or task type.

```yaml
governance_profile:
  id: standard-human-review
  risk_level: medium
  requires_human_approval: true
  trace_required: true
  allowed_autonomy: draft_and_recommend
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

### Risk level

Suggested early risk levels:

| Level | Description | Typical control |
|---|---|---|
| Low | Drafting, summarization, internal suggestions | Trace only |
| Medium | Artifact generation or workflow updates | Human review |
| High | Production-impacting, compliance, financial, safety, customer-facing actions | Explicit approval gate |
| Critical | Safety-critical or legally binding actions | Human authority only unless formally validated |

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

## Governance and context packets

The governance profile should affect context packet compilation.

For example, a high-risk task should produce a context packet with:

- narrower tool permissions
- stricter output contract
- mandatory gate
- mandatory trace events
- explicit human approver
- restricted autonomy level

## Evidence model

Evidence should connect:

```text
Task → Context Packet → Input Artifacts → Actions → Output Artifacts → Gate Decision → Trace
```

This chain allows teams to inspect what happened, why it happened, and who approved it.

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
