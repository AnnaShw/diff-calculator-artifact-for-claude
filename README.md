# Difference Calculator

A lightweight, single-file calculator for comparing two numbers. No dependencies, no build step — just open the HTML file in a browser.

## Features

- **Absolute difference** — `|A − B|`
- **Relative difference** — compared to the average of both values
- **Percent change** in both directions (A → B and B → A)
- **Editable input names** — rename A and B to anything (e.g. "Q1", "Before", "users_count")
- **History tracking** — toggle on to log multiple comparisons in a table
- **Entry labels** — tag each row with a metric name, table, or context note
- **Export** — download history as CSV or JSON
- Works entirely offline, no internet required

---

## Using as a Claude Artifact

You can run this calculator directly inside Claude as a persistent artifact with cross-session storage powered by Claude's built-in storage API.

**To add it to a Claude conversation:**

1. Open [claude.ai](https://claude.ai)
2. Start a new conversation and paste the following prompt:

```
Here is the source of a difference calculator tool. Please render it as an artifact with persistent storage using window.storage so my history is saved between sessions.

[paste the contents of diff_calculator.html here]
```

3. Claude will render it inline — your history will be saved automatically and restored each time you return to that conversation.

**How the storage works:**

When running as a Claude artifact, history is saved via `window.storage` (Claude's artifact storage API) instead of `localStorage`. This means:

- Entries persist across sessions within the same Claude conversation
- Each user's data is scoped to their own account
- Data is not shared between conversations

**Switching between standalone and artifact versions:**

| Context | Storage used | Persists across |
|---|---|---|
| Browser (standalone) | `localStorage` | Browser sessions on same device |
| Claude artifact | `window.storage` | Claude conversations (same account) |
---

## Usage

1. Download `diff_calculator.html`
2. Open it in any browser
3. Enter two numbers — results appear instantly
4. Toggle **Track history** to start logging comparisons
5. Click **+ Add** to save a result, then **↓ CSV** or **↓ JSON** to export


## Potential Use Cases

**Data & Analytics**
- Comparing query results across environments (dev vs prod, two DB replicas)
- Spot-checking metric changes between reporting periods
- Validating ETL outputs — e.g. row counts before and after a pipeline run

**Finance & Business**
- Revenue or cost comparisons across quarters or years
- Budget vs actuals tracking
- Price change analysis between suppliers or time periods

**Engineering & QA**
- Benchmarking performance metrics (latency, throughput, error rates)
- Comparing test results across builds or deployments
- Checking sensor readings or measurement tolerances

**Science & Research**
- Comparing experimental results against a control or baseline
- Calculating measurement error between instruments
- Logging repeated observations over time

**Everyday**
- Comparing prices while shopping
- Tracking progress toward a goal (weight, savings, steps)
- Any quick "how much did this change?" calculation

---

## Notes

History is saved to `localStorage` and persists between browser sessions. Clearing browser data will reset it.
