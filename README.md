# Financial Inclusion Gap Analysis

A data analytics project using World Bank Global Findex data to explore financial inclusion, digital banking access, and population-level access gaps.

The goal of this project is to understand how access to financial services differs across countries, regions, gender groups, income groups, and digital-payment adoption levels.

## Project Overview

- Analyse financial account ownership and digital finance access.
- Compare Nepal with South Asia and global benchmarks.
- Identify financial inclusion gaps by gender, income, education, and region.
- Use Python and SQL to clean, validate, and analyse the data.
- Build a Power BI dashboard to communicate the main insights.
- Document the full workflow for portfolio and internship use.

## Dataset

- **Dataset:** World Bank Global Findex Database
- **Source:** World Bank
- **Theme:** Financial inclusion, account ownership, digital payments, saving, borrowing, and financial resilience
- **Rows:** 8,577
- **Columns:** 438
- **Years available:** 2011, 2014, 2017, 2021, 2022, 2024
- **Survey-period note:** 2022 is an off-cycle survey period covering 16 countries
- **Unit of analysis:** Aggregated country-year-population-segment observation

Raw and processed data files are kept local and excluded from GitHub. The processed dataset can be reproduced by running the cleaning notebook.

## Initial Business Questions

- How does Nepal compare with South Asia and global averages in account ownership?
- Is there a gender gap in access to financial accounts?
- Are digital payments and mobile money improving financial inclusion?
- Which groups remain underserved?
- How do income level, education, region, and gender relate to financial access?

## Tools

- Python
- Pandas
- SQL and SQLite
- Power BI
- Git and GitHub

## Repository Structure

```text
financial-inclusion-gap-analysis/
|-- data/
|   |-- raw/
|   `-- processed/
|-- docs/
|-- notebooks/
|-- powerbi/
|-- reports/
|   `-- screenshots/
|-- sql/
|-- .gitignore
`-- README.md
```

## Progress

- [x] Repository initialized
- [x] Dataset downloaded and inspected
- [x] Data dictionary reviewed
- [x] Key indicators selected
- [x] Data cleaned and validated
- [ ] SQL analysis completed
- [ ] Power BI dashboard completed
- [ ] Final findings documented

## Current Progress

Dataset understanding, indicator selection, cleaning, and SQL analysis are substantially complete. The analysis-ready dataset contains 8,577 rows and 18 columns covering account ownership, financial institution access, mobile money, digital payments, and inactive accounts.

Country observations are separated from regional, income-group, and global aggregates. Missing indicators remain null because availability differs by survey year and population segment.

The SQL phase in `03_sql_analysis.ipynb` now includes Nepal trend analysis, benchmark comparisons against `SAS`, `LMC`, and `WLD`, subgroup account-ownership analysis, and 2024 digital-access subgroup analysis. Power BI-ready summary exports have also been created:

- `nepal_benchmark_summary.csv`
- `nepal_account_subgroup_summary.csv`
- `nepal_digital_access_2024_summary.csv`

The next step is to build the Power BI dashboard pages from these summary tables and document the final findings.
