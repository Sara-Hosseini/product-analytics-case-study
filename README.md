# Product Analytics Case Study
## User Retention, Funnel Analytics, Feature Adoption & A/B Testing

An end-to-end product analytics portfolio project built around a fictional European mobility platform.

The project demonstrates how behavioural event data can be transformed into decision-ready product insights using **Python, SQL, SQLite, statistical testing, and automated data-quality validation**.

The analysis focuses on:

- user activation and conversion
- product funnel performance and drop-off
- Day 1, Day 7, and Day 30 retention
- monthly cohort behaviour
- feature adoption
- customer segmentation
- A/B test evaluation
- management-ready business recommendations

> All datasets are synthetic and contain no personally identifiable information.

---

## Project Snapshot

| Metric | Result |
|---|---:|
| Users | 5,000 |
| Behavioural events | 141,813 |
| Completed bookings | 2,731 |
| Total simulated revenue | €39,589.80 |
| Data period | January 2024 – June 2025 |
| Automated validation checks | 23 passed |
| Pytest data-quality tests | 25 passed |
| Control conversion rate | 26.9% |
| Treatment conversion rate | 30.5% |
| Experiment uplift | +3.6 percentage points |

---

## Business Problem

The fictional mobility platform wants to understand:

1. Where users abandon the signup-to-booking funnel.
2. Which acquisition channels and platforms produce the strongest users.
3. Whether engagement features are associated with better retention and conversion.
4. How user behaviour changes across signup cohorts.
5. Whether a simplified booking flow improves conversion.
6. Which product actions should be prioritised by management.

---

## Key Findings

### Acquisition quality

Referral was the strongest acquisition channel:

- approximately **40.0% conversion**
- approximately **10.9% activation within seven days**

Paid Search performed substantially lower:

- approximately **23.5% conversion**
- approximately **5.0% activation**

This suggests that acquisition volume should not be evaluated without downstream user quality.

### Platform performance

iOS users had the highest conversion rate at approximately **30.0%**, followed by Android at **28.8%** and Web at **24.0%**.

The Web booking journey should therefore be investigated for product or usability friction.

### Feature adoption

Users who enabled notifications or added a favourite location showed slightly longer average engagement duration.

These findings indicate association rather than proven causation and should be validated through controlled experiments.

### Experiment performance

The `simplified_booking_flow` treatment increased conversion from approximately **26.9% to 30.5%**, an absolute uplift of around **3.6 percentage points**.

The experiment analysis includes conversion, revenue, uplift, confidence intervals, and statistical significance checks.

---

## Business Recommendations

1. Investigate the Web booking journey and prioritise the highest-friction funnel step.
2. Scale referral acquisition while monitoring cost and user quality.
3. Review Paid Search targeting, landing experience, and campaign economics.
4. Test contextual prompts for notification enablement and favourite-location adoption.
5. Continue evaluating the simplified booking flow before full rollout.
6. Monitor results by platform and acquisition channel to detect heterogeneous experiment effects.

Detailed findings are available in:

[`insights/phase2_summary.md`](insights/phase2_summary.md)

---

## Technical Stack

- **Python:** synthetic data generation, validation and database loading
- **SQL / SQLite:** KPI analysis, funnels, cohorts, retention, segmentation and experimentation
- **Pandas / NumPy:** data generation and processing
- **Pytest:** automated data-quality tests
- **Power BI:** dashboard planned
- **Git / GitHub:** version control and project documentation

---

## Repository Structure

```text
product-analytics-retention/
├── README.md
├── requirements.txt
├── data/
│   ├── raw/
│   │   ├── users.csv
│   │   ├── events.csv
│   │   └── experiments.csv
│   ├── processed/
│   └── README.md
├── src/
│   ├── config.py
│   ├── generate_data.py
│   ├── validate_data.py
│   ├── build_database.py
│   └── run_sql.py
├── sql/
│   ├── 00_schema.sql
│   ├── 01_data_quality.sql
│   ├── 02_business_overview.sql
│   ├── 03_kpi_dashboard.sql
│   ├── 04_funnel_analysis.sql
│   ├── 05_retention.sql
│   ├── 06_cohort_analysis.sql
│   ├── 07_feature_adoption.sql
│   ├── 08_segmentation.sql
│   ├── 09_ab_testing.sql
│   └── 10_business_recommendations.sql
├── insights/
│   └── phase2_summary.md
├── notebooks/
├── dashboard/
├── images/
└── tests/
    └── test_data_quality.py
```

---

## Future Improvements

- Interactive Power BI dashboard
- Python exploratory data analysis
- Executive presentation
- Product analytics blog article