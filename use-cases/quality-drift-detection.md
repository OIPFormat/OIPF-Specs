# Use case: Quality-Drift Detection

**Problem.** Quality failures are detected at the end (lab result, reject batch), long after
the process began drifting — so the loss is already incurred.

**Context.** Process variables tied to quality; recipes; batch events; lab/LIMS results;
quality thresholds; the asset/line graph linking them.

**Model contract.** Inputs: in-process variables + recipe + recent lab results. Outputs:
predicted quality metric, drift flag, contributing variables, confidence.

**Decision & workflow.** "Batch B drifting toward spec limit on parameter P" → explain
(which variables) → operator adjusts within constraints / holds batch → record → confirm
against final lab result.

**Savings.** Avoided rework/scrap + avoided giveaway, plus tighter, more consistent
operation. **Start at L1.**
