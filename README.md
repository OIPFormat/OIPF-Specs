<p align="center">
  <img src="assets/logo.svg" alt="OIPF — Operational Intelligence Packaging Format" width="460">
</p>

# OIPF — Operational Intelligence Packaging Format

**Operations-as-Code for industrial and operational systems.**

OIPF is an open framework for packaging *operational-intelligence use cases* —
predictive maintenance, energy-loss detection, quality-drift detection, cleaning/fouling
optimisation, downtime root-cause analysis, and the like — as **versioned, testable,
auditable artifacts** that deploy across many sites by configuration rather than
reconstruction.

It sits **above** existing operational standards (OPC UA, ISA-95, ISA-88, MQTT/Sparkplug,
historians, MES/CMMS/ERP) and replaces none of them. It is a domain-general sibling of
**UAPF** (algorithm packaging) and **MCPF** (agent trust): where UAPF makes an *algorithm*
executable and auditable, OIPF makes a *governed operational decision* portable.

> **Status: v0.3.0 — draft.** Comprehensive specification + reference example. Expect breaking changes.

📄 **Start with [`CONCEPT.md`](CONCEPT.md)** for the first-principles rationale, then the
[`spec/`](spec) for the architecture and components.

🖥️ **Interactive demo:** [`demo/`](demo) — technical *As-is vs With-OIPF* architecture + the executive decision loop, animated.

---

## Why OIPF exists

A trained model is portable — you can copy the file. What is *not* portable is everything
a model needs to act responsibly inside a live operational system: the **meaning** of each
signal, the **bounds** it must respect, the **governance** of who approves an action, and
the **truth** of whether it helped. Today these are rebuilt by hand on every deployment, so
the capability never compounds and each site becomes a bespoke project.

OIPF makes that judgment-in-context portable. It is possible because, across domains, the
**structure of an operational decision is invariant** — only the physics, tags and models
differ. Full derivation in [`CONCEPT.md`](CONCEPT.md); the detailed problem statement
(seven recurring barriers) is in [`spec/00-overview.md`](spec/00-overview.md).

## Architecture

```
  Industrial / operational data sources
  SCADA · DCS · PLC · historian · MES · CMMS · ERP · lab · documents
        ↓  Connector layer            OPC UA · MQTT/Sparkplug · SQL · APIs · import
        ↓  Data foundation            time-series store · lakehouse · event store · doc index
  ┌─────────────────────────────────────────────────────────────────────────┐
  │  OIPF runtime   plant graph · semantics · packages · model contracts ·   │  ← this repo
  │                 workflows · validation · audit · outcome feedback        │
  └─────────────────────────────────────────────────────────────────────────┘
        ↓  Intelligence layer         ML · physics · rules · LLM agents · optimisation
        ↓  Human-in-the-loop ops      recommendations · approvals · work orders · actions
        ↓  Outcome feedback           result · savings · model improvement · audit trail
```

The framework defines **ten components** across these tiers — canonical semantics, plant
graph, connector abstraction, package format, model contract, agentic workflow,
validation & simulation, audit & governance, outcome feedback, and runtime. See
[`spec/01-architecture.md`](spec/01-architecture.md) and
[`spec/02-components.md`](spec/02-components.md).

## Anatomy of a package

A package is a versioned directory with a manifest and declarative objects
([`examples/heat-exchanger-fouling`](examples/heat-exchanger-fouling)):

| Object | File | Purpose |
|---|---|---|
| Manifest | `oipf.yaml` | identity, version, conformance, maturity, object index |
| Asset graph | `asset-graph.yaml` | Site → Area → System → Unit → Asset + flows (ISA-95-aligned) |
| Tag map | `tag-map.yaml` | site tags → canonical variables + units (UNS-aligned) |
| States & events | `states-events.yaml` | operating modes + events (ISA-88-aligned) |
| Constraints | `constraints.yaml` | safety, quality, environmental, operational limits |
| Model contract | `model-contract.yaml` | declarative I/O for the physics/ML model |
| Workflow | `workflow.yaml` | recommend → explain → approve → act → record → feedback |
| Savings | `savings.yaml` | impact / savings attribution |
| Validation | `validation-tests.yaml` | pre-deploy checks |
| Outcome ledger | *(runtime)* | signed record of decisions & measured results |

## Deployment maturity levels

| Level | Name | Behaviour |
|---|---|---|
| L0 | Monitor | context + KPIs only |
| L1 | Advisory | recommends; a human acts |
| L2 | Supervised | recommends **and prepares** the action; human approves |
| L3 | Closed-loop (bounded) | acts within declared constraints; human on exceptions |
| L4 | Autonomous (bounded) | self-optimises within an envelope; human oversight |

## Conformance levels

**Core** (manifest + asset-graph + tag-map + model-contract + workflow) · **Plus** (+ validation + outcome + savings) · **Signed** (+ DID/VC-signed provenance via VeriDocs).

## Use-case catalogue

Reference briefs for the recurring package types live in [`use-cases/`](use-cases):
cleaning/fouling optimisation, energy-loss detection, predictive maintenance,
quality-drift detection, downtime root-cause analysis.

## Relationship to the ecosystem

**UAPF** — OIPF's workflow/approval/audit layer is a UAPF profile for operational technology · **MCPF** — agent-to-tool trust for agentic execution · **ProcessGit** — version-control substrate for packages · **VeriDocs / DID-VC** — signs the outcome & audit ledger.

## Repository layout

```
OIPF-Specs/
├── README.md · CONCEPT.md · LICENSE · CONTRIBUTING.md · CHANGELOG.md
├── spec/        00 overview · 01 architecture · 02 components ·
│                03 package-format · 04 lifecycle-and-conformance ·
│                05 governance · 06 roadmap-and-ecosystem
├── schemas/     JSON Schema (draft 2020-12)
├── use-cases/   reference package briefs
└── examples/    heat-exchanger-fouling (validated)
```

## Design principle

The format is **extracted, not invented**. Only the invariant decision loop is fixed up
front; every object/field beyond it earns its place by recurring across ≥2 independent
packages. Ecosystem and roadmap items (registries, marketplace) are explicitly **vision /
later phases**, never the lead — see [`spec/06-roadmap-and-ecosystem.md`](spec/06-roadmap-and-ecosystem.md).

## License

Apache-2.0 — see [LICENSE](LICENSE). Independent open specification, inspired by and
connected to UAPF; not affiliated with any single product or vendor.
