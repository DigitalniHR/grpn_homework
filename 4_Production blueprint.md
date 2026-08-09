# Production blueprint

## Access

- Employees see their own evidence; peer data is anonymous.
- Managers see named data for their reporting line.
- HR sees the company view.
- Until the policy is validated, employee access to peer comparisons should remain limited to avoid metric racing.

## Rating-cycle operation

```text
data hygiene → evidence calculation → manager review → gap explanation
→ calibration discussion where required → final human rating → policy review
```

The model runs once per rating cycle, a few weeks before rating conversations. Between cycles, only data-hygiene checks run. A permanent employee-monitoring dashboard would add surveillance pressure without improving the decision.

The pipeline reads existing operational systems. It does not add a new reporting process or require analysts to compile evidence manually. For 2,000 employees, calculation is a small batch job; the recurring work is resolving identity exceptions, weak peer groups and disputed evidence.

## Human decisions

- The manager submits the source rating.
- A one-point difference requires an explanation.
- A two-point or larger difference requires calibration.
- The manager and HR decide the final rating.
- HR owns role-specific weights, thresholds and policy changes.
- Employees can dispute incorrect identity links or source records.

## Operating measures

| Measure | Sample baseline | What improvement means |
|---|---:|---|
| Complete evidence coverage | 145 / 222 | identity and source coverage are improving |
| Major gaps | 48 / 145 comparable ratings | calibration is becoming more consistent |
| Weak peer groups | 6 groups below 3 complete profiles | benchmarks are becoming safer |
| Dispute rate | not available | evidence is being reviewed and corrected |

## Where it can fail

- **Metric gaming:** effort inflation or PR splitting. Mitigation: use effort rather than task count, reviewed files only, and keep activity at 25%.
- **Score becomes the goal:** people optimize visible traces instead of outcomes. Mitigation: retain manager context and a human final decision.
- **Period mismatch:** KPI and activity windows differ. Production must align and display the evaluation period.
- **Weak comparability:** department × seniority can still mix roles. Production needs role-level policy review and minimum cohort rules.
- **Missing or wrong identity:** work may be assigned to the wrong person or disappear. Unresolved joins remain visible and never become a low score.
- **Unequal observability:** Engineering produces more system traces than some other functions. Evidence requirements and access rules must be role-aware.

The operating principle is to automate evidence collection, not the performance decision.
