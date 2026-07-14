# Project Progress Log

This file records the work completed, concepts learned, decisions made, and problems encountered during the project.

## Day 1 - Repository Setup

**Date:** June 23, 2026

### Work Completed

- Created the local project repository.
- Created folders for data, notebooks, SQL, Power BI, reports, screenshots, and documentation.
- Added a starter README with project objective, dataset source, business questions, tools, and progress checklist.
- Added `.gitignore` rules to keep raw data, processed data, databases, and Power BI files local.

### Decisions Made

- Use World Bank Global Findex data for a financial inclusion analysis project.
- Focus the project on financial access gaps, digital payments, and Nepal/South Asia comparison.
- Keep large raw and processed data files out of GitHub.

### Next Step

Download the Global Findex dataset, inspect the available files, and identify the correct unit of analysis.

---

## Day 2 - Dataset Understanding

**Date:** June 24, 2026

### Work Completed

- Created `01_dataset_understanding.ipynb`.
- Loaded a small sample of the Global Findex 2025 CSV.
- Inspected the dataset shape and column names.
- Loaded core context columns for country, year, region, income group, and population segment.
- Checked available years, groups, regions, and income groups.
- Tested a possible row identifier using `codewb`, `year`, `group`, and `group2`.
- Previewed initial financial inclusion indicators.
- Confirmed Nepal appears in the dataset using country code `NPL`.

### Validation Results

- Rows: 8,577.
- Columns: 438.
- Years available: 2011, 2014, 2017, 2021, 2024.
- Nepal country code: `NPL`.

### Concepts Learned

- The dataset is based on survey data, but the CSV is not customer-level data.
- Each row appears to represent an aggregated country-year-population-segment observation.
- `group` and `group2` are important for understanding population segments.
- A duplicate check across multiple key columns helps test whether a combination can identify rows.
- Indicator columns need definition review before they are used in final analysis.

### Decisions Made

- Treat the dataset as aggregated country/segment-level financial inclusion data.
- Do not clean or transform the dataset yet.
- Review indicator meanings before selecting final analysis columns.

### Next Step

Review the indicator definitions and select the final indicators for the analysis.

---

## Day 3 - Indicator Review and Selection

**Date:** June 25, 2026

### Work Completed

- Continued `01_dataset_understanding.ipynb`.
- Reviewed initial Global Findex candidate indicators.
- Wrote plain-English meanings for key financial inclusion indicators.
- Grouped indicators into themes such as account ownership, mobile money, digital payments, saving, borrowing, and account inactivity.
- Checked missing values for candidate indicators.
- Previewed Nepal rows for selected indicators.
- Selected final context columns for the first analysis scope.
- Selected final indicator columns for the first analysis scope.

### Final Context Columns Selected

- `countrynewwb`
- `codewb`
- `year`
- `pop_adult`
- `regionwb24_hi`
- `incomegroupwb24`
- `group`
- `group2`

### Final Indicator Columns Selected

- `account_t_d`
- `fiaccount_t_d`
- `mobileaccount_t_d`
- `dig_acc`
- `merchant_pay`
- `g20_made`
- `g20_received`
- `inactive_t_d`

### Concepts Learned

- Indicator codes need to be translated into plain-English meanings before analysis.
- Not every available indicator should be included in the first analysis scope.
- Borrowing and saving indicators may be useful later, but they are not central to the first dashboard.
- Candidate indicator missingness should be checked before final cleaning.

### Decisions Made

- Focus the first analysis scope on account ownership, financial institution access, mobile money, digital payments, and inactive accounts.
- Keep borrowing and saving indicators as possible future additions.
- Start a new cleaning notebook next instead of continuing transformations inside the dataset-understanding notebook.

### Next Step

Start `02_data_cleaning.ipynb`, load only the selected columns, rename indicator columns into business-friendly names, check missing values, and prepare a clean analysis dataset.

---

## Day 4 - Initial Data Cleaning and Validation

**Date:** June 27, 2026

### Work Completed

- Created `02_data_cleaning.ipynb`.
- Loaded only the 16 selected context and indicator columns.
- Renamed coded columns into business-friendly analytical names.
- Profiled missing values overall and by survey year.
- Validated the proposed composite key using country code, year, group, and subgroup.
- Confirmed that the composite key contains no missing values or duplicate rows.
- Confirmed that all non-missing indicator values fall between 0 and 1.
- Reviewed categorical values and investigated the additional 2022 survey year.
- Confirmed that 2022 contains data for 16 countries and retained it as a legitimate off-cycle survey period.

### Decisions Made

- Keep indicator values as decimal proportions for downstream SQL and Power BI formatting.
- Do not remove rows or fill missing indicators until their year and segment availability is fully understood.
- Keep the 2022 observations and document their limited country coverage.

### Next Step

Document the final cleaning rules, create the analysis-ready dataset, and validate the processed output before export.

---

## Day 5 - Final Cleaning and Processed Dataset Export

**Date:** June 28, 2026

### Work Completed

- Identified 12 regional, income-group, and global benchmark entities.
- Added `entity_type` to separate country rows from aggregate benchmark rows.
- Added `survey_period_type` to label the limited 2022 observations as an off-cycle survey.
- Standardized text fields by removing leading and trailing spaces.
- Documented why missing indicator values must remain null rather than being replaced with zero.
- Created an ordered analysis-ready table with 8,577 rows and 18 columns.
- Exported the reproducible processed dataset to `data/processed/findex_analysis_ready.csv`.
- Reloaded the exported CSV and confirmed its shape matches the cleaned DataFrame.

### Validation Results

