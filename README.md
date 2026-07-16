# Product Analytics Case Study: User Retention, Feature Adoption, Conversion and Experiment Analysis

## Project overview

An end-to-end product analytics portfolio project built around a fictional
European mobility app. It simulates realistic user, behavioural-event, and
A/B test data, and will progressively build up the kind of analysis a
Product Data Analyst / Data Analyst / Business Analyst / BI Analyst is
expected to deliver: activation and retention analysis, funnel analysis,
cohort analysis, experiment evaluation, and an executive-facing dashboard.

This project is designed to demonstrate analytics engineering and product
analytics skills relevant to European tech companies such as FREE NOW,
Zalando, Delivery Hero, and HelloFresh.

## Business scenario

A fictional European mobility app wants to understand which user
behaviours, acquisition channels, platforms, and product features are
associated with **activation**, **retention**, **conversion**, and
**churn** — and whether a recent product change (a simplified booking
flow, tested via A/B experiment) improves conversion.

## Current phase

**Phase 1 — Data foundation (complete).** Repository structure, synthetic
datasets, data dictionary, and automated data-quality validation.

**Phase 2 — SQL analytics layer (complete).** A SQLite database built from
the Phase 1 CSVs, and ten SQL analysis scripts covering data quality,
business KPIs, funnel analysis, retention, cohort analysis, feature
adoption, segmentation, and A/B test evaluation. Findings and business
recommendations are written up in `insights/phase2_summary.md`.

**No Python exploratory analysis, dashboard, or further phases have been
built yet** — that begins in Phase 3.

## Repository structure

```
product-analytics-retention/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── raw/              # generated CSV datasets (users, events, experiments)
│   ├── processed/        # analytics.db (SQLite database built from data/raw/)
│   └── README.md         # full data dictionary
├── src/
│   ├── __init__.py
│   ├── generate_data.py    # synthetic data generator
│   ├── validate_data.py    # data quality validation report
│   ├── config.py           # generation parameters (seed, volumes, dates, paths)
│   ├── build_database.py   # loads data/raw/*.csv into data/processed/analytics.db
│   └── run_sql.py          # runs a .sql file against the database and prints results
├── sql/
│   ├── 00_schema.sql                  # DDL: tables + indexes
│   ├── 01_data_quality.sql            # SQL-side data quality checks
│   ├── 02_business_overview.sql       # headline business snapshot
│   ├── 03_kpi_dashboard.sql           # DAU/WAU/MAU, activation, conversion, revenue KPIs
│   ├── 04_funnel_analysis.sql         # signup -> search -> booking funnel, drop-off, abandonment
│   ├── 05_retention.sql               # Day 1/7/30 retention by segment, churn
│   ├── 06_cohort_analysis.sql         # monthly cohorts, retention heatmap source table
│   ├── 07_feature_adoption.sql        # notification/favourite/promo adoption vs retention
│   ├── 08_segmentation.sql            # country/platform/age/channel/revenue-tier segments
│   ├── 09_ab_testing.sql              # simplified_booking_flow: uplift + significance tests
│   └── 10_business_recommendations.sql # management-ready rollup tables
├── notebooks/            # reserved for exploratory analysis (Phase 3)
├── dashboard/            # reserved for Power BI dashboard (Phase 7)
├── images/               # reserved for exported charts/screenshots
├── insights/
│   └── phase2_summary.md # Phase 2 findings, KPIs, trends, and recommendations
└── tests/
    └── test_data_quality.py
```

## How to install

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install -r requirements.txt
```

## How to generate data

```bash
python src/generate_data.py
```

This creates `data/raw/users.csv`, `data/raw/events.csv`, and
`data/raw/experiments.csv`, and prints a generation summary (row counts,
date ranges, conversion rates by experiment group). Generation is
deterministic (fixed random seed in `src/config.py`).

## How to validate data

```bash
python src/validate_data.py
```

Runs structural and business-logic checks (schema, duplicate keys, orphan
foreign keys, revenue rules, category domains, funnel ordering, experiment
consistency, null rates, date ranges) and prints a pass/warning/fail
report. Exits with a non-zero status if any critical check fails.

Run the automated test suite with:

```bash
pytest tests/
```

## How to build the SQL database

```bash
python src/build_database.py
```

Loads `data/raw/*.csv` into a fresh SQLite database at
`data/processed/analytics.db`, using the schema defined in
`sql/00_schema.sql`. Re-run this any time the raw CSVs change.

## How to run the SQL analysis

Each file in `sql/` is a standalone, runnable script (multiple queries,
each with a comment explaining the business question it answers). Run any
of them against the database and print the results with:

```bash
python src/run_sql.py sql/03_kpi_dashboard.sql
python src/run_sql.py sql/09_ab_testing.sql --max-rows 30
```

Or open `data/processed/analytics.db` directly in any SQLite client
(e.g. DB Browser for SQLite, the `sqlite3` CLI, or a VS Code SQLite
extension) and run the `.sql` files from there.

## Next planned phases

1. Python exploratory analysis
2. Retention and cohort analysis (Python/pandas deep dive)
3. Funnel analysis (Python/pandas deep dive)
4. A/B test evaluation (Python/pandas deep dive)
5. Power BI dashboard
6. Business recommendations (final write-up)
