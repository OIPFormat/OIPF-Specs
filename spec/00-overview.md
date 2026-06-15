# OIPF Specification — 00 Overview

**Version 0.3.0 (draft)**

> For the first-principles rationale (why this layer is missing and why one general
> framework is possible), see [`../CONCEPT.md`](../CONCEPT.md).

## 1. Purpose & scope

OIPF defines how a single operational-intelligence use case is packaged so that it can be
deployed, configured, validated, audited and have its impact attributed **repeatably
across sites**. It turns an industrial-AI deployment from a bespoke project into a
portable, versioned artifact.

**In scope:** the package format and canonical objects; the framework architecture and its
components; deployment maturity and conformance; governance principles; the per-site
configuration (overlay) mechanism.

**Out of scope (referenced, not defined):** connectivity (OPC UA, MQTT/Sparkplug), control
logic (PLC/DCS/SCADA), enterprise/control hierarchy (ISA-95), recipe/batch structure
(ISA-88), the historian/lakehouse, and the physics/ML models themselves.

## 2. Core definition

**Operations-as-Code** means representing an operational decision capability as a
versioned, machine-readable, testable, auditable, deployable artifact. An OIPF package may
carry: plant/asset structure; tag-to-asset mapping; process flows; operating modes;
constraints (safety, quality, environmental, operational); model input/output contracts;
recommendation logic; human-approval workflow; savings logic; validation tests; audit
policy; outcome-feedback structure.

## 3. What OIPF is not

It is **not** a replacement for PLC/DCS/SCADA control; not a replacement for
MES/CMMS/ERP/historians; not a replacement for OPC UA/ISA-88/ISA-95/MQTT/Sparkplug; not a
closed communication protocol; not a hard real-time control layer; not a universal AI
model; and not an attempt to automate control without human governance. It is an
additional **semantic, operational and AI-native packaging layer** above existing systems.

## 4. Problem statement — seven recurring barriers

Operational-AI projects tend to fail to scale for the same reasons, regardless of domain:

1. **Fragmented operational data** — distributed across SCADA, DCS, historians, MES, CMMS,
   ERP, quality systems, spreadsheets, documents and operator logs.
2. **Poor contextualisation** — a tag may be readable but is not mapped to an asset,
   process step, state, constraint or business impact.
3. **Tribal knowledge** — critical operating logic lives in people's experience, not in
   machine-readable form.
4. **Bespoke deployments** — each site re-does data engineering, mappings, model inputs,
   workflows and dashboards.
5. **Weak transferability** — models and workflows built for one site do not move to
   another because the context is not packaged.
6. **Limited auditability** — recommendations lack a trail of data used, model version,
   constraints checked, who approved, and what happened.
7. **No production-native AI governance** — generic AI-governance frameworks cover model
   risk but not the full operational chain: data → recommendation → approval → action →
   outcome → learning.

Each OIPF object (§ in `02-components.md`) maps directly onto one or more of these barriers.

## 5. Canonical object set (summary)

Manifest · Asset graph · Tag map · States & events · Constraints · Model contract ·
Decision · Workflow · Outcome. Detailed in [`03-package-format.md`](03-package-format.md);
the surrounding framework components in [`02-components.md`](02-components.md).
