# Working MVP

## Google Sheet

The model was built first in Google Sheets for flexibility and observability.

- `E_` sheets contain source data as supplied.
- `T_` sheets resolve identities, consolidate evidence and calculate the model.
- `R_` sheets contain the Manager Card, HR Dashboard and Data Hygiene report.
- `Settings` is the editable source for weights and rating bands.

Link: https://docs.google.com/spreadsheets/d/1s1qiBj6gQVx3ynl_ltT5scdB2qJaQD57KEjnxf8MvA4/edit?usp=sharing

- To test the model, use `R_Manager Card` and select the manager and the direct report in cells `B3` and `B4`.
- You can see the manager rating, the rubric calculation, the proposed calculated rating and a chart of team performance.

- To see the company-wide result, use `R_HR Dashboard`. Select the area to measure: Manager (`B17`), Seniority (`D17`) or Department (`F17`).
- The dashboard compares the manager rating with the calculated rating within the selected control group.

- To review data quality, use `R_Data Hygiene`. The upper section lists every control as **Problem type**, **What we do**, **How we detect it** and **Count**. These are global, overlapping counts. The filters below apply to the affected-record detail, which includes source, severity, explanation and required action.
- `T_Data Hygiene Log` contains the auditable case-study output of the deterministic checks.

## HTML artifact

The HTML artifact mirrors the tested Sheet logic in a simpler interface. Its synthetic data and Data Hygiene results are embedded when the file is built.

- **Manager Card:** manager → direct report selection, individual and peer evidence, calculated rating, difference status, weekly context and manager explanation.
- **HR Dashboard:** manager, department and seniority filters; manager-vs-model KPI calibration; employee detail.
- **Data Hygiene:** the same four-column control catalog as the Sheet, followed by filters and the affected-record issue log.

The HTML artifact cannot fetch production data or rerun the hygiene checks at runtime.

This limitation is a deliberate scope decision. The case study is primarily about the design of the system—evidence rules, data controls, exceptions and human decision gates—rather than proving that I can build a production integration.

A single self-contained HTML file is also simple to share, and gave me confidence that a reviewer could open it reliably without installation, credentials, a web server or an API key. A full deployment was unnecessary for this case study.

In production, the Data Hygiene tests would be fully automated by a scheduled Google Apps Script over all `E_` source sheets. The script would refresh `T_Data Hygiene Log`; people would still resolve ambiguous identities and approve documented exceptions.

## Run

Open `Groupon_Performance_MVP.html`, or simply double-click the file. Use the tabs in the top menu bar to switch between the Manager Card, HR Dashboard and Data Hygiene.

`Groupon_Performance_MVP.html` is the standalone file to share with reviewers. The linked Google Sheet exposes the joins, formulas and editable policy assumptions for direct inspection.
