# Performance evidence review — handoff

A rule-based way to prepare performance ratings from evidence that already exists in operational systems. The calculated rating is a review prompt for the manager, not an automated HR decision.

## Read in this order

1. [Data analysis](1_Data%20analysis.md) — what the supplied data contains, what is usable as evidence and what is not.
2. [Performance evaluation](2_Performance%20evaluation.md) — rubric, weights, rating calculation, defensibility checks and results.
3. [Working POC](3_MVP.md) — the Google Sheet prototype and the runnable artifact.
4. [Production blueprint](4_Production%20blueprint.md) — how this would run for the whole company.
5. [Use of AI](5_Use%20of%20AI.md) — what was mine and what was AI-assisted.

## Try it

GitHub previews the file; it does not run the interactive app. To use it:

1. Open [`Groupon_Performance_POC.html`](Groupon_Performance_POC.html) and choose **Download raw**, or download the repository as a ZIP.
2. Keep the `.html` extension and open the downloaded file locally, for example by double-clicking it.

The file is self-contained: it needs no installation, web server, API key or internet connection after download. It opens in a current desktop browser such as Chrome, Safari or Firefox. Use the tabs in the top menu bar to switch between the Manager Card, HR Dashboard and Data Hygiene.

The downloadable file embeds synthetic case-study data and is a POC only; it must never be used to distribute or display production employee data.

The model itself is in the [Google Sheet prototype](https://docs.google.com/spreadsheets/d/1s1qiBj6gQVx3ynl_ltT5scdB2qJaQD57KEjnxf8MvA4/edit?usp=sharing), where every join, formula and weight can be inspected and changed. The artifact does not read it at runtime; [Working POC](3_MVP.md) explains how to navigate it.

In both prototypes, Data Hygiene first explains each control as **Problem type · What we do · How we detect it · Count**, then provides filters and the affected-record detail. The counts are overlapping signals, not a population total. The submitted results are a case-study snapshot; the production design uses an automated Google Apps Script run over every `E_` source sheet to refresh the issue log before scoring.
