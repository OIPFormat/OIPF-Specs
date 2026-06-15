# Use case: Downtime Root-Cause Analysis

**Problem.** The same stoppages recur because cause analysis is manual, slow, and not
captured in a form that prevents the next occurrence.

**Context.** Alarms, operator logs, maintenance records, process state and event sequences
across the line graph; downtime categories and cost.

**Model contract.** Inputs: event/alarm/state sequences around stoppages. Outputs: ranked
probable root causes, contributing event chain, similar-past-incident references,
confidence.

**Decision & workflow.** On a stoppage: assemble the event chain → propose ranked causes
with evidence → engineer confirms/corrects → record cause + corrective action → feed
operational memory so the pattern is recognised next time.

**Savings.** Reduced repeat downtime via faster diagnosis and prevention. **Start at
L0–L1** (analysis/advisory; this use case is read-mostly).
