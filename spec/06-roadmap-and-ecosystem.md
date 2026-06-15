# OIPF Specification — 06 Roadmap & Ecosystem

**Version 0.3.0 (draft)**

> **Discipline note.** The ecosystem and later roadmap phases below are **vision**, not the
> starting point. The format is *extracted* from real packages; registries and a marketplace
> are only credible after several working deployments. Do not front-load a grand standard.

## 1. Recommended initial scope

```
one area · one use case · one package · one model contract ·
one recommendation workflow · one savings calculation · one audit trail
```

A good first use case is cleaning/fouling optimisation: it connects sensor data, operating
states, procedures, downtime, resource use and *measurable* savings.

## 2. Roadmap (phased)

1. **Concept & reference model** — terminology, canonical objects, package + contract schemas. *(this repo)*
2. **First reference package** — one complete package end-to-end. *(heat-exchanger-fouling)*
3. **Reference runtime prototype** — load package → validate → read history → run model/rule → recommend → record decision → store outcome → audit log.
4. **Multi-use-case expansion** — energy-loss, predictive maintenance, quality-drift, downtime RCA.
5. **Governance & community** *(vision)* — publish draft spec, conformance tests, sample datasets, governance model, licensing.
6. **Ecosystem** *(vision)* — package registry, connector registry, model-contract registry, third-party packages, compatibility/certification.

## 3. Ecosystem vision *(later)*

**Package categories:** fouling/cleaning, energy, pump/compressor/boiler efficiency,
heat-exchanger and membrane performance, predictive maintenance, quality-drift, downtime
RCA, water/chemical reduction, bottleneck analysis. **Actors:** operators, integrators,
equipment makers, MES/SCADA vendors, digital-twin and process-engineering firms, research
labs, open-source community.

## 4. Risks & mitigations

| Risk | Mitigation |
|---|---|
| Framework too abstract | start from concrete use cases |
| Overlaps existing standards | clearly complementary scope (`00 §3`, `spec` standards table) |
| Buyers don't grasp it | sell business outcomes, not the framework |
| Too broad across industries | universal meta-model + domain packages |
| Becomes consulting-heavy | enforce package-based repeatability (overlays) |
| Safety concerns | advisory mode first, strict governance (`05`) |
| Data-quality problems | validation & data-readiness checks (`02 §7`) |
| Low adoption | open the schemas, publish reference packages |
