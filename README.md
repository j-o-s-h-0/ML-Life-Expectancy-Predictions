# Life Expectancy Predictions

This project explores which social, economic, and demographic factors most strongly predict average life expectancy in U.S. counties. Using data from sources like the CDC, U.S. Census Bureau, and OpenIntro, the project integrates diverse datasets and builds several machine learning models to predict life expectancy and understand the drivers of health inequality. The models are evaluated and compared, with visuals and metrics highlighting key trends and patterns.


## Table of Contents

- [Goals](#goals)
- [Data Sources](#data-sources)
- [Data Preprocessing](#data-preprocessing)
- [Feature Selection](#feature-selection)
- [Model Training](#model-training)
- [Model Comparison](#model-comparison)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [Credits](#credits)
- [Contact](#contact)


## Goals

- Identify which factors (race, income, education, obesity, health insurance, etc.) are most predictive of lower life expectancy.
- Highlight the role of systemic inequality in health outcomes using statistical modeling.
- Create high-quality visualizations to assist social advocacy and academic research.
- Demonstrate skills in data cleaning, feature engineering, model evaluation, and optimization for data science portfolio development.


## Data Sources

| Source | Description | Link |
|------|-----------|----|
| CDC/NCHS | Life Expectancy by County (2010–2015) | [CDC Link](https://data.cdc.gov/National-Center-for-Health-Statistics/U-S-Life-Expectancy-at-Birth-by-State-and-Census-T/5h56-n989/about_data) |
| OpenIntro | U.S. County Socioeconomic Data (2010s) | [OpenIntro Link](https://www.openintro.org/data/?data=county_complete) |
| U.S. Census Bureau | Population & Race Demographics (2010–2019) | [Census Link](https://www.census.gov/data/tables/time-series/demo/popest/2010s-counties-detail.html) |
| CDC | Adult Obesity Rates (2022) | [CDC Link](https://www.cdc.gov/obesity/data-and-statistics/adult-obesity-prevalence-maps.html) |
| ArcGIS ACS | Health Insurance Coverage (2022) | [ArcGIS Link](https://hub.arcgis.com/datasets/esri::acs-health-insurance-by-age-by-race-variables-centroids/about?layer=1) |
| GitHub - Camillol | Population Density by County (2011) | [GitHub Link](https://github.com/camillol/cs424p3/blob/master/data/Population-Density%20By%20County.csv) |
| Kaggle | U.S. Household Income Statistics (2018) | [Kaggle Link](https://www.kaggle.com/datasets/goldenoakresearch/us-household-income-stats-geo-locations) |


## Data Preprocessing

**Why drop counties with population < 10,000?**
  - Stabilizes estimates (small counties have volatile life expectancy estimates).
  - Reduces noise and risk of model overfitting to rare events.
  - Focuses analysis on more impactful regions for public policy.

**Major preprocessing fixes:**
- Combined multiple census tracts into a single county row by averaging values.
- Cleaned inconsistent state/county naming and encoding issues.
- Dropped rows with missing life expectancy or insurance data.
- Converted raw counts into percentages where appropriate (e.g., race distribution).
- Calculated per capita federal spending.


## Feature Selection

**Selected Features (17 total):**
- Represent diverse and meaningful determinants of health: demographics, economics, access, education.
- Include known predictors of health outcomes such as:
  - Racial demographics (`WAC_pct`, `BA_pct`, etc.)
  - Economic stressors (`Mean income`, `unemployment`, `child_poverty`)
  - Education levels (`hs_grad`, `bachelors`)
  - Access to infrastructure (`broadband`, `Density`)
  - Health indicators (`obesity_prevalence`, `h_insurance_pct`)
  - Gender distribution (`female_pct`)

**Features Removed:**
- Low correlation: Variables not meaningfully related to life expectancy.
- Multicollinearity: Some education/economic variables were redundant and removed to improve interpretability.


## Model Training

- The data was split into training and testing sets using an 80/20 ratio.
- Features were scaled using `StandardScaler`.
- Manual hyperparameter tuning was performed (e.g., `n_estimators=170` for tree-based models).
- Model performance was evaluated using R² and Mean Absolute Error (MAE).


## Model Comparison

| Model                     | R² Score | MAE (Years) | Notes                             |
|----------------------------|----------|-------------|-----------------------------------|
| Linear Regression          | 0.60     | 1.15        | Baseline, interpretable          |
| Random Forest Regressor    | 0.78     | 0.79        | Strong overall                   |
| Extra Trees Regressor      | 0.79     | 0.74        | Best performing model            |
| Gradient Boosting Regressor| 0.76     | 0.87        | Good but slightly slower         |
| Support Vector Regressor   | 0.70     | 0.96        | Decent but underperforms trees   |
| Neural Network (Keras)     | 0.68     | 0.97        | Reasonable but harder to tune    |


## Limitations

- Static model: Does not forecast future changes or use time-series data.
- Aggregated data: County-level stats hide individual-level variation.


## Future Improvements

- Add temporal features (e.g., change in income, obesity rates).
- Use more health-specific variables (e.g., smoking, diabetes rates).
- Explore structured prediction methods (e.g., LSTM, XGBoost).
- Improve regularization and feature selection pipelines.


## Credits

Developed by **Joshua Nelson**.

Data courtesy of CDC/NCHS, U.S. Census Bureau, OpenIntro, Kaggle (Golden Oak Research Group), ArcGIS/ACS, and GitHub (Camillol).

## Contact

Feel free to reach out via [LinkedIn](https://www.linkedin.com/in/joshua-thomas-nelson/) or email me directly at [contact@joshtn.com](mailto:contact@joshtn.com).