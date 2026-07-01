# 📊 Marketing Campaign Data Cleaning using Python & Pandas

![Python](https://img.shields.io/badge/Python-3.12-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Cleaning-green)
![NumPy](https://img.shields.io/badge/NumPy-Analysis-orange)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-red)

Transforming messy marketing campaign data into a clean, analysis-ready dataset through a structured data cleaning pipeline.

## 1. Problem

The raw dataset (2,020 rows, 12 columns) simulated common real-world data quality issues:

- Duplicate records
- Missing values in `channel` and `conversions`
- Inconsistent category labels (e.g. `Gogle`, `Tik_Tok`, `Facebok`, `E-mail`)
- Mixed boolean formats (`Y`/`N`, `1`/`0`, `TRUE`/`FALSE`)
- Currency-formatted numeric fields (e.g. `$102.82`)
- Date fields stored as text, with some campaigns showing an end date before the start date
- A logically invalid extra column (`Clicks2`) with 1,980 missing values
- Extreme outliers in campaign spend

## 2. Tools

Python, Pandas, NumPy, Jupyter Notebook

## 3. Approach

Each cleaning step was validated with a before/after check rather than assumed to have worked, and every fix followed an explicit rule rather than a blanket drop or fill.

1. **Duplicate check** — identified and removed 19 exact duplicate rows
2. **Missing values** — dropped the unusable `Clicks2` column, filled missing `channel` as `Unknown`, filled missing `conversions` with `0`
3. **Header cleaning** — standardized column names to lowercase snake_case
4. **Type conversion** — stripped currency symbols from `spend` and converted to numeric
5. **Category standardization** — mapped inconsistent channel labels to a single canonical set
6. **Boolean normalization** — mapped mixed `active` values to proper `True`/`False`
7. **Date parsing** — converted `start_date` and `end_date` from text to `datetime64`
8. **Logical integrity checks**:
   - Flagged campaigns where `clicks` exceeded `impressions` (none found)
   - Flagged campaigns where `end_date` preceded `start_date`, and corrected them using a 30-day campaign duration assumption
9. **Outlier handling** — capped extreme `spend` values above the IQR upper bound (3×IQR, to preserve legitimate high spenders while correcting clear data errors)
10. **Final validation report** — confirmed 0 missing values and 0 duplicate rows before export

## 4. Result

| Metric | Before | After |
|---|---|---|
| Rows | 2,020 | 1,669 |
| Missing values | 322 | 0 |
| Duplicate rows | 19 | 0 |
| Inconsistent channel labels | 11 unique | 6 unique |

The cleaned dataset is exported to `data/cleaned/marketing_campaign_cleaned.csv`, ready for analysis or dashboarding (e.g. Power BI, Tableau).


## Author

**Shayan Mukherjee**
