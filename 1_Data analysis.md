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

- 33 of 222 employees are absent from the identity map.
- Another 22 are blocked by shared handles.
- 55 employees therefore cannot be linked safely to all source systems.
- 12 task handles have an `_x` suffix and represent second accounts; without an explicit mapping, their work remains unassigned.
- 11 pairs share the same name, email and Jira username but have distinct employee IDs. The model preserves them as separate people because `employee_id` is authoritative.

After source and identity checks, 145 people have a complete evidence profile and 77 receive `Insufficient data`.

## What is usable

1. **KPI result** is the clearest outcome measure: actual performance against a stated target.
2. **Delivery effort** is usable activity context after excluding administration, bets and reporting tasks.
3. **Reviewed PR files changed** is usable Engineering activity context. Only PRs with at least one approval count.
4. **5/15 updates** provide context but receive zero weight.

## What is not usable as scored evidence

- Only 1,489 of 3,791 tasks are delivery work. The rest are reporting, administration or bets.
- All 327 bet updates are `On track`; a field with no variance cannot differentiate performance.
- Only 333 of 444 5/15 texts are unique. Forty templates repeat across people, so the text is not reliable scored evidence.
- 270 of 948 PRs have zero approvals and every PR is merged. Self-merges are not treated as verified activity.

## Baseline finding

Manager ratings have a correlation of **0.28** with KPI results and are not monotonic:

- median KPI result is 96% at rating 3 but 94% at rating 4;
- 10 people with a KPI result at or below 75% have rating 4–5;
- 7 people at or above 105% have rating 1–2.

This does not prove KPI is the complete definition of performance. It establishes a measurable internal inconsistency that the proposed model must improve.
