# RALF Foundations

RALF should be grounded in existing standards, protocols, and proven modeling practices. The framework should avoid reinventing established concepts unless RALF needs a new binding layer between them.

## Design stance

RALF is a **standards-composing framework**.

It does not try to replace process modeling, decision modeling, governance, provenance, software delivery, manufacturing integration, or agent runtimes. Instead, it defines how these ideas can be connected into reusable domain packs and task-specific context packets.

## Foundation map

| RALF area | Existing foundation to reuse | RALF usage |
|---|---|---|
| Process and lifecycle modeling | BPMN | Lifecycle phases, process flows, events, responsibilities, and handoffs |
| Decision logic | DMN | Repeatable decision tables, gate logic, routing rules, and business decisions |
| Responsibility modeling | RACI and role-based process modeling | Accountability, consulted/informed relationships, and approval ownership |
| Provenance | W3C PROV | Evidence, traceability, activity records, artifact lineage, and trust assessment |
| AI risk management | NIST AI RMF | Risk framing, governance, trustworthiness, controls, and monitoring |
| Knowledge management | ISO 30401 and ISO 9001 organizational knowledge concepts | Knowledge assets, ownership, maintenance, and evidence of organizational learning |
| Secure software development | NIST SSDF and OWASP SAMM | Secure delivery gates, review requirements, evidence, and maturity practices |
| Software delivery measurement | DORA metrics | Delivery performance and improvement loops |
| Tool/API integration | OpenAPI, AsyncAPI, MCP-style tool/data contracts | Tool exposure, permissioning, interface documentation, and runtime integration |
| Artifact provenance and supply chain | SPDX, CycloneDX, W3C PROV | Evidence records, dependency metadata, and traceable outputs |
| Manufacturing integration | ISA-95, RAMI 4.0, OPC UA, Asset Administration Shells | Domain packs for industrial operations and Industry 4.0 environments |

## Why these foundations matter

### BPMN for lifecycle and process structure

BPMN is a formal notation for business process modeling. RALF should not invent a new process notation when BPMN already provides a widely recognized way to describe process flows. RALF can use a simplified lifecycle view for non-technical users while preserving compatibility with more formal process models.

Reference: <https://www.omg.org/spec/BPMN/>

### DMN for decisions and gates

DMN provides a standard way to describe business decisions and business rules. In RALF, gates should be more than vague approval points. They should be expressible as criteria, rules, evidence checks, human approvals, or decision tables.

Reference: <https://www.omg.org/dmn/>

### W3C PROV for evidence and traceability

RALF treats artifacts and traces as first-class entities. W3C PROV gives a useful conceptual base for tracking entities, activities, and agents involved in producing data or things.

Reference: <https://www.w3.org/TR/prov-overview/>

### NIST AI RMF for AI risk

RALF should support AI use without making AI action invisible or uncontrolled. NIST AI RMF provides a practical grounding for managing AI risks and promoting trustworthy AI development and use.

Reference: <https://www.nist.gov/itl/ai-risk-management-framework>

## RALF contribution

RALF's contribution is not a replacement for these foundations.

RALF contributes:

1. A shared meta-model that connects lifecycle, role, knowledge, tool, artifact, gate, and trace concepts.
2. A domain-pack structure for packaging reusable operational knowledge.
3. A context-packet structure for giving humans, systems, or agents bounded task context.
4. A governance view that keeps human accountability, evidence, and approval gates explicit.
5. A practical bridge between domain experts and technical implementation.

## Grounding rule for future documentation

Every major RALF concept should answer three questions:

1. **What existing standard or practice does this reuse?**
2. **What does RALF add that is not already covered?**
3. **What must remain human-owned or organization-owned?**
