# Use case: Cleaning / Fouling Optimisation

**Problem.** Fixed, conservative cleaning schedules cost money both ways: too early wastes
labour, chemicals and downtime; too late wastes energy/throughput and risks quality.

**Context.** Assets that foul (exchangers, membranes, filters, evaporators); tags for the
performance indicator (heat-transfer coefficient, transmembrane pressure, differential
pressure, flux); operating states incl. cleaning cycles; cleaning events.

**Model contract.** Inputs: performance-indicator + flow/pressure history. Outputs: fouling
trajectory, optimal clean-by date, confidence.

**Decision & workflow.** "Schedule cleaning in N days" → explain (trajectory, penalty,
slot) → engineer approves → CMMS work order → record → compare post-clean reset vs.
predicted.

**Savings.** Energy/throughput penalty from degraded performance vs. clean baseline, net of
cleaning cost. **Start at L2.** Worked example: [`../examples/heat-exchanger-fouling`](../examples/heat-exchanger-fouling).