- Missing composite-key values: 0.
- Duplicate composite keys: 0.
- Indicator values outside the valid 0-to-1 range: 0.
- Country rows: 7,893.
- Aggregate benchmark rows: 684.
- Off-cycle 2022 rows: 176.

### Decisions Made

- Retain aggregate benchmark rows for Nepal comparisons, but distinguish them from countries using `entity_type`.
- Retain the 2022 observations and label them as off-cycle survey data.
- Preserve missing indicator values as null because unavailable data is not equivalent to zero usage.
- Keep processed data out of GitHub because it is reproducible from the cleaning notebook.

### Next Step

Begin SQL analysis using the processed dataset and validate the main financial-inclusion comparisons before dashboard development.

---

## Day 6 - SQL Setup and Nepal Trend Analysis

**Date:** June 29, 2026

### Work Completed

- Created `03_sql_analysis.ipynb`.
- Loaded `findex_analysis_ready.csv` into a local SQLite database.
- Created the `findex_clean` SQL table for reproducible query-based analysis.
- Ran initial SQL validation queries for total rows, entity-type distribution, survey-year coverage, and distinct country-code coverage.
- Queried Nepal national overall rows using `country_code = 'NPL'`, `entity_type = 'Country'`, `"group" = 'all'`, and `"group2" = 'all'`.
- Built initial Nepal trend queries for account ownership, digital access, mobile money, and inactive accounts.
- Identified benchmark aggregate codes for future comparison: `SAS`, `LMC`, and `WLD`.

### Concepts Learned

- SQLite provides a lightweight way to practice SQL locally without needing a separate database server.
- Aggregate benchmark rows are not identified through Nepal's `region` or `income_group` values alone; they use their own aggregate `country_code` values.
- SQL filtering must stay explicit to avoid mixing country rows, aggregate rows, and subgroup rows in the same result.
- Reproducible SQL analysis starts with table validation before interpretation.

### Decisions Made

- Use SQLite as the SQL engine for the project.
- Keep benchmark comparisons based on aggregate `country_code` values such as `SAS`, `LMC`, and `WLD`.
- Restrict Nepal trend analysis to the national overall view before moving into subgroup analysis.

### Next Step

Continue the SQL notebook with benchmark comparisons for Nepal versus South Asia, Lower middle income, and world, then move into subgroup gap analysis by gender, age, and income.

---

## Day 7 - Benchmark, Subgroup, and Power BI Summary Exports

**Date:** July 13, 2026

### Work Completed

- Extended `03_sql_analysis.ipynb` with Nepal benchmark comparisons against:
  - South Asia (`SAS`)
  - Lower middle income (`LMC`)
  - world (`WLD`)
- Added subgroup account-ownership analysis for Nepal by gender, age, and income group.
- Added 2024 digital-access subgroup analysis for Nepal.
- Wrote interpretation notes for subgroup account-ownership results and 2024 digital-access results.
- Created compact Power BI-ready summary tables from SQL outputs.
- Exported the summary tables to `data/processed/`:
  - `nepal_benchmark_summary.csv`
  - `nepal_account_subgroup_summary.csv`
  - `nepal_digital_access_2024_summary.csv`

### Key Analytical Findings

- Nepal remains below South Asia, Lower middle income, and world benchmarks on account ownership across the comparison years.
- The gender gap in account ownership narrows sharply and is nearly closed by 2024.
- The age gap becomes the largest account-ownership gap by 2024.
- The income gap remains meaningful, although it improves over time.
- In 2024 digital access, women and poorer groups lag clearly behind men and richer groups.

### Decisions Made

- Use account ownership as the main long-term benchmark and subgroup trend metric.
- Treat digital access as a 2024-focused comparison metric because earlier-year coverage is limited.
- Build the Power BI dashboard from the exported summary tables instead of repeating SQL logic inside Power BI.

### Next Step

Build the Power BI pages using the exported summary tables, capture dashboard screenshots, and document the final portfolio findings.

---

## Day 8 - Power BI Dashboard Build and Screenshot Capture

**Date:** July 14, 2026

### Work Completed

- Built the `Executive Overview` Power BI page with:
  - four KPI cards for Nepal and South Asia 2024 values
  - an account-ownership benchmark trend chart
  - a 2024 digital-access benchmark comparison chart
- Built the `Nepal Account Gaps` page showing account-ownership subgroup trends for:
  - gender
  - age
  - income
- Built the `2024 Digital Access` page showing Nepal's 2024 digital-access gaps for:
  - gender
  - age
  - income
- Saved the Power BI report file to `powerbi/financial_inclusion_gap_analysis.pbix`.
- Captured dashboard screenshots and stored them under `reports/screenshots/`.

### Dashboard Structure

- `Executive Overview`
- `Nepal Account Gaps`
- `2024 Digital Access`

### Key Dashboard Takeaways

- Nepal remains below South Asia, Lower middle income, and world benchmarks in account ownership.
- The gender gap in account ownership narrows strongly and is almost closed by 2024.
- The age gap becomes the largest account-ownership gap by 2024.
- In 2024 digital access, women, poorer groups, and older adults lag behind their comparison groups.

### Decisions Made

- Use benchmark summary tables rather than the full dataset directly inside Power BI.
- Present digital-access comparisons as a 2024-focused page because earlier coverage is limited.
- Keep the dashboard limited to three clear pages instead of expanding the report too early.

### Next Step

Document the final findings in the project README and prepare the final GitHub handoff.

---

## Final Project Status

- Final findings have been documented in the project README.
- SQL analysis, Power BI pages, screenshots, and documentation are complete.
- The remaining operational step is to commit and push the updated documentation and screenshot files to GitHub.

---
