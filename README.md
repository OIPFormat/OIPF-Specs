# OIPF — Operational Intelligence Packaging Format

**Operations-as-Code for industrial plants.**

OIPF is an open packaging format for deploying operational-intelligence use cases —
fouling and cleaning optimisation, energy-loss reduction, predictive maintenance,
throughput and yield optimisation — across industrial sites as **versioned, testable,
auditable packages**. *Deploy once, configure per site, run anywhere.*

OIPF is a domain-general sibling of **UAPF** (algorithm packaging) and **MCPF** (agent
trust). Where UAPF packages an *algorithm* and makes it executable and auditable, OIPF
packages a deployable *operational-intelligence use case*: the plant context, the model
contract, the human-in-the-loop decision workflow, and the outcome/savings feedback
needed to run a model on a real plant and replicate it across sites.

> **Status: v0.1.0 — draft.** Initial specification + reference example. Expect breaking changes.

---

## The problem OIPF addresses

Process and utility plants lose 15–25% of operating value to avoidable inefficiency —
over-cleaning, undetected fouling, suboptimal operating conditions, siloed local
optimisation. This is **not a data-shortage problem**: plants already stream continuous
data from thousands of sensors. The value is trapped because:

- **integration is slow** — every historian, SCADA and tag convention is different;
- **contextualisation is poor** — raw tags carry no shared meaning;
- **models are bespoke** — each site rebuilds from scratch;
- **replication takes months** — nothing transfers plant-to-plant.

Industrial AI deployments therefore tend to collapse into bespoke consulting. OIPF exists
to make a deployment **a portable artifact instead of a project**.

## What OIPF is — and is not

OIPF is the missing layer **above** existing industrial standards, not a replacement.

**OIPF defines:** how a plant-intelligence use case is packaged, configured, deployed,
validated, audited, and its savings attributed — repeatably across sites.

**OIPF does NOT replace** (it references):
- control logic (PLC / DCS / loops),
- connectivity standards (OPC UA, MQTT/Sparkplug),
- enterprise/control hierarchy (ISA-95 / IEC 62264),
- recipes and procedures (ISA-88),
- historians, lakehouses, or the physics/ML models themselves.

## The layer model

```
  Connectivity   OPC UA  ·  MQTT / Sparkplug  ·  APIs
  Data           historian  /  lakehouse  /  time-series store
  ┌───────────────────────────────────────────────────────────┐
  │  OIPF       context + model contract + decision workflow   │   ← this repo
  │             + outcome ledger  (the portable layer)         │
  └───────────────────────────────────────────────────────────┘
  Models         physics + ML  (project-specific, proprietary)
  Interface      operator / engineer UX
```

## Anatomy of an OIPF package

A package is a versioned directory (or archive) with a manifest and a set of declarative
objects. See [`examples/heat-exchanger-fouling`](examples/heat-exchanger-fouling).

| Object | File | Purpose |
|---|---|---|
| Manifest | `oipf.yaml` | identity, version, conformance level, object index |
| Asset graph | `asset-graph.yaml` | Site → Area → System → Unit → Asset + flows (ISA-95-aligned) |
| Tag map | `tag-map.yaml` | messy site tags → canonical variables + units (UNS-aligned) |
| States & events | `states-events.yaml` | operating modes + events (ISA-88-aligned) |
| Constraints | `constraints.yaml` | safety, quality, environmental, operational limits |
| Model contract | `model-contract.yaml` | declarative I/O for the physics/ML model |
| Workflow | `workflow.yaml` | recommend → explain → approve → act → record → feedback |
| Savings | `savings.yaml` | impact / savings attribution formula |
| Validation | `validation-tests.yaml` | pre-deploy checks (CI for a deployment) |
| Outcome ledger | *(runtime)* | signed record of decisions & measured results |

The **workflow** object is OIPF's UAPF DNA: a process-as-code, human-in-the-loop,
auditable decision flow — UAPF profiled for operational technology.

## Deployment maturity levels

Like autonomy levels for a car, a package declares how much control it is trusted with.

| Level | Name | Behaviour |
|---|---|---|
| **L0** | Monitor | surfaces context + KPIs only |
| **L1** | Advisory | recommends; a human decides and acts |
| **L2** | Supervised | recommends **and prepares** the action (work order / setpoint); human approves |
| **L3** | Closed-loop (bounded) | acts within declared constraints; human on exceptions |
| **L4** | Autonomous (bounded) | self-optimises within an envelope; human oversight |

Most packages ship at **L1** and earn higher levels per site, gated by `constraints.yaml`.

## Conformance levels

- **Core** — manifest + asset-graph + tag-map + model-contract + workflow + audit. Minimum to be a valid OIPF package.
- **Plus** — Core + validation suite + outcome ledger + savings.
- **Signed** — Plus + cryptographically signed provenance (DID/VC via VeriDocs).

## Relationship to the wider ecosystem

- **UAPF** — OIPF's workflow/approval/audit layer is a UAPF profile for operational technology.
- **MCPF** — agent-to-tool trust when agentic execution is involved.
- **ProcessGit** — the version-control substrate for packages (branch/merge/what-if).
- **VeriDocs / DID-VC** — signs the outcome & audit ledger (the *Signed* conformance level).

## Repository layout

```
oipf/
├── README.md
├── LICENSE                 Apache-2.0
├── CONTRIBUTING.md
├── CHANGELOG.md
├── spec/
│   ├── 00-overview.md
│   ├── 01-package-format.md
│   └── 02-lifecycle-and-conformance.md
├── schemas/                JSON Schema (draft 2020-12)
│   ├── oipf.package.schema.json
│   ├── asset-graph.schema.json
│   ├── model-contract.schema.json
│   ├── workflow.schema.json
│   └── outcome.schema.json
└── examples/
    └── heat-exchanger-fouling/    worked manufacturing example
```

## Design principle (read before extending)

Do **not** grow this into a 200-page standard up front. The format is *extracted* from
real packages, not invented ahead of them. The rule: ship 1–2 concrete packages in a
domain, find what genuinely repeats, then promote only the stable parts into the spec.
Open at the manifest/interface level; keep models and runtime proprietary.

## License

Apache-2.0 — see [LICENSE](LICENSE). Spec text may move to CC-BY-4.0 in a future release.
OIPF is an independent open specification, inspired by and connected to UAPF; it is not
affiliated with any single product or vendor.
