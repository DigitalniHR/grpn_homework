# Performance evaluation

Goal: Create a rule-based system taking into account available performance signals.


## Evidence logic

The design follows three rules:

1. outcomes > activity;
2. measured data > self-report;
3. activity is interpreted relative to people in the control group (same department and seniority).


## Rubric

1) KPI actual against target — highest confidence, structured data, consistent across the whole company.
It receives 75% weight in the rubric, split in a 3:1 ratio:

- **56.25 percentage points** for the person's individual KPI result against target
- **18.75 percentage points** for the person's KPI result relative to the average of the control group
- As a supporting criterion, the group component recognizes how KPIs are met within the control group (for example, missing the target but performing strongly in a difficult environment)
- It has been confirmed that employees in the same control group do have comparable KPIs (e.g. sales quota in the Sales dept.)

2) Activity relative to the group. Each activity signal is expressed as the person's value divided by the average of the control group.
It receives 25% weight in the rubric.

What counts in:
- Reviewed pull requests, number of files changed
- Sum of effort points for reported tasks (Asana, Jira)

- Engineering: 50/50 weight split between PRs and tasks
- Non-engineering: tasks only

3) Self-reported activity in 5/15
- Used for context only, no weight in the rubric


## Rating calculation

All weights and thresholds are editable in the Google Sheet `Settings` tab. The submitted HTML artifact contains the agreed final policy.

| Calculated score | Rating | Tag |
|---:|---:|---|
| below 75% | 1 | Lowest |
| 75–95% | 2 | Below |
| 95–105% | 3 | Mid |
| 105–125% | 4 | Above |
| 125% and above | 5 | Highest |

Missing required evidence is never converted to zero performance. It produces no calculated rating and the status `Insufficient data`. A peer group with fewer than three complete profiles is flagged as weak because its benchmark is unstable; the current MVP leaves the diagnostic rating visible for review.

Only complete profiles contribute to a control-group average. This prevents missing records from depressing the benchmark artificially. Production policy must distinguish an unresolved data gap from an approved exception such as sickness, leave or a source that is not applicable to the role. An exception needs a reason, owner and expiry date; it does not silently become a zero.

## Rating status

| Difference | Status | Required action |
|---:|---|---|
| 0 | Supported | no calibration action |
| 1 point difference | Justify | manager explains relevant context |
| 2+ points difference | Major gap | calibration discussion |
| no calculated rating | Insufficient data | repair evidence or identity coverage |

## How defensibility was tested

The first test is correlation with KPI and comparison with manager ratings. It is useful for internal consistency, but it is not an independent validation because KPI is also the largest input to the model.


On top of that, we ran an additional series of checks:


1. **Target ordering:** higher ratings should correspond to higher KPI results and fewer people below the company target.
2. **Dominance contradictions:** within the same peer group, a person should not receive a rating two or more points higher while being worse on every available signal.
3. **Obvious contradictions:** ratings 4–5 should not be assigned when the KPI result is below 75% without strong counter-evidence.

These checks test whether the decision can withstand a challenge. They do not claim to measure a person's true value.

## Results

All results use the 145 people with complete evidence.

| Rating | Manager n | Manager average KPI | Manager below target | Model n | Model average KPI | Model below target |
|---:|---:|---:|---:|---:|---:|---:|
| 1 | 12 | 81% | 92% | 31 | 69% | 100% |
| 2 | 32 | 89% | 72% | 35 | 87% | 94% |
| 3 | 51 | 95% | 53% | 28 | 97% | 57% |
| 4 | 31 | 92% | 65% | 32 | 106% | 28% |
| 5 | 19 | 106% | 47% | 19 | 119% | 5% |

- Dominance contradictions fall from **27 under manager ratings to 0 under the model**.
- Rating 4–5 with a KPI result below 75% falls from **8 people to 0**.

The new method is therefore more internally consistent and easier to defend. The resulting review queue is 48 `Supported`, 49 `Justify`, 48 `Major gap` and 77 `Insufficient data`. It is not proven objectively accurate: KPI is an input to the model, activity covers a shorter period than KPI, and peer groups may still combine different roles.

## Feedback loop

Every retained `Justify` or `Major gap` requires a short manager explanation. HR reviews recurring explanations after each company-defined rating cycle. A repeated reason indicates either missing evidence or a policy that should be reconsidered for that role.

Two independent outcome measures should be added in production:

1. **Manager adjustment rate:** after seeing the evidence recommendation, what proportion of managers change their proposed rating, in which direction, and why? This measures whether the system changes decisions rather than merely reproducing its own inputs.
2. **Employee fairness feedback:** after the cycle, ask employees whether the evidence was complete, understandable and fairly reflected in the conversation. Track the result over time and by role, while protecting anonymity.

These measures should sit alongside calibrated overrides and appeals. Together they test usefulness and perceived fairness without asking the score to validate itself.

In the `HR dashboard`, HR can review anomalies across the company.
