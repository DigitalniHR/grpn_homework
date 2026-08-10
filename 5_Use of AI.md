# Use of AI

AI accelerated analysis, implementation and verification. It did not replace the architecture, the rating logic or the decisions behind them.

- **Data analysis first.** I reviewed the supplied data to establish what was usable as evidence and created the data map in Excalidraw. In parallel, I asked AI to analyze the same inputs and cross-check my conclusions.

- **Prototype in Google Sheets.** I built the model in a Sheet mainly for observability and flexibility — every join, formula and threshold stays visible and editable.

- **Architecture by hand, formulas with AI.** I designed the architecture myself and used AI to load the data and fill in the formulas.

- **No black-box formulas.** I understand every formula in the Sheet and can write and change it myself; AI was used for speed.

- **Rubric logic is mine.** Signals, weights and thresholds are my design decision.

- **Claude as an opponent.** I used Codex to challenge the model and find possible bugs in the Sheet. (Codex seems better in working with Google Sheets than Claude)

- **AI-assisted HTML implementation.** Codex generated the artifact from the specification and logic tested in the Sheet. I reviewed the behavior, challenged the edge cases, ran the tests and can explain or change the implementation.

- **Proofreading.** AI was used to correct and improve the written part.

- **Final read-through.** I had AI read the whole submission to check that it answers the brief in full, that every question is covered and that the explanation follows a logical flow.

The Sheet was built before the HTML artifact so every formula and policy decision could be inspected directly. The final rating logic remains in the editable `Settings` sheet / `rating_policy.json`, not in a prompt.
