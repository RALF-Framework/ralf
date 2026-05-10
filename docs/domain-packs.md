# RALF Domain Packs

A **domain pack** is a reusable package of domain structure.

It helps teams avoid starting from a blank page when modeling a lifecycle, set of roles, skills, artifacts, gates, and knowledge assets.

## Purpose

Domain packs help RALF scale across different fields without forcing every organization to use the same vocabulary.

Examples:

- software development basic
- predictive maintenance basic
- manufacturing planning basic
- quality management basic
- customer support basic
- compliance workflow basic

## What a domain pack contains

A domain pack may include:

```text
manifest.yaml
lifecycles/
roles/
skills/
artifacts/
gates/
knowledge/
tools/
governance/
examples/
```

## Minimal manifest

```yaml
ralf_pack_version: "0.1"
pack:
  id: software-development-basic
  name: Software Development Basic
  description: A starter pack for modeling software delivery work.
  version: "0.1.0"
  status: draft
  maintainers:
    - RALF Framework
  domains:
    - software-development
  foundations:
    - BPMN-style lifecycle modeling
    - DMN-style decision and gate modeling
    - W3C PROV-inspired traceability
    - NIST AI RMF-inspired AI risk management
```

## Design rules

### 1. Use domain language first

Domain packs should use language that practitioners recognize.

For example, a maintenance domain pack should use terms like:

- asset
- fault
- inspection
- work order
- technician
- planner
- spare part
- downtime

It should not force AI-centric terms into the practitioner experience.

### 2. Keep the pack customizable

A domain pack is a starting point, not a law.

Organizations should be able to rename roles, add phases, remove gates, and change artifact templates.

### 3. Separate generic and premium knowledge

Public basic packs should teach the framework and provide useful examples.

Specialized expert packs may be commercial or private.

### 4. Include examples

Every domain pack should include at least one complete example context packet.

### 5. Version carefully

Domain packs should be versioned because lifecycle models, artifacts, gates, and role definitions may change over time.

## Suggested starter packs

### Software Development Basic

Purpose: model a simple software delivery lifecycle.

Typical phases:

```text
Discovery → Design → Build → Review → Release → Improve
```

Typical roles:

```text
Product Owner, Solution Architect, Developer, Reviewer, Operator
```

Typical artifacts:

```text
Problem Brief, Solution Design, Implementation, Test Report, Review Record, Release Notes
```

### Predictive Maintenance Basic

Purpose: model maintenance work supported by data and human approval.

Typical phases:

```text
Monitor → Detect → Diagnose → Plan → Execute → Validate → Learn
```

Typical roles:

```text
Asset Owner, Maintenance Planner, Technician, Reliability Engineer, Operations Manager
```

Typical artifacts:

```text
Signal Summary, Anomaly Report, Diagnosis Note, Work Order, Completion Record
```

### Quality Management Basic

Purpose: model quality issue handling and improvement.

Typical phases:

```text
Detect → Contain → Analyze → Correct → Verify → Prevent
```

Typical roles:

```text
Quality Manager, Process Owner, Operator, Reviewer, Compliance Lead
```

## Domain pack quality checklist

A domain pack is not ready unless it answers:

- What lifecycle does it model?
- What roles are required?
- What artifacts are produced?
- What gates control quality or risk?
- What knowledge assets are authoritative?
- What tools may be used?
- Which tasks are safe for AI assistance?
- Which actions require human approval?
- What evidence must be recorded?
