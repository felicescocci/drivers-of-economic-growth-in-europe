# The Drivers of Economic Growth in Europe

## Evidence from productivity, investment, education, and R&D

This undergraduate portfolio project uses Python and panel data to study the factors associated with annual **GDP growth** across European countries. Its main analysis examines **labour productivity growth** and **investment**; a supplementary extension adds **education expenditure** and **research-and-development (R&D) expenditure** as measures of human-capital and innovation investment.

The project is intentionally careful about scope. It estimates **associations**, not causal effects, and keeps the original balanced model separate from the smaller education-and-R&D extension.

## Research questions

**Main analysis**

> How are productivity growth and investment associated with economic growth across European countries after accounting for persistent country differences and common annual shocks?

**Supplementary extension**

> How much are productivity growth, investment, education expenditure, and R&D expenditure associated with GDP growth in European countries?

## Data and study scope

The main analysis uses a balanced panel of **41 European countries**, observed annually from **2000 to 2018**. This produces **779 country-year observations**.

| Source | Indicator | Project variable | Unit | Role |
|---|---|---|---:|---|
| World Bank, World Development Indicators | `NY.GDP.MKTP.KD.ZG` | GDP growth | Annual % | Dependent variable |
| World Bank, World Development Indicators | `NE.GDI.TOTL.ZS` | Investment | % of GDP | Main explanatory variable |
| World Bank, Aggregate and Sector Productivity Database | `WB.ASPD.dlpe` | Labour productivity growth | Annual % | Main explanatory variable |
| World Bank, World Development Indicators | `SE.XPD.TOTL.GD.ZS` | Education expenditure | % of GDP | Supplementary explanatory variable |
| World Bank, World Development Indicators | `GB.XPD.RSDV.GD.ZS` | R&D expenditure | % of GDP | Innovation proxy in the extension |

## Headline findings from the main model

The preferred specification is a **two-way fixed-effects model** with country and year fixed effects and country-clustered standard errors.

| Driver | Coefficient | Interpretation |
|---|---:|---|
| Productivity growth | **0.614** | A 1 percentage-point increase is associated with approximately 0.61 percentage points higher GDP growth. |
| Investment (% of GDP) | **0.216** | A 1 percentage-point increase is associated with approximately 0.22 percentage points higher GDP growth. |

Both coefficients are statistically significant in the preferred model. Productivity has the stronger and more stable association with GDP growth. Investment remains positively associated with growth, although its estimated magnitude is more sensitive to unusually large country-specific shocks.

## What the education-and-R&D extension adds

Notebook 05 broadens the economic perspective without replacing the main result. It examines whether education expenditure and R&D expenditure are associated with GDP growth after accounting for productivity growth and investment.

Because the additional indicators are not available for every country-year, the extension is based on a smaller, **unbalanced** complete-case sample. The coverage rows below all start from the same 779-observation core panel; they are not sequential filters.

| Data requirement | Observations available |
|---|---:|
| Original balanced core panel | 779 |
| Core panel with education expenditure observed | 614 |
| Core panel with R&D expenditure observed | 722 |
| Final sample with all five analysis variables observed | **574** |

The final extension sample covers **40 countries** and remains within 2000–2018, but countries contribute different numbers of years. To make the comparison fair, Notebook 05 estimates both its restricted baseline model and its extended model on these **same 574 country-years**. It therefore does not compare an extended 574-observation model directly with the original 779-observation main model.

The extension reports **contemporaneous conditional associations**, not proof that changing education or R&D expenditure would cause GDP growth to change. These variables may have long-run effects, and part of their economic contribution may operate through productivity itself.

## Policy implication

Although the models do not establish a direct or immediate causal effect of education or R&D spending on annual GDP growth, both remain relevant areas for policy. Education can strengthen human capital, while R&D can support innovation, technology adoption, and future productivity. European policymakers can therefore view them as long-term investments that help create conditions for sustainable growth, alongside policies that support productive private investment and efficient resource allocation.

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
│   ├── 04_panel_regression_analysis.ipynb
│   └── 05_extended_growth_model.ipynb
└── data/
    ├── raw/
    │   ├── gdp_growth.csv
    │   ├── investment.csv
    │   ├── education.csv
    │   ├── productivity.xlsx
    │   └── R&D_expenditure.csv
    └── processed/
        ├── europe_panel_collected.csv
        ├── europe_panel_core_cleaned.csv
        └── europe_panel_extended_cleaned.csv
