# OIPF Specification — 00 Overview

**Version 0.1.0 (draft)**

> For the first-principles rationale (why this layer is missing and why one general
> framework is possible), see [`../CONCEPT.md`](../CONCEPT.md).

## 1. Purpose

OIPF (Operational Intelligence Packaging Format) defines how a single
operational-intelligence use case is packaged so that it can be deployed, configured,
validated, audited and have its impact attributed **repeatably across industrial sites**.

The goal is to turn an industrial-AI deployment from a bespoke project into a portable,
versioned artifact.

## 2. Scope

In scope: the package format; canonical objects (asset graph, tags, states, events,
constraints, model contract, decision, workflow, outcome); deployment maturity levels;
conformance levels; the configuration/override mechanism for per-site adaptation.

Out of scope (referenced, not defined): connectivity (OPC UA, MQTT/Sparkplug), control
logic, enterprise/control hierarchy (ISA-95), recipe/batch structure (ISA-88), the
historian/lakehouse, and the physics/ML models themselves.

## 3. Principles

- **Above, not against.** OIPF references existing standards; it never reimplements them.
- **Meta-structure is universal; packages are domain-specific.** The objects below are
  shared; their contents differ per plant.
- **Extraction over invention.** The format is grown from real packages, not written ahead
  of them. New fields are promoted only after recurring across ≥2 independent packages.
- **Human-in-the-loop first.** Packages default to advisory (L1). Higher autonomy is earned
  per site and gated by declared constraints.
- **Every recommendation is explainable and economically attributed.**

## 4. Relationship to UAPF

UAPF packages an algorithm/process as code and makes it executable and auditable. OIPF
re-uses that DNA for the **decision/workflow** object — recommend → explain → approve →
act → record → feedback — and surrounds it with the plant context, model contract and
outcome ledger required to run a model on a real plant. In short: **OIPF is UAPF profiled
for operational technology, plus the contextualisation and outcome layers.**

## 5. Canonical object set

| Object | Role |
|---|---|
| Manifest | identity, version, conformance, object index, maturity level |
| Asset graph | physical/logical topology and flows |
| Tag map | site tag → canonical variable + unit |
| States & events | operating modes and discrete events |
| Constraints | the envelope the package may act within |
| Model contract | declarative I/O boundary of the model(s) |
| Decision | recommendation schema (action, reason, confidence, impact) |
| Workflow | the executable, auditable human-in-the-loop flow |
| Outcome | signed record of decision and measured result |

See `01-package-format.md` for the normative structure and `02-lifecycle-and-conformance.md`
for deployment, maturity and conformance.
