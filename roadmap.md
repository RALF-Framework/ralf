# RALF Roadmap

This roadmap is intentionally conservative. The framework should stabilize before building too much implementation on top of unstable concepts.

RALF is currently a proposed framework. The roadmap should therefore support validation, not only implementation.

---

## Phase 0 — Foundation

Status: in progress

Goals:

- define the RALF purpose and boundaries
- document the core concepts
- identify existing standards and patterns to reuse
- create early examples
- publish initial repository structure
- clarify what RALF does not claim yet

Deliverables:

- README
- foundations document
- core concepts document
- architecture document
- first example project
- research and validation status notes

---

## Phase 1 — Core model draft

Goals:

- define the first RALF meta-model
- create draft JSON/YAML schemas
- define the domain pack structure
- define the context packet structure
- define the governance profile structure
- create validation rules

Deliverables:

- `ralf-project.schema.json`
- `ralf-domain-pack.schema.json`
- `ralf-context-packet.schema.json`
- `ralf-governance-profile.schema.json`
- `ralf-policy.schema.json`
- schema examples
- model validation notes

---

## Phase 2 — Governance and evidence model

Goals:

- formalize governance profiles
- define policies, controls, evidence requirements, and approval rules
- define risk and autonomy levels
- define trace and provenance expectations
- test gate logic with examples
- clarify compliance-related language and limits

Deliverables:

- governance model documentation
- governance profile examples
- policy examples
- control examples
- evidence requirement examples
- gate examples
- compliance limitation note

---

## Phase 3 — Developer tooling

Goals:

- create a basic CLI
- validate RALF project files
- validate governance profiles
- render lifecycle diagrams
- inspect roles, artifacts, governance controls, and gates
- compile example context packets
- report missing evidence, missing roles, and missing gates

Possible commands:

```bash
ralf validate project.yaml
ralf validate-governance governance-profile.yaml
ralf inspect project.yaml
ralf graph project.yaml
ralf compile-context task.yaml
ralf audit-readiness project.yaml
```

---

## Phase 4 — Domain packs

Goals:

- publish basic public domain packs
- define domain pack quality checklist
- create reusable templates
- support versioned imports
- include governance profiles and evidence requirements in starter packs

Starter packs:

- software development basic
- predictive maintenance basic
- quality management basic
- project delivery basic

---

## Phase 5 — RALF Studio validation prototype

Goals:

- create a visual modeling environment for RALF
- allow users to model lifecycle, roles, artifacts, gates, governance, and context packets
- test whether non-AI experts can understand and use the framework
- collect validation evidence from real workflow modeling sessions
- identify which concepts are too complex, unclear, or unnecessary

Validation questions:

- Can users model a real lifecycle?
- Can users identify responsible and accountable roles?
- Can users define required artifacts and gates?
- Can users attach governance controls and evidence requirements?
- Can users understand a generated context packet?
- Does RALF improve clarity before automation is introduced?

Deliverables:

- Studio prototype
- validation workflow
- example modeled organizations or workflows
- usability notes
- framework revision backlog

---

## Phase 6 — Runtime adapter contract

Goals:

- define runtime adapter interface
- map context packets to external execution systems
- support human workflow and AI workflow targets
- preserve traceability across adapters
- define where runtime governance checks happen

Possible adapter targets:

- human work instructions
- workflow systems
- ticketing systems
- AI agent runtimes
- automation platforms
- policy engines

---

## Phase 7 — Runtime governance experiments

Goals:

- test policy checks around tool calls
- test human approval gates
- test trace recording
- test evidence generation
- test adapter-level governance enforcement

Important limitation:

RALF should not claim full regulatory compliance from these experiments. These experiments test whether governance structures can be represented and applied.

---

## Phase 8 — Ecosystem

Goals:

- create compatibility rules
- define contribution process for packs
- define certification or compatibility labels
- publish documentation site
- prepare RALF Studio integration path
- support community examples

---

## Maturity checkpoints

RALF should only increase its maturity claims when evidence exists.

| Claim | Required evidence |
|---|---|
| Conceptual framework | Published paper and specification draft |
| Machine-readable model | Schemas and validation examples |
| Practical modeling framework | Studio prototype and modeled real workflows |
| Developer-ready framework | CLI, schemas, examples, and documentation |
| Runtime-ready framework | Adapter contract and traceable execution examples |
| Governance-ready framework | Tested governance profiles, gates, evidence, and audit traces |
| Production-ready ecosystem | Stable versioning, compatibility rules, documentation, and user validation |

---

## Current priority

The current priority is:

```text
paper alignment → specification alignment → schema alignment → CLI validation → Studio validation
```

The framework should avoid overclaiming before real validation exists.
