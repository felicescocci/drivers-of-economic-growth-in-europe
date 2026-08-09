# Data Dictionary

## Identifiers

| Variable | Type | Description |
|---|---|---|
| `Country Code` | Text | ISO3-style country code used to merge and index the datasets |
| `Country Name` | Text | World Bank country or economy name |
| `Year` | Integer | Calendar year |

## Economic variables

| Variable | Type | Unit | Source indicator | Description |
|---|---|---:|---|---|
| `GDP Growth` | Numeric | Annual % | `NY.GDP.MKTP.KD.ZG` | Annual percentage growth rate of GDP at market prices based on constant local currency |
| `Investment` | Numeric | % of GDP | `NE.GDI.TOTL.ZS` | Gross capital formation as a share of GDP |
| `Productivity Growth` | Numeric | Annual % | `WB.ASPD.dlpe` | Annual labour productivity growth rate |
| `Education Expenditure` | Numeric | % of GDP | `SE.XPD.TOTL.GD.ZS` | Total government expenditure on education as a share of GDP |
| `Potential_Outlier` | Boolean | True/False | Created during cleaning | Marks a country–year with at least one core variable outside the pooled 1.5×IQR bounds; values are retained |

## Processed datasets

| File | Rows | Countries | Period | Use |
|---|---:|---:|---:|---|
| `europe_panel_collected.csv` | 2,714 | 46 | 1960–2018 | Broad staging panel with missing observations retained |
| `europe_panel_core_cleaned.csv` | 779 | 41 | 2000–2018 | Balanced main sample for EDA and regression |
| `europe_panel_extended_cleaned.csv` | 614 | 40 | 2000–2018 | Unbalanced complete-case sample including education expenditure |

## Interpretation notes

- GDP growth and productivity growth are percentage **rates**.
- Investment and education expenditure are percentage **shares of GDP**.
- A one-unit regression change therefore means one percentage point, not a 1% proportional change.
- The `Potential_Outlier` flag is diagnostic. It does not identify errors and is not used to remove observations from the main sample.
- Education expenditure should be interpreted cautiously because country coverage changes over time and economic effects may occur with a lag.