```

## Notebook workflow

1. **Data collection** imports the GDP, investment, education, and productivity sources; selects European economies; reshapes the source tables; and creates a broad 1960–2018 staging panel.
2. **Data cleaning** assesses missingness, selects 2000–2018, validates values, flags rather than deletes potential outliers, and exports the core and extended panels.
3. **Exploratory data analysis** examines distributions, correlations, time patterns, cross-country differences, within-country relationships, and outlier sensitivity.
4. **Panel regression analysis** compares pooled OLS, country fixed effects, and two-way fixed effects; then assesses model fit, multicollinearity, residual behaviour, covariance robustness, and sensitivity to the largest residuals.
5. **Extended growth model** merges education expenditure and R&D expenditure into the cleaned core panel, documents the resulting coverage loss, presents two descriptive charts, and compares two same-sample two-way fixed-effects models.

## How to run the project

Create a Python environment and install the required packages:

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

Place the five raw files shown in the project structure in `data/raw/`. Notebook 05 requires the R&D file; it accepts `R&D_expenditure.csv`, `R-D_expenditure.csv`, or `01-R-D_expenditure.csv`. The first collection notebook also accepts the original downloaded filenames for its four inputs, so renaming those files is optional.

In VS Code, select the `.venv` kernel and run the notebooks in numerical order. Run Notebooks 01 and 02 before Notebook 05 because it depends on their cleaned outputs. If `linearmodels` is missing, run `%pip install linearmodels` in a notebook cell once, restart the kernel, and run the notebook again from the beginning.

## Main analytical choices

- **2000–2018** is selected because earlier decades have weaker coverage and the productivity source ends in 2018.
- The **balanced core panel** is retained for the main model so every one of the 41 countries contributes each year.
- Missing core, education, and R&D values are **not imputed**. The extension instead uses a transparent complete-case sample.
- Potential outliers are retained because recessions and recoveries are economically meaningful events, not automatic data errors.
- **Country fixed effects** control for persistent national characteristics.
- **Year fixed effects** control for shocks shared across Europe in a given year.
- **Country-clustered standard errors** allow regression errors to be correlated within countries over time.
- The two extension regressions use the **same observations**, so changes in coefficients are not silently driven by a change in sample composition.

## Limitations

- The estimates show **associations**, not causal effects; reverse causality and omitted time-varying factors may remain.
- GDP growth may itself influence productivity, investment, education expenditure, and R&D expenditure.
- The education-and-R&D extension has incomplete coverage, so its 574-observation sample is smaller and unbalanced.
- Education and R&D can affect growth over long lags that a contemporaneous annual model does not capture.
- Education and R&D may partly influence growth through productivity, so their coefficients do not measure their full long-run contribution.
- Institutions, trade, demographics, business conditions, sectoral structure, and measurement differences are not fully captured.
- The project ends in 2018 because of productivity-data availability; results apply to the selected European countries and period.

## Portfolio skills demonstrated

- Multi-source data collection, validation, and reshaping
- Panel-data construction and missing-data analysis
- Transparent cleaning and economically informed outlier decisions
- Statistical visualisation and accessible economic interpretation
- Pooled OLS and fixed-effects panel modelling
- Same-sample model comparison and robust inference
- Reproducible project organisation in Python and Jupyter notebooks
- Clear separation between statistical association, causal claims, and policy relevance

## Short project summary

This project studies GDP growth across Europe using a balanced 41-country panel for 2000–2018. Its main fixed-effects analysis finds that stronger productivity growth and higher investment shares are associated with higher GDP growth, with productivity showing the clearest and most stable relationship. A supplementary education-and-R&D extension broadens the economic story using a smaller common sample, while remaining explicit that the evidence is associational and that long-run effects cannot be fully captured by annual contemporaneous data
