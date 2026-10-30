
# Workforce Demand and Employment Growth Analysis (2025–2035)

### Using the U.S. National Employment Matrix

## 1. Project Overview

This project analyses projected employment patterns across occupations and industries in the United States using the U.S. Bureau of Labor Statistics (BLS) National Employment Matrix.

The analysis compares estimated employment in 2025 with projected employment in 2035 to identify occupations and industries expected to experience significant employment growth or decline. It also examines employment distributions, percentage growth and relationships between employment indicators.

**Dataset Source:** [U.S. Bureau of Labor Statistics – Occupational Employment Projections Data](https://www.bls.gov/emp/data/occupational-data.htm)

## 2. Project Objectives

- Prepare and validate the BLS National Employment Matrix for analysis.
- Examine the structure and quality of the original dataset.
- Identify potential statistical outliers and assess them without automatically removing genuine extreme observations.
- Compare projected employment levels for 2025 and 2035.
- Identify occupation–industry combinations with the largest absolute increases and declines.
- Examine records with the highest reported percentage growth.
- Summarise employment changes across industries using detailed records.
- Explore distributions and relationships among employment indicators through visualisations.

## 3. Dataset Description

The dataset was obtained from the U.S. Bureau of Labor Statistics (BLS), Employment Projections programme.

The original workbook, `matrix.xlsx`, includes a Field Descriptions worksheet. Employment estimates are expressed in thousands and published to one decimal place.

### Dataset Summary

| Dataset Characteristic | Details |
|---|---:|
| Original records | 113,898 rows |
| Original columns | 14 |
| Final cleaned dataset | 113,898 rows × 16 columns |
| Detailed analysis subset | 34,474 rows × 16 columns |
| Projection period | 2025–2035 |
| Main record types | Summary and Line item |
| Employment unit | Thousands of jobs |

### Important Variables

| Column | Description |
|---|---|
| `occupation_code` / `occupation_title` | Occupation identifier and name |
| `industry_code` / `industry_title` | Industry identifier and name |
| `occupation_type` / `industry_type` | Indicates Summary or Line item classification |
| `2025_employment` | Employment estimate for 2025 |
| `2035_employment` | Projected employment for 2035 |
| `numeric_change_202535` | Source-reported numerical employment change |
| `percent_change_202535` | Source-reported percentage employment change |
| `calculated_employment_change` | Independently calculated employment change |
| `change_difference` | Difference between reported and calculated employment change |

## 4. Tools and Technologies

| Tool / Library | Purpose |
|---|---|
| Python | Data processing and analysis |
| Google Colab | Development environment |
| Pandas | Data cleaning, filtering and manipulation |
| NumPy | Numerical calculations and validation |
| Matplotlib | Static data visualisation |
| Seaborn | Statistical visualisation |
| Plotly Express / Graph Objects | Interactive visualisations |
| Microsoft Excel | Dataset inspection and export |

## 5. Data Cleaning and Preprocessing

The original dataset was preserved in `df_raw`, while `df_clean` was created as the working dataset.

The following preprocessing activities were performed:

- Standardised column names into lowercase snake_case.
- Removed leading and trailing whitespace from text columns.
- Checked missing values across all columns. No missing values were detected.
- Checked complete duplicate records. No complete duplicates were identified.
- Retained Summary and Line item classifications because they represent different levels of detail.
- Checked employment estimates for negative values. None were identified.
- Checked percentage distribution columns for values outside the 0–100 range.
- Checked for infinite numerical values. None were identified.
- Created two derived columns: `calculated_employment_change` and `change_difference`.
- Checked occupation and industry codes for missing, blank and whitespace-affected values.

The dataset contained 1,112 unique occupation codes and 423 unique industry codes.

### IQR-Based Outlier Assessment

The Interquartile Range (IQR) method was applied to the full cleaned dataset.

| Variable | Potential Outliers |
|---|---:|
| 2025 Employment | 17,912 |
| 2035 Employment | 17,913 |
| Numerical Employment Change | 30,649 |
| Percentage Employment Change | 7,886 |

These observations were treated as potential statistical outliers rather than confirmed errors.

The extreme values were retained because the dataset contains both aggregate summary records and detailed occupation–industry records. Large employment totals and changes can be expected for broad categories, while high percentage growth can occur when starting employment levels are relatively small.

### Validation of Source-Reported Changes

Source-reported numerical employment changes were compared with independently calculated changes.

- Maximum absolute difference: approximately 0.1 thousand.
- Records differing by more than 0.01 thousand: 22,982.
- Published employment estimates are rounded to one decimal place.

The original BLS-reported numerical and percentage changes were retained to preserve the source values.

## 6. Exploratory Data Analysis (EDA)

### Record Classification

The original dataset contains Summary and Line item records for both occupations and industries.

A separate detailed subset was created by retaining records where both `occupation_type` and `industry_type` were classified as `Line item`.

| Dataset | Records | Description |
|---|---:|---|
| `df_clean` | 113,898 | Complete cleaned dataset |
| `df_detailed` | 34,474 | Detailed occupation–industry records |

The original dataset was retained for broader analysis, while the detailed subset was used for the main occupation–industry rankings and visualisations.

### Employment Change Range

| Indicator | Minimum | Maximum |
|---|---:|---:|
| Numerical employment change | −772.4 thousand | 5,917.6 thousand |
| Percentage employment change | −68.3% | 218.4% |

Negative values were retained because they represent projected employment declines rather than necessarily invalid data.

### Correlation Analysis

The correlation matrix examined the relationship between four employment indicators.

| Employment Indicators | 2025 Employment | 2035 Employment | Numerical Change | Percentage Change |
|---|---:|---:|---:|---:|
| 2025 Employment | 1.00 | 1.00 | 0.57 | 0.01 |
| 2035 Employment | 1.00 | 1.00 | 0.64 | 0.02 |
| Numerical Change | 0.57 | 0.64 | 1.00 | 0.08 |
| Percentage Change | 0.01 | 0.02 | 0.08 | 1.00 |

**Interpretation:**

- 2025 and 2035 employment levels have a very strong positive correlation.
- Numerical employment change has moderate positive correlations with both employment levels.
- Percentage growth has very weak correlations with the other employment indicators.

Correlation describes association and does not establish causation.

## 7. Data Visualisation

Eight visualisations were developed to communicate the main employment patterns.

| No. | Visualisation | Analytical Purpose |
|---:|---|---|
| 1 | Horizontal Bar Chart | Identifies the top 10 occupation–industry combinations by employment increase. |
| 2 | Scatter Plot | Highlights the top 10 detailed records by reported percentage growth. |
| 3 | Treemap | Compares the 15 industries with the largest summed employment increases. |
| 4 | Diverging Bar Chart | Compares the largest projected employment gains and declines. |
| 5 | Correlation Heatmap | Examines relationships between employment indicators. |
| 6 | Histogram | Displays the distribution of projected employment changes. |
| 7 | Bubble Chart | Explores employment size, numerical change and percentage growth. |
| 8 | Dumbbell Chart | Compares 2025 and 2035 employment for selected occupation–industry combinations. |

## 8. Key Findings and Insights
