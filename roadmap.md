# RALF Roadmap

This roadmap is intentionally conservative. The framework should stabilize before building too much implementation on top of unstable concepts.

## Phase 0 — Foundation

Status: in progress

Goals:

- define the RALF purpose and boundaries
- document the core concepts
- identify existing standards to reuse
- create early examples
- publish initial repository structure

Deliverables:

- README
- foundations document
- core concepts document
- architecture document
- first example project

## Phase 1 — Core model draft

Goals:

- define the first RALF meta-model
- create draft JSON/YAML schemas
- define the domain pack structure
- define the context packet structure
- create validation rules

Deliverables:

- `ralf-project.schema.json`
- `ralf-domain-pack.schema.json`
- `ralf-context-packet.schema.json`
- schema examples
- model validation notes

## Phase 2 — Developer tooling

Goals:

- create a basic CLI
- validate RALF project files
- render lifecycle diagrams
- inspect roles, artifacts, and gates
- compile example context packets

Possible commands:

```bash
ralf validate project.yaml
ralf inspect project.yaml
ralf graph project.yaml
ralf compile-context task.yaml
```

## Phase 3 — Domain packs

Goals:

- publish basic public domain packs
- define domain pack quality checklist
- create reusable templates
- support versioned imports

Starter packs:

- software development basic
- predictive maintenance basic
- quality management basic
- project delivery basic

## Phase 4 — Runtime adapter contract

Goals:

- define runtime adapter interface
- map context packets to external execution systems
- support human workflow and AI workflow targets
- preserve traceability across adapters

## Phase 5 — Governance and evidence

Goals:

- formalize governance profiles
- define risk and autonomy levels
- define trace and provenance model
- test gate logic with examples

## Phase 6 — Ecosystem

Goals:

- create compatibility rules
- define contribution process for packs
- define certification path
- publish documentation site
- prepare RALF Studio integration path
