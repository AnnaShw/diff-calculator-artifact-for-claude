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

## Usage

1. Download `diff_calculator.html`
2. Open it in any browser
3. Enter two numbers — results appear instantly
4. Toggle **Track history** to start logging comparisons
5. Click **+ Add** to save a result, then **↓ CSV** or **↓ JSON** to export

## Live Demo

Hosted via GitHub Pages: `https://yourusername.github.io/diff-calculator`

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
