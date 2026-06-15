# OIPF Specification — 03 Package Format

**Version 0.3.0 (draft)**

## 1. Structure

A package is a directory (or archive) rooted at a manifest named `oipf.yaml`.

```
<package>/
  oipf.yaml              # manifest (required)
  asset-graph.yaml       # required
  tag-map.yaml           # required
  states-events.yaml     # recommended
  constraints.yaml       # required for L2+
  model-contract.yaml    # required
  workflow.yaml          # required
  savings.yaml           # required for conformance "Plus"
  validation-tests.yaml  # required for conformance "Plus"
```

Per-site adaptation uses **overlays**: a deployment supplies `site.<id>.yaml` that overrides
tag mappings, constraint thresholds and parameters. The base package is unchanged across
sites — portability is a property of the structure, not of goodwill.

## 2. Manifest (`oipf.yaml`)

Required: `oipf` (spec version), `id`, `version`, `title`, `domain`, `maturity` (L0–L4),
`conformance` (Core | Plus | Signed), `objects` (object → file map). Optional: `description`,
`authors`, `tags`, `x-` extensions. Schema: `schemas/oipf.package.schema.json`.

## 3. Objects (normative summary)

- **Asset graph** — `Site → Area → System → Unit → Asset` + `flows`; ISA-95-aligned. (`schemas/asset-graph.schema.json`)
- **Tag map** — site tag → canonical `variable` + `unit` + `quantity` + `asset_ref`, optional `derivation`.
- **States & events** — operating modes with entry/exit predicates; discrete events with detection rules; ISA-88-aligned.
- **Constraints** — `safety`/`quality`/`environmental`/`operational` with `severity` and `on_violation` (`block`/`warn`/`escalate`).
- **Model contract** — `inputs` (variable + window), `outputs` (type/range/confidence), `validity`, `model_ref`, `version`. (`schemas/model-contract.schema.json`)
- **Decision & workflow** — recommendation schema + `explain → approve → act → record → feedback`. (`schemas/workflow.schema.json`)
- **Outcome** — append-only ledger entry per decision with disposition, measured result, attributed saving and provenance. (`schemas/outcome.schema.json`)

## 4. Cross-reference rules (validator MUST check)

Every model-contract input resolves to a tag-map entry; every tag-map `asset_ref` exists in
asset-graph; every constraint references known variables; the manifest's `maturity` is
supported by the present objects (e.g. L2 requires `constraints.yaml`).
