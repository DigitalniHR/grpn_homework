# Working MVP

## Google Sheet

The model was built first in Google Sheets so every join, formula, threshold and weight could be inspected and changed directly.

- `E_` sheets contain source data as supplied.
- `T_` sheets resolve identities, consolidate evidence and calculate the model.
- `R_` sheets contain the Manager Card and HR Dashboard.
- `Settings` is the editable source for weights and rating bands.

## HTML artifact

The HTML artifact mirrors the tested Sheet logic in a simpler interface. It does not read the Sheet at runtime.

- **Manager Card:** manager → direct report selection, individual and peer evidence, calculated rating, difference status, weekly context and manager explanation.
- **HR Dashboard:** manager, department and seniority filters; manager-vs-model KPI calibration; employee detail.

The artifact is a single local file with synthetic data embedded inside it. It needs no web server, package installation, public URL or API key.

## Run

```bash
open Groupon_Performance_MVP.html
```

Alternatively, double-click `Groupon_Performance_MVP.html`. It runs locally without installation, a web server or an API key.

## Submitted files

```text
README.md                         entry point
Presentation.html                 12-slide walkthrough
Groupon_Performance_MVP.html      runnable artifact
presentation-assets/              presentation screenshots
1_...md to 5_...md                analysis and handoff notes
```

The repository intentionally contains the finished case-study outputs only. Supplied source data and implementation/build files are not republished.
