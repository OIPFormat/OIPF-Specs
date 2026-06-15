# Changelog

## [0.1.0] — draft
- Initial specification: overview, package format, lifecycle & conformance.
- JSON Schemas: package manifest, asset-graph, model-contract, workflow, outcome.
- Deployment maturity levels L0–L4; conformance levels Core / Plus / Signed.
- Reference example: `heat-exchanger-fouling` (manufacturing — cleaning optimisation).
- Defined relationship to OPC UA, ISA-95, ISA-88, Sparkplug/UNS and to UAPF/MCPF/ProcessGit/VeriDocs.

## [0.2.0] — concept rewrite
- Added CONCEPT.md: first-principles, domain-neutral rationale (as-Code lineage; "the invariant is the decision, not the domain").
- Removed problem framing borrowed from external company/role descriptions; README now derives the problem generally.
- No schema or example changes.

## [0.3.0] — scope realignment
- Restored the full framework architecture as the spec body while keeping the v0.2 first-principles rationale (CONCEPT.md) as the "why".
- spec/ restructured: 00 overview (incl. 7-barrier problem statement), 01 architecture (7-tier + 10 components), 02 components (detailed), 03 package-format, 04 lifecycle & conformance, 05 governance (7 principles + open/proprietary), 06 roadmap & ecosystem (phased, labelled vision/later).
- Added use-cases/ catalogue: cleaning/fouling, energy-loss, predictive maintenance, quality-drift, downtime RCA.
- Connector Abstraction and Runtime Environment restored as first-class components.
- No breaking changes to schemas or the heat-exchanger example.
