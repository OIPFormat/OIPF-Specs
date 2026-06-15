# Use case: Predictive Maintenance

**Problem.** Run-to-failure causes unplanned downtime; fixed-interval maintenance replaces
healthy parts. Neither uses the asset's actual condition.

**Context.** Rotating/critical assets; condition tags (vibration, temperature, current,
acoustic); failure modes; maintenance history; spare-part lead times; downtime cost.

**Model contract.** Inputs: condition-signal history. Outputs: degradation state, estimated
remaining useful life with confidence band, dominant failure mode.

**Decision & workflow.** "Asset X — intervene within window W (mode M)" → explain →
planner schedules within a maintenance window respecting spares → work order → record →
compare predicted vs. observed at intervention.

**Savings.** Avoided unplanned-downtime cost + avoided premature replacement, net of planned
intervention. **Start at L1–L2.**
