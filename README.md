# **Economic Growth and Health System Factors in Global Child Mortality**

**Author:** Collins Audi  
**Date:** 2025-12-04  

---

### **Background and Purpose**

Reducing child mortality before the fifth birthday is a core target of **Sustainable Development Goal 3** (Health and Well-being) and a key indicator of a country’s **Human Development Index (HDI)**. Historically, the **Preston Curve** showed a strong correlation between per capita income and under-5 mortality: higher income → lower child deaths.

Globally, under-5 mortality decreased from 94 per 1,000 live births in 1990 to 37 per 1,000 in 2023, driven by economic growth and health programs (World Bank, 2023). However, studies suggest that economic growth alone is insufficient without strategic healthcare investment. Countries with similar income levels can have divergent child survival outcomes, influenced by health system equity, access, and quality.

---

### **Research Question**

To what extent does health system structural maturity (proxied by income status) moderate the impact of domestic health expenditure on child survival, and do these efficiency gains outweigh vertical interventions like immunization?

---

### **Key Variables (2000–2022)**

* **Under-5 Mortality Rate:** Primary outcome variable.
* **Access to Water and Sanitation (WASH):** Infrastructure indicator.
* **Healthcare Expenditure:** Measured as a % of GDP.
* **GDP per Capita:** PPP-adjusted economic status.
* **Under-5 Population Size:** Demographic weight.

**Data Sources:** Our World in Data, UNICEF, and The World Bank.

---

### **Step 1: Data Importing, Cleaning, and Preparation**

#### **Phase 1: Mortality Data**
1.  **Importing:** Loaded raw UNICEF CSV and cleaned column names.
2.  **Selecting:** Kept median estimates for mortality values.
3.  **Reshaping:** Pivoted data from wide to long format for time-series analysis.

![Mortality Data Cleaning](path/to/image.png)

#### **Phase 2: Health and Economic Indicators**
We aligned the following datasets by country and year:
* Immunization (DPT coverage)
* Healthcare Expenditure (% of GDP)
* GDP per capita and WASH Access
* Country Income Status

![Data Overview](path/to/image.png)

#### **Phase 3: Data Merging and Audit**
* Merged datasets using `iso_code` + `year`.
* Removed duplicates and incomplete rows.
* **Output:** `merged_data.csv` covering 186 countries.

![Merged Data Audit](path/to/image.png)

---

### **Step 2: Visualizing Under-5 Mortality vs GDP**

We explored the **Preston Curve** using an **Animated Bubble Chart (Plotly)**.
* **Bubble Size:** Under-5 population.
* **Color:** SDG region.
* **Key Insight:** We observed a strong negative correlation between GDP and mortality. Small wealth gains in low-income countries lead to the largest mortality reductions.

![Preston Curve Animation](path/to/image.gif)

---

### **Step 3: Handling Missing Data**

* **Pattern Analysis:** Visualized via heatmaps; missingness was associated with higher mortality.
* **Classification:** Identified as **Missing at Random (MAR)**.
* **Imputation:** Used **MICE (2l.pmm)** with predictors including mortality, population, income status, and region.
* **Validation:** Density plots and convergence checks confirmed realistic and bounded imputations.

![Missing Data Heatmap](path/to/image.png)
![Imputation Validation](path/to/image.png)

---

### **Step 4: Regression Analysis**

**Modeling Approach:**
* **Panel Dataset:** 122 countries (2000–2022).
* **Method:** Median Quantile Regression with bootstrapped errors and fixed effects.

#### **Key Findings**
1.  **Efficiency:** Health spending is significantly more efficient in high-income countries.
2.  **System Penalty:** Low-income countries face an efficiency penalty due to weaker health system maturity.
3.  **Drivers:** Immunization coverage and WASH infrastructure remain the most critical drivers of child survival.
4.  **Conclusion:** GDP growth alone is insufficient without targeted, strategic health system investment.

![Regression Results](path/to/image.png)
