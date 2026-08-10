# Production blueprint

## Access

- Employees see their own evidence; peer data is anonymous.
- Managers see named data for their reporting line.
- HR sees the company view.

The level of transparency depends on the company culture and its approach to performance management.

## Data

- Connect the system to data sources such as GitHub, Asana, Jira, KPI tracking and 5/15 tracking.
- Run regular routines to fetch the data and store it in a data warehouse the system reads from.
- Manager feedback is stored in the system as well.
- With every data fetch, run deterministic data-hygiene checks and write every issue to one auditable log.
- We can consider using AI to read text comments and assess their quality, specificity and measurability.

### Automated Data Hygiene in Google Sheets

For the Sheet-based production stage, a time-driven Google Apps Script runs after source refreshes. It reads every `E_` sheet in batches, applies one versioned deterministic rule library, and rebuilds `T_Data Hygiene Log`. `R_Data Hygiene` only presents that output; it does not duplicate the test logic.

```text
E_Employees + E_Identity Map + E_KPI + E_Tasks + E_PR + E_Weekly Reports
                              │
                              ▼
             Google Apps Script · scheduled trigger
                  batch read → deterministic tests
                              │
                              ▼
              T_Data Hygiene Log · auditable output
                    │                         │
                    ▼                         ▼
          R_Data Hygiene report      reminders to the owner
                    │
                    ▼
     quality gate: successful, current run required before scoring refresh
                    │
                    ▼
     human gate: manager / People Ops resolves identity or approves exception
```

The automated checks cover identity uniqueness and mapping, required evidence, weak control groups, PR review evidence, repeated 5/15 text, non-informative bet status and period alignment. A failed or stale script run stops the scoring refresh and alerts the process owner. The tests and log refresh are fully automated; resolving ambiguous identities and approving sickness, leave or role exceptions remain human decisions.

## Weekly operation

Once a week, the system runs two small routines:

1. **Data hygiene:** the scheduled Apps Script checks source freshness, identity resolution, required evidence, missing 5/15 updates, unreviewed merged PRs, repeated templates, period mismatches and weak control groups. The issue log records the affected person or system, source, severity, explanation and required action. Missing-data reminders go to the responsible employee or manager.
2. **Manager context summary:** send each manager a short factual view of their own reporting line: 5/15 updates, delivery tasks and reviewed PR activity. This is context for follow-up, not a live performance score and not a new reporting obligation.

The weekly health measures are complete-profile coverage overall and by department/seniority, unresolved identity and missing-evidence count and age, source freshness, weak-control-group count, reminder resolution rate, and successful delivery of the manager summaries.

Approved exceptions such as sickness, leave or a source that does not apply to a role need a documented reason, owner and expiry date. While evidence is unresolved or excepted, it is excluded from scoring and from the affected control-group average.

## Rating-cycle operation

data hygiene → evidence calculation → manager review → gap explanation
→ calibration discussion where required → final human rating → policy review

The brief does not define how often formal ratings happen. The model therefore runs once per company-defined rating cycle, a few weeks before rating conversations. HR reviews the results and outcome feedback after each cycle.

Between cycles, the weekly hygiene check and manager context summary run; calculated ratings do not. A permanent live employee-scoring dashboard would add surveillance pressure without improving the decision.

Independent validation should include the manager adjustment rate after recommendations are shown and an anonymous employee fairness survey after rating conversations. Calibrated overrides and appeals add a third source of evidence about where the rubric misses relevant context.

The pipeline reads existing operational systems. It does not add a new reporting process or require analysts to compile evidence manually.
For 2,000 employees, calculation is a small batch job; the recurring work is resolving identity exceptions, weak peer groups and disputed evidence.

## Interface

The trend is to move toward helpful agents rather than yet another system interface. Part of the interaction can happen where employees already work, for example in Slack.

A Slack bot could remind people to submit their data and let them submit it directly in the conversation, send managers a short regular summary, and alert them to upcoming activities.


## Human decisions

- The manager submits the source rating.
- A one-point difference requires an explanation.
- A two-point or larger difference requires calibration.
- HR owns role-specific weights, thresholds and policy changes.

- Plan: deploy an AI copilot that reads all metrics, context and signals and helps the manager (ask the right questions, challenge the decision, prepare for 1-1s).
- AI should support analysis and interpretation of information; it should not take part in any decision.


## Where it can fail

- **Metric gaming:** effort inflation or PR splitting. Mitigation: use effort rather than task count, reviewed files only, and keep activity at 25%.
- **Score becomes the goal:** people optimize visible traces instead of outcomes. Mitigation: retain manager context and a human final decision.
- **Period mismatch:** KPI and activity windows differ. Production must align and display the evaluation period.
- **Weak comparability:** department × seniority can still mix roles. Production needs role-level policy review and minimum cohort rules.
- **Missing or wrong identity:** work may be assigned to the wrong person or disappear. Unresolved joins remain visible and never become a low score.
- **Unequal observability:** Engineering produces more system traces than some other functions. Evidence requirements and access rules must be role-aware.

The operating principle is to automate evidence collection, not the performance decision.

## Long-term product direction: the “Garmin” idea

This is a future product hypothesis, not part of the rating rubric or the MVP. Like a sports tracker, the system could collect useful work signals automatically and give employees a vivid private view of their own effectiveness.

Possible future signals include autonomous AI runs, context switching, blocks of focused work and the quality of agent prompting. Their purpose would be employee development, not rating input. Any experiment would need clear employee benefit, opt-in or equivalent privacy governance, and separate validation before it could influence performance decisions.
