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

### 8.1 Occupations with the Largest Employment Increases

Home health and personal care aides in services for the elderly and persons with disabilities recorded the largest selected occupation–industry increase.

| Occupation | Industry | Employment Increase (Thousands) |
|---|---|---:|
| Home health and personal care aides | Services for the elderly and persons with disabilities | 533.3 |
| Home health and personal care aides | Home healthcare services | 202.9 |
| Stockers and order fillers | General merchandise retailers | 116.1 |
| Stockers and order fillers | Grocery and specialty food retailers | 112.6 |
| Cooks, restaurant | Full-service restaurants | 93.0 |
| Software developers | Computer systems design and related services | 72.6 |
| Electricians | Electrical contractors and other wiring installation contractors | 62.2 |
| Registered nurses | General medical and surgical hospitals; private | 62.0 |
| Nurse practitioners | Offices of physicians | 58.7 |
| Medical assistants | Offices of physicians | 58.0 |

### 8.2 Highest Reported Percentage Growth

Data scientists in solar electric power generation recorded the highest reported percentage growth among the selected detailed records.

| Occupation | Reported Growth |
|---|---:|
| Data scientists | 218.4% |
| Logisticians | 185.3% |
| Mechanical engineers | 175.1% |

High percentage growth should be considered alongside the absolute number of jobs added.

### 8.3 Industries with Significant Employment Increases

The following industries recorded the largest summed employment increases across detailed records.

| Industry | Summed Employment Increase (Thousands) |
|---|---:|
| Services for the elderly and persons with disabilities | 623.8 |
| Home healthcare services | 335.4 |
| Computer systems design and related services | 310.6 |

These figures are sums of detailed records and are not verified official BLS industry totals.

### 8.4 Employment Declines

The analysis also identified occupation–industry combinations with projected employment declines.

Cashiers in grocery and specialty food retailers recorded the largest decline among the ten selected losses.

### 8.5 Employment Change Distribution

Most detailed occupation–industry employment changes were concentrated close to zero, with a positively skewed distribution and a longer tail toward larger increases. Some records also showed projected declines.

### 8.6 Employment Size and Projected Change

The bubble chart displayed 33,711 records after applying a central 98% filter for visual clarity. A further 763 extreme records were excluded from this chart only, not from the cleaned dataset.

### 8.7 Employment Relationships

The correlation analysis showed that employment levels in 2025 and 2035 were very strongly correlated. Absolute employment change had moderate positive relationships with employment size, while reported percentage growth had very weak correlations with the other indicators.

## 9. Recommendations

- Interpret employment growth using both absolute job change and percentage change.
- Give attention to care-related occupations and services when examining projected workforce demand.
- Consider technology, engineering, logistics and professional occupations when exploring areas of percentage growth.
- Use detailed occupation–industry records for specific comparisons and clearly label aggregate or summed results.
- Retain extreme observations unless there is evidence that they are data errors.
- Compare projections with future realised employment data as those observations become available.

## 10. Conclusion

The project examined projected U.S. employment patterns from 2025 to 2035 using the BLS National Employment Matrix.

The analysis identified substantial projected increases in care-related services and notable growth in selected technology, retail, healthcare and professional occupation–industry combinations. It also identified records with projected employment declines, demonstrating that workforce demand is not expected to change uniformly across all occupations and industries.

The findings highlight the importance of examining employment levels, absolute changes and percentage growth together. The largest percentage increase does not necessarily correspond to the largest number of additional jobs.

Overall, the project demonstrates how data cleaning, exploratory analysis and visualisation can transform a large employment dataset into meaningful insights about future workforce demand.

## 11. Limitations

- Employment projections are estimates and may differ from future actual employment.
- Employment estimates are rounded to one decimal place in thousands, which can produce small differences when recalculating changes.
- Industry-level totals calculated by summing detailed records may differ from official summary totals because of rounding and suppression.
- IQR identifies statistical extremes but does not determine whether a record is erroneous.
- Central 98% filters used in selected charts omit extreme records from those particular visualisations only.
- Correlation results describe relationships and do not establish causal relationships.

## 12. Future Scope

- Compare projected employment with subsequent actual employment data.
- Extend the analysis to additional projection years when updated BLS matrices become available.
- Investigate selected occupations and industries in greater detail.
- Explore regional or state-level employment patterns if suitable data are available.
- Examine additional factors associated with workforce demand.

