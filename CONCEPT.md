# OIPF — A Concept

**Operational Intelligence Packaging Format**
*Concept note, v0.2 — derived from first principles; vendor- and domain-neutral.*

## 1. One line

OIPF makes an applied-intelligence use case **portable**: it packages the context,
decision logic, human-in-the-loop workflow and outcome contract a model needs in order to
run inside a real operational system — as a versioned, testable, auditable artifact. The
same capability then deploys across many sites by *configuration*, not reconstruction.

## 2. Where the idea comes from

Software has spent two decades making one layer after another reproducible by representing
it as versioned code:

- Infrastructure-as-Code — servers and networks
- Configuration-as-Code — application settings
- Policy-as-Code — access and governance rules
- Pipeline-as-Code — build and release
- **Process-as-Code (UAPF)** — algorithms and procedures, made executable and auditable

Each step took something that used to be rebuilt by hand on every project and turned it
into a portable artifact. **One layer is still bespoke on every project: putting a
decision-making model to work inside a live operational system.** OIPF is the next step in
that progression.

## 3. The problem, stated generally

A trained model is already portable — you can copy the file. What is *not* portable is
everything required to let that model act responsibly in the real world. On each
deployment, four things are rebuilt by hand:

1. **Meaning** — what each signal is, which asset it belongs to, what state the system is
   in. Raw signals carry no meaning on their own.
2. **Bounds** — the safety, quality, regulatory and operational limits inside which any
   action is permitted.
3. **Governance** — who approves an action, how it is explained, what happens on exception.
   Real operations keep humans accountable.
4. **Truth** — how you measure whether the action actually helped, and feed that back.

None of these travel with the model. So every site rebuilds them, and the capability never
compounds. **The bottleneck is not model accuracy; it is that judgment-in-context has no
portable form.**

## 4. The observation that makes a *general* framework possible

Operational domains differ in their physics. They do not differ in the *shape of a
governed decision*. Strip away the domain and every model-driven operational decision is
the same loop:

```
observe context → infer under declared validity → test against constraints
→ recommend with reason + confidence → human decides → act → record outcome → learn
```

A pump, a membrane, a heat exchanger, a substation, an HVAC plant, a pasteuriser: the
physics differ; this loop does not. **The invariant is the decision, not the domain.**

That single observation is what licenses one framework to serve water, manufacturing,
energy and buildings without pretending they are the same system. You standardise the
invariant loop and treat the domain specifics — tags, thresholds, models — as
configuration plugged into it.

## 5. What OIPF therefore is

A **packaging format and lifecycle for that invariant loop.** It sits *above* existing
operational standards and references them; it replaces none of them.

- It is **not** a control system (PLC/DCS/SCADA), a connectivity protocol
  (OPC UA, MQTT/Sparkplug), a data store (historian/lakehouse), or a model.
- It **is** the portable layer for *judgment*: context + constraints + model contract +
  governed decision + outcome, versioned as code.

## 6. Why each part of a package exists

The package objects are not a wish-list; each is forced by Section 3.

| Object | Exists because… |
|---|---|
| Context — asset graph + semantic tag map | signals need meaning (§3.1) |
| Constraints | actions need bounds (§3.2) |
| Model contract | the model must declare inputs, outputs and validity to be swappable and testable |
| Decision + workflow | judgment must be governed, explained and human-in-the-loop (§3.3) — the UAPF DNA |
| Outcome ledger | the loop must close and stay auditable (§3.4) |
| Validation tests | it is *as-code*, so it must be testable before deployment |
| Manifest | identity, version, conformance, maturity |

Remove any one object and a deployment again needs hand-work to fill the gap — which is
exactly what OIPF exists to prevent.

## 7. How portability actually works

A package ships as a **base** (the invariant loop plus the domain logic) and a per-site
**overlay** (tags, thresholds, model references). You adapt a deployment by writing an
overlay, never by forking the package — the way a Terraform module or a Helm chart is
reused across environments. Portability is a property of the structure, not of goodwill.

## 8. Governance is intrinsic, not added later

Because the format is for *consequential* decisions, governance is part of the artifact:

- **Advisory before autonomous** — packages default to recommending; a human acts.
- **Read before write** — connect read-only first; closed-loop only after validation and risk sign-off.
- **Constraints as hard guards** — at higher autonomy, the constraint object is the enforced envelope.
- **Signed provenance** — every decision and outcome traces to data window, model version, approver and result.

Maturity is declared per package (L0 monitor → L4 bounded-autonomous) and granted per site.

## 9. Relationship to UAPF

UAPF packages an algorithm or procedure and makes it executable and auditable. OIPF takes
that executable-process DNA for its **decision/workflow** object and surrounds it with the
three things a *stateful, real-world, consequential* execution additionally needs: context
(meaning), a model contract (swappable inference) and an outcome ledger (closing the loop).
In one sentence: **OIPF is UAPF extended from "an executable process" to "a governed
operational decision."** ProcessGit provides the version-control substrate; VeriDocs signs
the outcome ledger.

## 10. How it must be built

The format is **extracted, not invented.** Only the invariant loop is fixed up front.
Every object and field beyond it earns its place by recurring, in materially the same
shape, across at least two independent packages in two settings. There is no 200-page
standard on day one — there are reference packages, and the stable parts are promoted later.

## 11. The same skeleton, two domains

The point of the framework is that the *skeleton does not change* between these; only the
overlay does.

- **Water utility** — a membrane-integrity package: context = treatment train +
  flux/pressure/turbidity tags; constraints = permeate-quality + transmembrane-pressure
  limits; model contract = fouling trajectory; decision = clean / defer with reason;
  outcome = energy + chemical use, recorded.
- **Process manufacturing** — a heat-exchanger package: same skeleton; context =
  exchanger + duty/temperature/flow tags; model contract = fouling-resistance trajectory;
  decision = schedule / defer; outcome = energy use, recorded.

Different physics, identical structure. That identity *is* the deliverable.

## 12. What this is good for

- Deploying the same operational-intelligence capability across many sites without rebuilding it each time.
- Making AI in operations auditable end-to-end: data → model version → constraints → human decision → outcome.
- Keeping models swappable behind a stable contract.
- Turning tribal operating knowledge into versioned, testable artifacts.
- Giving an organisation a portable asset that compounds with every deployment, instead of a string of one-off projects.

## 13. In one sentence

**Operational intelligence becomes portable when the meaning, the limits, the human
decision and the measured outcome around a model are treated as code — and that is
possible because, across domains, the structure of an operational decision does not change.**
