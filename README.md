Economic Growth and Health System Factors in Global Child Mortality

Author: Collins Audi
Date: 2025-12-04

Background and Purpose

Reducing child mortality before the fifth birthday is a core target of Sustainable Development Goal 3 (Health and Well-being) and is a key indicator of a country’s Human Development Index (HDI). Historically, the Preston Curve showed a strong correlation between per capita income and under-5 mortality: higher income → lower child deaths.

Globally, under-5 mortality decreased from 94 per 1,000 live births in 1990 to 37 per 1,000 in 2023, driven by economic growth and health programs (World Bank, 2023).

However, studies suggest that economic growth alone is insufficient without strategic healthcare investment. Countries with similar income levels can have divergent child survival outcomes, influenced by health system equity, access, and quality (Houweling et al., 2005; Victoria, 2003).

Modern evidence emphasizes healthcare quality as a determinant of child survival, highlighting the importance of Universal Health Coverage (UHC) and health system infrastructure (Kruk et al., 2018; WHO, 2023).

Research Question:

To what extent does health system structural maturity (proxied by income status) moderate the impact of domestic health expenditure on child survival, and do these efficiency gains outweigh vertical interventions like immunization?

Key Variables (per country, 2000–2022):

Under-5 mortality rate
Access to water and sanitation (WASH)
Healthcare expenditure (% of GDP)
GDP per capita (PPP-adjusted)
Under-5 population size

Data Sources:

Our World in Data
UNICEF
World Bank
Step 1: Data Importing, Cleaning, and Preparation
Phase 1: Mortality Data

Steps for preparing UNICEF under-5 mortality data:

Importing the Data: Load the raw CSV and clean column names.
Selecting Median Estimates: Keep the most likely values for mortality.
Reshaping: Pivot data from wide → long format for easier analysis.

Result: A tidy dataset with a yearly mortality timeline per country.

Insert Image Placeholder for Mortality Data Cleaning:
![Mortality Data Cleaning](path/to/image.png)

Phase 2: Health and Economic Indicators

Imported and cleaned datasets:

Immunization (DPT coverage)
Healthcare Expenditure (% of GDP)
GDP per capita
WASH Access
Under-5 Population
Country Income Status

Steps:

Round numeric values for readability
Align data by country and year for merging

Insert Image Placeholder for Dataset Overview:
![Data Overview](path/to/image.png)

Phase 3: Data Merging and Audit

Process:

Merge datasets using iso_code + year
Remove duplicates and incomplete rows
Audit coverage: 177 countries have full 2000–2022 data; 9 partial

Output: merged_data.csv with 186 countries, ready for analysis.

Insert Image Placeholder for Merged Data Audit:
![Merged Data Audit](path/to/image.png)

Step 2: Visualizing Under-5 Mortality vs GDP (Preston Curve)

Objective: Explore the relationship between GDP per capita and under-5 mortality over time.

Method:

Animated bubble chart (Plotly)
Bubble size = Under-5 population
Color = SDG region
Logarithmic axes for GDP and mortality

Key Insights:

Strong negative correlation between GDP and mortality
Logarithmic pattern: small wealth gains in low-income countries → large mortality reductions
Large populations in low-income countries (e.g., India, Bangladesh) carry a disproportionate mortality burden

Insert Image Placeholder for Animated Bubble Chart:
![Preston Curve Animation](path/to/image.gif)

Step 3: Handling Missing Data

Approach:

Missingness patterns visualized via heatmaps
WASH, GDP, and health expenditure missingness associated with higher mortality
Missingness identified as MAR (Missing at Random)
Imputed using MICE (2l.pmm) with predictor variables including mortality, population, income status, and region

Insert Image Placeholder for Missing Data Heatmap:
![Missing Data Heatmap](path/to/image.png)

Step 4: Imputation Validation
Density plots, strip plots, and convergence checks confirm realistic and bounded imputations
Final dataset (final_imputed.csv) ready for regression analysis

Insert Image Placeholder for Imputation Validation Plots:
![Imputation Validation](path/to/image.png)

Step 5: Regression Analysis

Modeling Approach:

Panel dataset: 122 countries, 2000–2022
Outcome: log under-5 mortality
Predictors: log health spending, WASH access, DPT coverage
Income status = proxy for health system structural maturity
Median Quantile Regression with bootstrapped errors
Fixed effects for country-level characteristics

Key Findings:

Spending is more efficient in high-income countries
Low-income countries face an efficiency penalty due to weaker health systems
Immunization coverage and infrastructure are critical drivers of child survival
GDP alone is insufficient without strategic health system investment

Insert Image Placeholder for Regression Results:
![Regression Results](path/to/image.png)
