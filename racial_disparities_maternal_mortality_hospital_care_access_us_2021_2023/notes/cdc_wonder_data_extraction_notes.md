# Data Extraction Notes  
CDC WONDER Maternal Mortality Data (2021–2023)

## Purpose
These notes document how maternal mortality data were extracted from the CDC WONDER
Multiple Cause of Death database for use in the project:

**“Racial Disparities in Maternal Mortality and Their Association with Hospital Characteristics and Maternal Care Access Across U.S. States (2021–2023)”**

The goal of this extraction was to obtain state-level maternal mortality data by race
that could be cleaned, aggregated, and merged with hospital and maternal care access datasets.

---

## Data Source
- Platform: CDC WONDER
- Dataset: Multiple Cause of Death (Final)
- Provider: National Center for Health Statistics (NCHS)
- Access method: Web-based query interface with CSV export

---

## Time Frame
- Years selected: **2021–2023**
- Rationale:
  - Aligns with availability and coverage of secondary datasets (hospital characteristics and maternal care access data)
  - Allows aggregation across multiple years to mitigate small counts and suppression

---

## Cause of Death Selection
- Cause type: **Underlying Cause of Death**
- ICD-10 codes used: **O00–O99**
  - Pregnancy, childbirth, and the puerperium
- Rationale:
  - Standard definition for maternal mortality
  - Avoids double counting that can occur with multiple-cause selections

---

## Geography
- Geographic level: **State**
- Included: All U.S. states available in CDC WONDER
- Excluded:
  - Non-state geographies (e.g., territories) where applicable

---

## Race Classification
- Race variable: **Single Race 6**
- Races selected:
  - Black or African American
  - White
- Rationale:
  - Ensures mutually exclusive racial categories
  - Avoids ambiguity introduced by multi-race classifications
  - Maximizes comparability across states

---

## Measures Selected
The following measures were requested in the CDC WONDER query:

- Deaths
- Population
- Crude Rate (exported but **not used** in analysis)

Rationale:
- Deaths and population are required to compute aggregated mortality rates after cleaning
- Crude rates provided by CDC WONDER are unstable for small populations and suppressed cells and were therefore discarded during cleaning

---

## Suppression and Zero Counts
CDC WONDER applies suppression rules for small cell counts to protect confidentiality.

During extraction:
- Both **suppressed values** and **zero-death rows** were included in the export

During cleaning (documented in the cleaning notebook):
- Suppressed death counts were converted to missing values (`NaN`)
- Zero death counts were retained as true zeros
- Aggregation across years was performed prior to rate calculation to reduce the impact of suppression

---

## Output Format
- Export format: CSV
- File naming (raw export prior to cleaning):
  - `cdc_wonder_maternal_mortality_2021_2023_raw.csv`

This raw file was then processed and cleaned in the notebook:
`01_cdc_wonder_maternal_mortality_cleaning_2021_2023.ipynb`

---

## Notes on Reproducibility
- The CDC WONDER interface does not provide a persistent query URL
- These notes are intended to allow another analyst to manually reproduce the extraction if needed
- Cleaned and analysis-ready versions of the data are included in the `data/clean/` and `data/analysis/` folders to avoid repeated manual extraction

---

## Contact / Context
This extraction was performed as part of a collaborative academic project.
Questions about the cleaning or aggregation steps should be directed to the accompanying
notebook and README documentation.
