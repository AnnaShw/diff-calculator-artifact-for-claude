# Difference Calculator

A lightweight, single-file tool for comparing numbers — manually or from CSV files. No dependencies, no build step — just open the HTML file in a browser.

## Features

### Manual mode
- **Absolute difference** — `|A − B|`
- **Relative difference** — compared to the average of both values
- **Percent change** in both directions (A → B and B → A)
- **Editable input names** — rename A and B to anything (e.g. "Q1", "Before", "users_count")
- **History tracking** — toggle on to log multiple comparisons in a table
- **Entry labels** — tag each row with a metric name, table, or context note
- **Export** — download history as CSV or JSON

### File mode (CSV/TSV)
- Load two CSV or TSV files and compare them row-by-row
- **Multi-column filters** — add any number of column+values filter rows per file (AND logic between rows)
- **Segment columns** — select one or more columns as the join key; multiple columns are concatenated with `_`
- **Metric overrides** — assign a different metric column to specific segments using glob patterns:
  - `*_RTB` — matches all segments ending in `_RTB`
  - `mobile_*` — matches all segments starting with `mobile_`
  - `*banner*` — matches segments containing `banner`
  - `exact_value` — exact match
  - Live match count shown as you type
- **Same or different metric columns** per file
- **Custom display names** for File A and File B values

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

The tool automatically picks the best available storage backend:

| Context | Storage used | Persists across |
|---|---|---|
| Browser (standalone) | `localStorage` | Browser sessions on same device |
| Claude artifact | `window.storage` | Claude conversations (same account) |

When `window.storage` is available (inside Claude), it takes priority. Otherwise the tool falls back to `localStorage` silently — no configuration needed.

---

## Usage

### Manual
1. Download `diff_calculator.html`
2. Open it in any browser
3. Enter two numbers — results appear instantly
4. Toggle **Track history** to start logging comparisons
5. Click **+ Add** to save a result, then **↓ CSV** or **↓ JSON** to export

### From Files
1. Switch to the **📂 From Files** tab
2. Drop or browse for File A and File B (CSV or TSV)
3. Optionally add filters per file via **+ Add filter**
4. Select segment column(s) for the join key
5. Choose the metric column(s) to compare
6. Optionally add **Metric Overrides** for segments that use a different metric
7. Click **⚡ Calculate**

---

## Potential Use Cases

**Data & Analytics**
- Comparing query results across environments (dev vs prod, two DB replicas)
- Spot-checking metric changes between reporting periods
- Validating ETL outputs — e.g. row counts before and after a pipeline run
- Cross-source reconciliation with different metric column names per source

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

- History is saved automatically and persists between sessions (via `localStorage` in standalone mode, `window.storage` in Claude)
- CSV files with UTF-8 BOM are handled correctly
- Scientific notation values (e.g. `3.07E+07`) are parsed correctly
- Clearing browser data will reset history in standalone mode
