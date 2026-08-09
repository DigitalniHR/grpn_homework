# Performance evaluation

## Decision supported

The model calculates an evidence-based rating and compares it with the manager rating. It does not set the final rating. It identifies which ratings need no action, a manager explanation or a calibration discussion.

## Evidence policy

The design follows three rules:

1. results carry more weight than activity;
2. verified system data carries more weight than self-report;
3. activity is interpreted relative to people in the same department and seniority.

| Evidence | Weight | Treatment |
|---|---:|---|
| KPI against target | 56.25% | individual result |
| KPI relative to peer group | 18.75% | department × seniority average |
| Activity relative to peer group | 25% | delivery; Engineering splits delivery and reviewed PRs equally |
| 5/15 | 0% | visible context only |

Only delivery tasks with effort count. PR activity counts reviewed files changed, not lines of code or unapproved self-merges.

## Rating calculation

All weights and thresholds are editable in the Google Sheet `Settings` tab. The submitted HTML artifact contains the agreed final policy.

| Calculated score | Rating | Tag |
|---:|---:|---|
| below 75% | 1 | Lowest |
| 75–95% | 2 | Below |
| 95–105% | 3 | Median |
| 105–125% | 4 | Above |
| 125% and above | 5 | Highest |

Missing required evidence is never converted to zero performance. It produces no calculated rating and the status `Insufficient data`. A peer group with fewer than three complete profiles is flagged as weak because its benchmark is unstable; the current MVP leaves the diagnostic rating visible for review.

## Rating status

| Difference | Status | Required action |
|---:|---|---|
| 0 | Supported | no calibration action |
| 1 point | Justify | manager explains relevant context |
| 2+ points | Major gap | calibration discussion |
| no calculated rating | Insufficient data | repair evidence or identity coverage |

## How defensibility was tested

There is no ground-truth performance label in the dataset, so the model cannot be tested for predictive accuracy. It is tested against four observable consistency checks:

1. **Target ordering:** higher ratings should correspond to higher KPI attainment and fewer people below the company target.
2. **Dominance contradictions:** within the same peer group, a person should not receive a rating two or more points higher while being worse on every available signal.
3. **Obvious contradictions:** ratings 4–5 should not be assigned when KPI attainment is below 75% without strong counter-evidence.
4. **Stability:** splitting activity into odd and even weeks should not move most people by more than one rating point.

These checks test whether the decision can withstand a challenge. They do not claim to measure a person's true value.

## Results

All results use the 145 people with complete evidence.

| Rating | Manager median KPI | Manager below target | Model median KPI | Model below target |
|---:|---:|---:|---:|---:|
| 1 | 77% | 92% | 68% | 100% |
| 2 | 90% | 72% | 89% | 94% |
| 3 | 96% | 53% | 96% | 62% |
| 4 | 94% | 65% | 106% | 26% |
| 5 | 102% | 47% | 116% | 5% |

- Dominance contradictions fall from **27 under manager ratings to 0 under the model**.
- Rating 4–5 with KPI attainment below 75% falls from **8 people to 0**.
- In the odd/even-week split, **84%** of people remain within one rating point.

The new method is therefore more internally consistent and easier to defend. It is not proven objectively accurate: KPI is an input to the model, activity covers a shorter period than KPI, and peer groups may still combine different roles.

## Feedback loop

Every retained `Justify` or `Major gap` requires a short manager explanation. HR reviews recurring explanations after each rating cycle. A repeated reason indicates either missing evidence or a policy that should be reconsidered for that role. Policy changes apply only after review across managers, not from a single exception.
