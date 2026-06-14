# OIPF Specification — 01 Package Format

**Version 0.1.0 (draft)**

## 1. Package structure

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

Per-site adaptation is done by **overlays**: a deployment supplies a `site.<id>.yaml`
that overrides tag mappings, constraint thresholds and parameters without forking the
package. The base package stays identical across sites.

## 2. Manifest (`oipf.yaml`)

Required keys: `oipf` (spec version), `id`, `version`, `title`, `domain`, `maturity`
(L0–L4), `conformance` (Core | Plus | Signed), and `objects` (a map of object → file).
Optional: `description`, `authors`, `tags`, `x-` extensions.

See `schemas/oipf.package.schema.json`.

## 3. Asset graph

A directed hierarchy `Site → Area → System → Unit → Asset`, plus `flows` describing the
movement of material, water, energy, steam or chemicals between assets. Each asset carries
an `isa95_role` hint where applicable. See `schemas/asset-graph.schema.json`.

## 4. Tag map

Maps site-specific tags (historian/SCADA names) to **canonical variables** with explicit
`unit`, `quantity` (e.g. temperature, pressure, flow), `asset_ref`, and optional
`derivation` (for computed variables such as an overall heat-transfer coefficient).

## 5. States & events

`states`: named operating modes (e.g. `in_service`, `cleaning`, `bypass`, `startup`),
each with an entry/exit predicate over canonical variables. `events`: discrete occurrences
(e.g. `cleaning_performed`, `fault`, `threshold_crossed`) with detection rules.

## 6. Constraints

The envelope within which the package may recommend or act: `safety`, `quality`,
`environmental`, `operational` limits. Each constraint has a `severity` and an
`on_violation` policy (`block`, `warn`, `escalate`). For L3+ these are hard guards on
autonomous action.

## 7. Model contract

Declarative I/O boundary that decouples the model from the deployment:
`inputs` (canonical variables + window), `outputs` (predictions/recommendations with
ranges and `confidence`), `validity` (input ranges within which outputs are trusted),
`model_ref` (opaque pointer to the proprietary model), and `version`.
See `schemas/model-contract.schema.json`.

## 8. Decision & workflow

`decision`: the recommendation schema — `action`, `reason`, `confidence`,
`predicted_impact`, `valid_until`. `workflow`: the executable steps that take a decision
through `explain → approve → act → record → feedback`, including the `approver` role and
`exception` handling. See `schemas/workflow.schema.json`.

## 9. Outcome

A runtime, append-only ledger entry per decision: `decision_ref`, `disposition`
(`accepted` | `rejected` | `modified`), `action_taken`, `measured_result`,
`attributed_saving`, and provenance (`model_version`, `data_window`, `actor`, `timestamp`).
At conformance **Signed**, each entry carries a DID/VC signature. See
`schemas/outcome.schema.json`.
