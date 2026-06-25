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
- **Years available:** 2011, 2014, 2017, 2021, 2024
- **Unit of analysis:** Aggregated country-year-population-segment observation

The raw dataset will not be committed if it is large. Local data files should be stored under `data/raw/`.

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
- [ ] Data cleaned and validated
- [ ] SQL analysis completed
- [ ] Power BI dashboard completed
- [ ] Final findings documented

## Current Progress

The Global Findex 2025 CSV has been downloaded and initially inspected. The dataset appears to be aggregated at a country-year-population-segment level, not individual customer level.

Initial indicator review is complete. The first analysis scope will focus on account ownership, financial institution access, mobile money, digital payments, and inactive accounts.
