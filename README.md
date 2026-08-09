# The Drivers of Economic Growth in Europe

## Evidence from productivity and investment

This undergraduate portfolio project studies how **labour productivity growth** and **investment** are associated with annual **GDP growth** across European countries. The analysis uses Python to build a country–year panel, document data-quality decisions, explore economic patterns, and estimate pooled and fixed-effects regressions.

The final sample is a balanced panel of **41 European countries observed annually from 2000 to 2018**, giving **779 country–year observations**.

## Research question

> How are productivity growth and investment associated with economic growth across European countries after accounting for persistent country differences and common annual shocks?

The project estimates associations rather than causal effects. This distinction is maintained throughout the notebooks.

## Headline findings

The preferred country-and-year fixed-effects model finds that:

| Driver | Coefficient | Interpretation |
|---|---:|---|
| Productivity growth | **0.614** | A 1 percentage-point increase is associated with approximately 0.61 percentage points higher GDP growth |
| Investment (% of GDP) | **0.216** | A 1 percentage-point increase is associated with approximately 0.22 percentage points higher GDP growth |

Both coefficients are statistically significant with country-clustered standard errors and remain significant under the alternative covariance estimators reported in the regression notebook.

Productivity has the stronger and more stable association. Investment remains positive, although its magnitude is more sensitive to unusually large country-specific shocks.

## Data sources

| Source | Indicator | Project variable | Unit | Role |
|---|---|---|---:|---|
| World Bank, World Development Indicators | `NY.GDP.MKTP.KD.ZG` | GDP Growth | Annual % | Dependent variable |
| World Bank, World Development Indicators | `NE.GDI.TOTL.ZS` | Investment | % of GDP | Main explanatory variable |
| World Bank, Aggregate and Sector Productivity Database | `WB.ASPD.dlpe` | Productivity Growth | Annual % | Main explanatory variable |
| World Bank, World Development Indicators | `SE.XPD.TOTL.GD.ZS` | Education Expenditure | % of GDP | Supplementary variable |

Education expenditure is examined descriptively but is not included in the balanced main regression. Its country–year coverage is incomplete, its composition changes over time, and its effects may occur with long lags.

## Project structure

```text
europe-gdp-growth/
├── README.md
├── requirements.txt
├── data_dictionary.md
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_exploratory_data_analysis.ipynb
│   └── 04_panel_regression_analysis.ipynb
└── data/
    ├── raw/
    │   ├── gdp_growth.csv
    │   ├── investment.csv
    │   ├── education.csv
    │   └── productivity.xlsx
    └── processed/
        ├── europe_panel_collected.csv
        ├── europe_panel_core_cleaned.csv
        └── europe_panel_extended_cleaned.csv
```

The collection notebook also accepts the original downloaded filenames listed inside that notebook, so renaming the four raw files is optional.

## Notebook workflow

1. **Data collection** imports the four sources, selects European economies, reshapes the source tables, and creates a broad 1960–2018 staging panel.
2. **Data cleaning** analyses missingness, selects 2000–2018, validates values, flags rather than deletes potential outliers, and exports the core and extended samples.
3. **Exploratory analysis** examines distributions, correlations, time patterns, cross-country differences, within-country relationships, and outlier sensitivity.
4. **Panel regression** compares pooled OLS, country fixed effects, and two-way fixed effects; then checks model fit, multicollinearity, residual behaviour, covariance robustness, and sensitivity to the largest residuals.

## How to run the project

Create a Python environment, install the packages, place the four raw files in `data/raw`, and run the notebooks in numerical order.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

On Windows, activate the environment with:

```powershell
.venv\Scripts\activate
```

In VS Code, select the `.venv` kernel and use **Restart Kernel and Run All Cells** for each notebook.

## Main analytical choices

- **2000–2018** is selected because earlier decades have much weaker coverage and the productivity source ends in 2018.
- The **balanced core panel** keeps the main model comparable across countries and years.
- Missing core variables are not imputed because artificial values could distort economic relationships.
- Potential outliers are retained because major recessions and recoveries are economically meaningful.
- **Country fixed effects** control for persistent country characteristics.
- **Year fixed effects** control for shocks shared across Europe in the same year.
- **Country-clustered standard errors** allow regression errors to remain correlated over time within each country.

## Limitations

- The estimates are contemporaneous associations, not causal effects.
- GDP growth may itself influence productivity and investment, creating reverse causality.
- Time-varying policies, financial conditions, external demand, and measurement differences may remain omitted.
- The sample ends in 2018 because of productivity-data availability.
- Education expenditure is not part of the main regression because its panel is incomplete and its effects may be delayed.
- Results apply to the selected European sample and period rather than to all countries or all years.

## Portfolio skills demonstrated

- Multi-source data collection and reshaping
- Missing-data and panel-balance analysis
- Transparent cleaning and outlier decisions
- Statistical visualisation and economic interpretation
- Pooled OLS and fixed-effects panel modelling
- Robust inference and sensitivity analysis
- Reproducible project organisation
- Clear separation between association and causation

## Short project summary

This project combines four World Bank datasets to study GDP growth across Europe. After building a balanced 41-country panel for 2000–2018, the analysis finds that productivity growth has the strongest positive relationship with GDP growth. Investment is also positively associated with growth, but its magnitude is more sensitive to large shocks. Country and year fixed effects show that these relationships remain after controlling for persistent country differences and shared annual events, although the evidence should not be interpreted causally.
