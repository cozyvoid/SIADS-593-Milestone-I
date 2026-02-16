# Hospital Data Extraction and Cleaning
SIADS 593 – Team Project  
Dataset: CMS Hospital General Information  
Temporal Coverage: October 2021 – December 2023  

---

## 1. Data Source

Hospital-level data were obtained from the **Centers for Medicare & Medicaid Services (CMS) Hospital General Information** public dataset. This dataset contains facility-level information for U.S. hospitals participating in Medicare, including hospital identifiers, geographic location, ownership and type classifications, service availability, health IT adoption indicators, and selected quality ratings.

CMS releases hospital general information data on a **quarterly reporting cycle**, rather than as complete calendar-year surveys.

---

## 2. Temporal Coverage

The hospital data used in this project cover the period from **October 2021 through December 2023**. Earlier quarters of 2021 were not included in the extracted dataset. As a result:

- Calendar year **2021 reflects partial-year hospital coverage** (October–December only)
- Years **2022 and 2023 provide more complete annual coverage**

All records were assigned a `year` value based on the CMS reporting period. Analyses involving hospital characteristics interpret 2021 cautiously, with greater emphasis placed on 2022–2023.

---

## 3. Raw File Organization

Raw CMS hospital files were extracted from quarterly CMS archives and renamed to preserve year provenance. Files were stored in the following directory structure:

work/data/raw/hospitals/
├── `Hospital_General_Information_2021.csv`
├── `Hospital_General_Information_2022.csv`
└── `Hospital_General_Information_2023.csv`


No preprocessing was applied to the raw CSV files prior to ingestion.

---

## 4. Data Ingestion

Each yearly CSV file was read into pandas and augmented with a `year` column to preserve temporal structure. The three datasets were then concatenated into a single long-format DataFrame, with each row representing a **hospital–year observation**.

---

## 5. Column Standardization and Selection

Column names were standardized to ensure consistency and reproducibility:

- Converted to lowercase
- Whitespace removed
- Special characters replaced with underscores

From the standardized schema, only variables relevant to hospital structure, access, and integration with maternal mortality outcomes were retained.

### Retained Variables

| Variable | Description |
|--------|-------------|
| hospital_id | CMS hospital identifier |
| hospital_name | Hospital name |
| state | Two-letter state abbreviation |
| hospital_city | City location |
| hospital_zip | ZIP code (stored as string) |
| year | Reporting year |
| hospital_type | CMS hospital classification |
| hospital_ownership | Ownership category |
| hospital_has_emergency_services | Emergency services availability |
| hospital_has_ehr_interoperability | EHR interoperability indicator |
| hospital_overall_rating | CMS overall hospital rating |

Columns were renamed to be **merge-safe**, human-readable, and consistent with naming conventions used in the CDC maternal mortality dataset.

---

## 6. Binary Variable Normalization

Two hospital characteristics—emergency service availability and EHR interoperability—were reported using heterogeneous text encodings. These fields were normalized to numeric binary indicators using the following rules:

| Original Encoding | Normalized Value |
|------------------|------------------|
| "Yes", "Y" | 1 |
| "No", "N" | 0 |
| Missing / Unreported | NaN |

Missing values were preserved and not imputed to avoid introducing bias or overstating hospital capabilities.

---

## 7. Data Type Handling

Additional data type standardization included:

- **ZIP codes** stored as character strings to preserve leading zeros
- **Hospital overall ratings** coerced to numeric values, with invalid entries converted to NaN
- **Year** stored as integer

---

## 8. Data Quality Checks

Several validation steps were performed:

- Verified one row per hospital per year (no duplicated hospital–year records)
- Confirmed state coverage across all years
- Assessed missingness rates for key variables:
  - Emergency services: 100% coverage
  - EHR interoperability: ~72.5% coverage
  - Overall rating: ~59% coverage

Observed missingness patterns were consistent with CMS reporting practices and were retained without imputation.

---

## 9. Output Dataset

The final cleaned hospital dataset was saved to:

`work/data/clean/hospitals_clean_2021_2023.csv`


This dataset is structured for aggregation to the **state–year level** and subsequent integration with CDC WONDER maternal mortality data.

---

## 10. Intended Use in Analysis

Hospital data will be aggregated to compute state–year indicators of maternal care infrastructure, including:

- Number of hospitals per state–year
- Proportion of hospitals offering emergency services
- Proportion of hospitals reporting EHR interoperability
- Average overall hospital rating

These aggregated measures provide contextual indicators of hospital access and capacity and will be used to assess whether differences in hospital characteristics are associated with racial disparities in maternal mortality across U.S. states.


