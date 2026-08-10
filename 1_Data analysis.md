# Data analysis

## Data supplied

| Source | Coverage | Period |
|---|---:|---|
| Employees | 222 people, 8 departments | current snapshot |
| KPI outcomes | 222 rows, one KPI per person | Q2 2026 |
| Tasks | 3,791 Jira and Asana tasks | 1–28 June |
| Pull requests | 948 PRs, 59 authors | 1–28 June |
| 5/15 updates | 444 self-reports | two weeks |
| Identity map | 188 rows, 178 unique emails | current snapshot |

The periods do not align. KPI covers Q2, activity covers four weeks and 5/15 covers two weeks. The prototype treats this as sample data and does not adjust the windows.

## Identity and coverage

All joins use confirmed `employee_id` mappings. Handles are never inferred from names.

- 33 of 222 employees are absent from the `identity_map.csv`
- Another 22 are blocked by shared handles.
- 55 employees therefore cannot be linked safely to all source systems.
- 12 task handles have an `_x` suffix and represent second accounts; without an explicit mapping, their work remains unassigned.
- 11 pairs share the same name, email and Jira username but have distinct employee IDs. The model preserves them as separate people because `employee_id` is authoritative.

After source and identity checks, 145 people have a complete evidence profile and 77 receive `Insufficient data`. The 145 complete profiles are also the only records allowed into activity peer benchmarks. A person with missing required evidence is excluded from both scoring and the corresponding control-group average; a missing record is never treated as zero performance.

Logic: removing unclear records is safer than assigning data to the wrong people.

In production, a weekly data-hygiene routine should identify missing evidence, notify the responsible employee or manager, and record approved exceptions such as sickness, leave or a role for which a source is not applicable. An exception needs a reason, owner and expiry date. Until the gap is resolved or approved, the person remains outside the score and the affected control-group benchmark.

## Data-hygiene checks

The Data Hygiene report makes every deterministic control explicit: **Problem type**, **What we do**, **How we detect it** and the current **Count**. Counts can overlap because one employee or source record may fail more than one check; they must not be added together as if they represented unique people.

The 15 checks cover four areas:

- **Identity:** duplicate names/emails with different Employee IDs, employees absent from the identity map, ambiguous logins, unmapped raw logins and secondary `_x` accounts. Employee ID remains the source of truth.
- **Required evidence:** missing KPI, delivery-task or reviewed-PR evidence and missing 5/15 updates. Required gaps produce `Insufficient data`; 5/15 remains a weekly follow-up rather than a score input.
- **Comparability:** department × seniority groups below the minimum of three complete profiles are flagged for HR review. Six of the 31 groups in this case-study dataset meet that condition. The POC does not merge groups automatically: in production, People/HR must decide whether adjacent seniority levels can be combined only after verifying comparable roles and KPIs; otherwise the group-relative benchmark remains diagnostic only.
- **Source and policy quality:** unreviewed merged PRs, repeated 5/15 templates, non-informative bet statuses, mismatched evidence windows and manager ratings without a defined period.

For the case study, these checks were run against the supplied files and their results were materialized in the report. In a Sheet-based production stage, a scheduled Google Apps Script would read all `E_` source sheets, run the same rule set consistently and rebuild `T_Data Hygiene Log` before any rating refresh.


## What is usable

1. **KPI result** is the clearest outcome measure: actual performance against a stated target.
2. **Delivery effort** is usable activity context after excluding administration, bets and reporting tasks.
3. **Reviewed PR files changed** is usable Engineering activity context. Only PRs with at least one approval count.
4. **5/15 updates** have inconsistent data quality: some entries are very ambiguous and the same reports repeat. They provide context but no reliable structured signal.

## What is not usable as scored evidence

- Only 1,489 of 3,791 tasks are delivery work. The rest are reporting, administration or bets.
- All 327 bet updates are `On track`; a field with no variance cannot differentiate performance.
- Only 333 of 444 5/15 texts are unique. Forty templates repeat across people, so the text is not reliable scored evidence.
- 270 of 948 PRs have zero recorded approvals and every PR is merged. Merged PRs without a recorded review are not treated as verified activity.

## Baseline finding

Across the 167 employees whose identity and KPI outcome can be resolved safely, manager ratings have a correlation of **0.28** with KPI results and show serious anomalies. This broader baseline is used only to diagnose the supplied manager ratings; the model itself is evaluated on the 145 complete profiles.

- average KPI result is 95% at rating 3 but 92% at rating 4;
- 10 people with a KPI result at or below 75% have rating 4–5;
- 7 people at or above 105% have rating 1–2.

This establishes a measurable internal inconsistency that the proposed model must improve. Because KPI is also the largest input to the proposed score, KPI alignment is an internal-consistency test, not independent proof that the model is fair or accurate.

For more detail, see the `R_HR Dashboard` tab in the Google Sheet prototype or the HR Dashboard in the HTML artifact.
