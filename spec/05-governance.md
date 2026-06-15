# OIPF Specification — 05 Governance

**Version 0.3.0 (draft)**

## 1. Governance principles

1. **Human-in-the-loop by default** — first deployment mode recommends to humans, not autonomous control.
2. **Read-only before write-back** — connect read-only first; closed-loop only after validation, risk assessment and safety sign-off.
3. **Open interfaces, controlled runtime** — package schemas and connector interfaces should be open/transparent; runtimes and models may be commercial.
4. **Auditability** — every recommendation traces to data inputs, model version, constraints, confidence, human decision and outcome.
5. **Portability** — a package moves across sites by configuration (overlay), not redesign.
6. **Safety & compliance** — the framework must respect industrial safety, cybersecurity, quality, environmental and regulatory requirements; constraints are first-class objects.
7. **Versioning & rollback** — packages are versioned and rollback-capable.

## 2. Open specification vs proprietary runtime

A balanced strategy: open the interfaces, keep the engine commercial.

| Open specification | Proprietary / implementation-specific |
|---|---|
| package manifest | runtime engine |
| object model | advanced model implementations |
| model-contract schema | optimisation algorithms |
| recommendation schema | domain packages (or marketplace) |
| audit-log schema | operator user interface |
| connector abstraction | savings-attribution engine |
| validation-test format | deployment tooling / management console |

This supports trust and ecosystem growth without removing commercial opportunity.
