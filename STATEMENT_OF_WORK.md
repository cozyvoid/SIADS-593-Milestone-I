# Statement of Work (SOW)

## Project Title
Racial Disparities in Maternal Mortality and Hospital Care Access in the United States (2021–2023)

## Team Members
- Carter Pasternak
- Samantha Salazar

## Project Overview
This project examines racial disparities in maternal mortality across U.S. states from 2021–2023 and evaluates whether variation in hospital characteristics and maternal care infrastructure are associated with differences in disparity magnitude. Using CDC WONDER mortality data and CMS Hospital Compare data, we compute state-level mortality rates for Black and White women, derive disparity metrics, and analyze their relationship to hospital access indicators.

The project focuses on descriptive and exploratory analysis at the state-year level.

---

## Project Objectives

1. Compute maternal mortality rates by race (Black and White) for 2021–2023.
2. Quantify racial disparities using:
   - Absolute gap (Black − White rate)
   - Relative ratio (Black / White rate)
3. Construct state-level hospital infrastructure measures:
   - Share of hospitals with emergency services
   - Share with EHR interoperability
   - Average hospital rating
4. Examine geographic variation in disparities.
5. Explore associations between hospital characteristics and disparity magnitude.
6. Communicate findings through maps, ranked charts, and comparative visualizations.

---

## Scope

### In Scope
- State-level aggregation
- 2021–2023 time frame
- Black vs. White maternal mortality comparisons
- Structural hospital characteristics
- Descriptive statistical analysis
- Data visualization and interpretation

### Out of Scope
- Causal inference
- Individual-level analysis
- Within-state hospital-level matching
- Socioeconomic covariate modeling
- Age-adjusted mortality modeling
- Predictive modeling

---

## Datasets

### Primary Dataset
**CDC WONDER – Maternal Mortality (ICD-10 O00–O99)**  
- State-level death counts
- Population counts
- Race (Single Race 6 classification)
- Years: 2021–2023

### Secondary Dataset
**CMS Hospital General Information Data**
- Emergency services indicator
- EHR interoperability indicator
- Overall hospital rating
- October snapshots for 2021–2023

---

## Data Processing Plan

### Maternal Mortality Data
- Filter to 2021–2023
- Treat suppressed values as missing (not zero)
- Aggregate deaths and population by state, race, and year
- Compute mortality rate per 100,000
- Compute disparity gap and ratio

### Hospital Data
- Use October snapshots for consistency
- Standardize Yes/No indicators to binary (1/0)
- Aggregate to state-year level
- Compute proportions and averages

### Integration
- Merge datasets by state and year
- Exclude incomplete state-year race pairs
- Produce final analytical dataset

---

## Deliverables

- Cleaned mortality dataset (2021–2023)
- Cleaned hospital dataset (2021–2023)
- Merged analysis dataset
- Reproducible cleaning notebooks
- Visualizations:
  - Choropleth maps (disparities and hospital metrics)
  - Ranked bar charts
  - SPLOM (exploratory)
- Final written report (LaTeX)
- README and documentation files

---

## Roles and Responsibilities

### Samantha Salazar
- CDC WONDER data extraction and cleaning
- Disparity metric construction
- Hospital data cleaning and aggregation
- Methods documentation
- Report writing (Methods, Results, Discussion)
- Visual redesign and narrative development

### Carter Pasternak
- State-level hospital metric construction
- Choropleth map development
- Bar chart creation
- Visual integration into report
- Contributing to Results interpretation

Both team members:
- Joint analysis decisions
- Peer review of code
- Presentation preparation

---

## Timeline

| Phase | Task | Owner | Status |
|-------|------|-------|--------|
| Data Collection | Extract CDC WONDER data | Sam | Complete |
| Data Collection | Extract CMS hospital data | Sam | Complete |
| Cleaning | Mortality cleaning | Sam | Complete |
| Cleaning | Hospital cleaning | Sam | Complete |
| Integration | Merge datasets | Carter | Complete |
| Analysis | Disparity calculations | Sam | Complete |
| Analysis | Hospital associations | Carter | Complete |
| Reporting | Draft report | Both | Complete |
| Finalization | Revisions and submission | Both | Complete |

---

## Risks and Mitigation

| Risk | Mitigation |
|------|------------|
| Suppressed mortality counts | Treat as missing; exclude incomplete states |
| Small state denominators | Interpret cautiously; avoid causal claims |
| Proxy hospital measures | Explicitly state structural limitations |
| Ecological fallacy | Emphasize state-level inference only |

---

## Assumptions

- CDC death certificates accurately reflect maternal causes.
- CMS hospital data accurately represent hospital characteristics.
- October snapshots reasonably represent annual hospital structure.
- State-level aggregation is appropriate for exploratory analysis.

---

## Signatures

Samantha Salazar: Samantha A. Salazar  
Carter Pasternak: Carter R. Pasternak 
Date: 02/20/2026
