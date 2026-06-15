# Use case: Energy-Loss Detection

**Problem.** Assets drift from their efficient operating point; the loss is invisible
because nothing compares actual consumption to what it *should* be at the current load.

**Context.** Energy-consuming assets (pumps, compressors, fans, boilers, chillers); tags
for power/fuel, production load, ambient conditions; expected-efficiency curves; energy
price.

**Model contract.** Inputs: consumption + load + conditions. Outputs: expected vs. actual
consumption, anomaly flag, estimated loss rate, probable cause class, confidence.

**Decision & workflow.** "Asset X is consuming N% above expected at this load" → explain →
operator/engineer reviews → corrective action or work order → record → verify recovery.

**Savings.** Recovered energy = (actual − expected) consumption × price over the corrected
period. **Start at L1.**
