# Performance evidence review

## 1. Submission

**Groupon · AI-First CEO Office (People)**

**Performance evidence review**

A transparent prototype for making performance conversations more evidence-grounded.

- `Presentation.html`: this walkthrough
- `1_Data analysis.md` to `5_Use of AI.md`: analysis, model, MVP, operation and AI use
- `Groupon_Performance_MVP.html`: runnable Manager Card and HR Dashboard
- Google Sheet: transparent modeling prototype

**Presentation**

What was found, what was built and how it is evaluated.

**Numbered details**

Short source documents for analysis, evaluation, MVP, operation and AI.

**Runnable artifact + Sheet**

A local Manager Card and HR Dashboard, with the Sheet retained as the transparent model prototype.

## 2. What we found in the data

**The inputs contain both useful evidence and material noise**

### Safe population first

- 145 complete profiles
- 77 insufficient profiles
- 33 people absent from identity map
- 22 people blocked by shared handles
- Strict join: handles are never inferred from names, only employee ID

This bar separates profiles eligible for an evidence score from profiles held out because evidence is incomplete.

Missing evidence becomes **Insufficient data**, never low performance.

### What cannot be scored as delivered performance

| Signal | Finding | Decision |
| --- | --- | --- |
| Tasks | 1,489 / 3,791 are delivery work | Exclude admin, reporting and bets |
| Bets | 327 / 327 marked “On track” | No variance, exclude |
| 5/15 | 333 / 444 texts are unique | Context only |
| PR | 270 / 948 have no approval | Count reviewed files only |

The model starts by removing unreliable evidence, not by scoring everything available.

KPI covers Q2; tasks and PR cover four weeks; 5/15 covers two weeks.

## 3. Current calibration

**Manager rating is only weakly related to KPI results**

Chart: *Median KPI result by manager rating.*

This chart plots median KPI result for each existing manager-rating level. Rating 4 is below rating 3, so the rating scale is not consistently ordered by KPI result.

- KPI × rating correlation: **0.28**
- Rating 4 has lower median KPI result than rating 3: **94% vs 96%**
- 10 people: KPI at or below 75%, rating 4–5
- 7 people: KPI at or above 105%, rating 1–2

This is a consistency baseline, not a claim that KPI fully defines performance.

## 4. Signals selected

**Results are primary; activity is verified, role-aware context**

### KPI result: Primary

Actual result against an explicit target. This is the strongest observable outcome signal.

### Activity: Verified

Delivery effort for all roles; reviewed PR files for Engineering. No unapproved PRs, admin tasks or Bet updates.

### Control group: Relative

Department × seniority peers provide a benchmark when an absolute target is absent. Fewer than 3 complete profiles means a weak benchmark.

5/15 updates remain visible as context, but have **0% rating weight**.

## 5. Rubric

**One weighted score, five editable bands**

**56.25% KPI vs target + 18.75% KPI vs peers + 25% activity vs peers**

| Component | Logic | Weight |
| --- | --- | --- |
| KPI | Result against target plus position in the peer group | 75% total |
| Activity | Delivery effort; Engineering splits delivery and reviewed PR files 50/50 | 25% total |
| Settings | Weights, step and bands are visible and editable in the Sheet | No hidden rules |

Screenshot caption: The Settings tab is the single visible place for weights, step and rating bands.

No required evidence means **no calculated rating**.

## 6. Who decides

**The system proposes a rating; the manager and HR make the judgment**

1. Gather evidence
2. Calculate proposal
3. Show rating gap
4. Manager adds context
5. Calibrate exceptions
6. Human final rating

| Status | Difference | Required action |
| --- | --- | --- |
| Supported | 0 | Manager rating and calculated rating match. No calibration action. |
| Justify | 1 | One-point difference. Manager records relevant context. |
| Major gap | 2+ | Two or more points. HR calibration discussion. |

The calculated rating is a **review proposal**, never the final performance decision.

## 7. Manager Card

**One view combines evidence, peer context and the required action**

Screenshot caption: The Manager Card brings selection, individual evidence, peer context, rating proposal and manager feedback into one workflow.

1. **Select manager and employee**: the employee list contains only direct reports of the selected manager.
2. **Compare individual result with peers**: KPI result, delivery effort and reviewed PR activity are shown against department × seniority peers.
3. **See the rating proposal and gap**: manager rating, calculated rating, evidence score and status stay side by side.
4. **Capture manager context**: feedback is required when a gap remains before the final decision.

## 8. HR Dashboard

**The company view shows where manager ratings need a challenge**

Screenshot caption: The HR Dashboard compares the same filtered population across the manager rating and calculated rating.

1. **Filter one population**: manager, seniority and department filters drive table, chart and employee detail together.
2. **Compare both rating systems**: counts, median KPI result and below-target share for manager and calculated ratings.
3. **Inspect people behind the gap**: HR can investigate the exact evidence and manager explanation.

### Defensibility checks

- Dominance contradictions: **27 → 0**
- High rating plus KPI result below 75%: **8 → 0**
- **84%** remain within one point in odd/even-week split

No ground-truth performance label exists. These tests show internal consistency and defensibility, not objective accuracy.

## 9. Role of AI

**AI accelerated the work; it does not rate people**

1. **Manual model first**: dependency map, joins, weights and thresholds were designed in the transparent Google Sheet.
2. **AI-assisted implementation**: analysis, formulas, edge-case checks, interface copy and HTML implementation.
3. **Deterministic output**: the final logic is an observable rubric and Settings, not an opaque prompt or runtime AI call.

Screenshot caption: The runnable artifact mirrors the Manager Card workflow. It contains no runtime AI call.

AI helps build and test the system. **Humans remain accountable for ratings.**

## 10. Production blueprint

**Run before rating conversations; automate evidence, not the decision**

1. Data hygiene
2. Evidence calculation
3. Manager review
4. Gap explanation
5. Calibration where needed
6. Final human rating

### Access

- Employee: own evidence; peers anonymous
- Manager: named reporting line
- HR: company calibration

### Human gates

- 1 point: manager justification
- 2+ points: calibration discussion
- Final: manager and HR decision

### Operating measures

- 145 / 222: complete coverage
- 48 / 145: major gaps
- 6 groups: weak benchmarks

Watch coverage, major gaps, weak peer groups and dispute rate. Protect against metric gaming, period mismatch, wrong identity and unequal observability.

The calculated rating is a diagnostic review proposal, not an automated HR decision.
