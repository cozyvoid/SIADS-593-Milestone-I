---

# Racial Disparities in Maternal Mortality and Hospital Care Access (2021–2023)

## Project Overview

This project investigates racial disparities in maternal mortality across U.S. states and evaluates whether variation in hospital characteristics and care access may be associated with the magnitude of those disparities.

The analysis integrates:

* **CDC WONDER maternal mortality data (2021–2023)**
* **CMS Hospital General Information data (October 2021–December 2023)**

The unit of analysis is **state–year (2021–2023)**.

---

## Research Question

Are racial disparities in maternal mortality associated with differences in hospital characteristics and maternal care access across U.S. states?

---

## Repository Structure

```
project_root/
│
├── data/
│   ├── raw/
│   │   ├── cdc_wonder_maternal_mortality_2018_2023_raw.csv
│   │   ├── Hospital_General_Information_2021.csv
│   │   ├── Hospital_General_Information_2022.csv
│   │   └── Hospital_General_Information_2023.csv
│   │
│   ├── clean/
│   │   ├── cdc_wonder_maternal_mortality_2021_2023_clean.csv
│   │   ├── hospitals_clean_2021_2023.csv
│   │
│   ├── analysis/
│   │   ├── state_race_mortality_rates_2021_2023.csv
│   │   └── state_maternal_racial_disparities_2021_2023.csv
│
├── notebooks/
│   ├── 01_cdc_wonder_maternal_mortality_cleaning_2021_2023_final.ipynb
│   ├── 01_clean_hospital_general_information_final.ipynb
│   └── cdc_wonder_hospital_info_merged_visualizations.ipynb
│
├── documentation/
│   ├── cdc_wonder_data_extraction_notes.md
│   └── hospital_data_extraction_and_cleaning_notes.md
│
└── README.md
```

---

## Data Sources

### 1. CDC WONDER – Maternal Mortality

* Dataset: Multiple Cause of Death (Final)
* ICD-10 codes: O00–O99 (Pregnancy, childbirth, puerperium)
* Race classification: Single Race 6 (Black, White)
* Years: 2021–2023
* Aggregation level: State

Detailed extraction procedure is documented in:
**cdc_wonder_data_extraction_notes.md** 

---

### 2. CMS Hospital General Information

* Source: Centers for Medicare & Medicaid Services
* Reporting cycle: Quarterly
* Data used: October 2021 – December 2023
* Structure: Hospital–year observations

Extraction and cleaning process documented in:
**hospital_data_extraction_and_cleaning_notes.md** 

---

## Data Processing Pipeline

### Maternal Mortality Data

1. Extract deaths and population counts by state and race
2. Convert suppressed counts to missing values
3. Aggregate across years (2021–2023)
4. Calculate crude mortality rates
5. Compute disparity metrics:

   * Absolute Gap
   * Relative Ratio

### Hospital Data

1. Concatenate yearly CMS hospital files
2. Standardize column names
3. Normalize binary indicators (Yes/No → 1/0)
4. Convert ratings to numeric
5. Aggregate hospital metrics to state–year level:

   * Number of hospitals
   * % with emergency services
   * % with EHR interoperability
   * Average hospital rating

### Final Dataset

Maternal mortality and hospital metrics were merged by:

* `state`
* `year`

---

## Derived Variables

| Variable        | Description                                  |
| --------------- | -------------------------------------------- |
| rate_black      | Black maternal mortality rate per 100,000    |
| rate_white      | White maternal mortality rate per 100,000    |
| mortality_gap   | Absolute disparity (Black − White)           |
| mortality_ratio | Relative disparity (Black / White)           |
| pct_emergency   | Share of hospitals with emergency services   |
| pct_ehr         | Share of hospitals with EHR interoperability |
| avg_rating      | Average CMS overall hospital rating          |

---

## Notebooks

### 01_cdc_wonder_maternal_mortality_cleaning_2021_2023_final.ipynb

Cleans and aggregates CDC maternal mortality data.

### 01_clean_hospital_general_information_final.ipynb

Cleans CMS hospital data and produces state-year hospital metrics.

### cdc_wonder_hospital_info_merged_visualizations.ipynb

Merges datasets and generates:

* Choropleth maps
* Ranked disparity bar charts
* Scatterplots (hospital access vs disparity)
* Hospital quality maps

---

## Important Methodological Notes

* Suppressed CDC counts were treated as missing.
* Zero counts were retained.
* 2021 hospital data reflect partial-year coverage (October–December).
* No imputation was performed for missing hospital ratings or EHR reporting.

---

## Software Requirements

* Python 3.x
* pandas
* numpy
* matplotlib
* seaborn
* geopandas
* plotly (optional)
* jupyter

Install dependencies with:

```
pip install pandas numpy matplotlib seaborn geopandas plotly
```

---

## Reproducibility

CDC WONDER does not provide a permanent query URL.
Extraction parameters are documented for manual replication in .

All cleaned and merged datasets are included to avoid repeated manual extraction.

---

## Limitations

* Analysis limited to 2021–2023
* Hospital data reflect quarterly reporting snapshots
* Maternal mortality calculated using crude (not age-adjusted) rates
* State-level aggregation may mask within-state disparities

---

## Authors

Samantha A. Salazar and Carter Pasternak
SIADS 593 – Milestone I Project
University of Michigan
Master of Applied Data Science

---

