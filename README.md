# Difference Calculator

A single-file tool for comparing numbers — manually, from CSV files, or via in-file pivot. No dependencies, no build step — open the HTML file in any browser.

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

### Pivot mode
- Compare two groups **within a single file** — like an Excel pivot table
- Pick a **pivot column** whose values define the two sides (e.g. `period`, `source`, `country`)
- Click pills to select **Value A** and **Value B**
- **Multiple metrics at once** — select several metric columns; each becomes its own comparison group with display names auto-filled as `{pivotValue}_{metricName}`
- **Segment drilldown** — when multiple metrics are selected, optionally enable segment breakdown:
  - Each metric shows as a single summary row
  - A **▸ N** expand button reveals inline sub-rows with the full segment breakdown
  - Multiple rows can be expanded simultaneously
- **Aggregation** — sum, average, or first value when multiple rows share the same segment key
- **Pre-filters** — narrow the data before pivoting (AND logic)

### Results table
- **Grouped by metric pair** — when you calculate multiple times with different metrics, each pair gets its own labeled section with a colored group header
- **Column names sub-header** — each group shows the actual A and B column names in indigo/emerald so you always know which value is which
- **Total row** per group — sums A and B across all rows in the group and computes the diff (suppressed for single-row multi-metric groups)
- **Clickable column sort** — click any header (Segment, A, B, |A−B|, Relative %) to sort asc/desc within each group
- **Top N filter** — show only the top 5 / 10 / 20 rows per group

### Export
- **CSV** — wide flat table: one row per segment, one column group per metric pair; includes a TOTAL row at the bottom
- **JSON** — one object per segment with nested keys per metric pair

---

## Using as a Claude Artifact

Run the calculator directly inside Claude as a persistent artifact with cross-session storage.

**To add it to a conversation:**
1. Open [claude.ai](https://claude.ai)
2. Start a new conversation and paste:

```
Here is the source of a difference calculator tool. Please render it as an artifact with persistent storage using window.storage so my history is saved between sessions.
[paste the contents of diff_calculator.html here]
```

3. Claude renders it inline — history is saved automatically and restored each session.

**Storage backends:**

| Context | Storage used | Persists across |
|---|---|---|
| Browser (standalone) | `localStorage` | Browser sessions on same device |
| Claude artifact | `window.storage` | Claude conversations (same account) |

`window.storage` takes priority when available. Otherwise falls back to `localStorage` silently.

---

## Usage

### Manual
1. Download `diff_calculator.html` and open it in any browser
2. Enter two numbers — results appear instantly
3. Toggle **Track history** to start logging comparisons
4. Click **+ Add** to save a result, then **↓ CSV** or **↓ JSON** to export

### From Files
1. Switch to the **⇄ Files** tab
2. Drop or browse for File A and File B (CSV or TSV)
3. Optionally add filters per file via **+ filter**
4. Select segment column(s) for the join key
5. Choose the metric column(s) to compare
6. Optionally add **Metric Overrides** for segments that use a different metric column
7. Click **⚡ Calculate**

### Pivot
1. Switch to the **⊞ Pivot** tab
2. Drop or browse for a single CSV or TSV file
3. Optionally add pre-filters
4. Select the **pivot column** and click two value pills to set A and B
5. Select one or more **metric columns**
6. If a single metric: select segment columns for the row key
7. If multiple metrics: optionally enable **segment drilldown** via the toggle
8. Click **⚡ Calculate**

---

## Potential Use Cases

**Data & Analytics**
- Comparing query results across environments (dev vs prod, two DB replicas)
- Spot-checking metric changes between reporting periods
- Validating ETL outputs — row counts before and after a pipeline run
- Cross-source reconciliation when metric column names differ per source
- Comparing multiple metrics at once across two time periods or environments

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

- History is saved automatically and persists between sessions (`localStorage` standalone, `window.storage` in Claude)
- CSV files with UTF-8 BOM are handled correctly
- Clearing browser data will reset history in standalone mode
- Drilldown sub-rows are not included in CSV/JSON exports — only the summary metric row is exported
