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
