# Predicting Road Accident Severity in Great Britain

Data Science course project — King Faisal University, College of Computer Science & Information Technology.

This project analyses all **202,452 police-reported injury collisions in Great Britain in 2024 and 2025** (DfT STATS19 open data) to find which conditions are linked to severe collisions. Severity is studied as **KSI (killed or seriously injured) vs. slight**.

- **Milestone 1:** data preparation, cleaning, exploratory data analysis and hypothesis tests.
- **Milestone 2:** classification models to predict KSI collisions.

## Team

| Member | Student ID | Role |
|---|---|---|
| Afnan AlNasser | 223049806 | Member 1 — data preparation, Abstract, Introduction, dataset description, time factors, report integration |
| Lulu Abdullah AlMaghlouth | 223036019 | Member 2 — Literature Review, environmental factors, references |
| Roaa Almansour | 223031400 | Member 3 — data cleaning, preprocessing and methodology, data quality, road factors |
| Shahad AlShammary | 223037205 | Member 4 — descriptive statistics, severity and year comparison, hypothesis tests, conclusion |

## Repository structure

```
├── README.md
├── data/
│   ├── raw/                 Original DfT files (unchanged)
│   └── processed/           Files produced by the notebooks
├── notebooks/               One notebook per step, run in order
├── figures/                 Charts used in the report
└── report/                  Milestone reports (Word / PDF)
```

## Notebooks (run in this order)

| Notebook | Owner | What it does | Output |
|---|---|---|---|
| `01_data_preparation.ipynb` | Afnan AlNasser | Merges 2024 + 2025, decodes all codes with the DfT data guide, converts hidden missing codes to real missing values, adds the KSI targets, time features and grouped categories | `collisions_2024_2025_prepared.csv.gz`, `missing_values_report.csv`, `data_dictionary.csv` |
| `Member3_Data_Cleaning.ipynb` | Roaa Almansour | Handles the remaining missing values (codes and `Unknown` categories, indicator columns), checks data types, ranges and dates, removes redundant label columns | `UK_Road_Accidents_Cleaned_2024_2025.csv.gz` |
| `02_time_factors_member1.ipynb` | Afnan AlNasser | KSI rate by hour, weekday, month and rush hour; chi-square and z-tests; 2024 vs 2025 comparison | `fig2_ksi_by_hour.png` |
| `Member4_EDA.ipynb` | Shahad AlShammary | Descriptive statistics, outliers, severity by year and the seven hypothesis tests (Table III) | `fig1_severity_by_year.png` |

## Data

Source: Department for Transport, *Road Safety Open Data* — https://www.gov.uk/government/statistical-data-sets/road-safety-open-data (final 2024 and 2025 collision files, downloaded 17 October 2026).

| File | Description |
|---|---|
| `data/raw/dft-road-casualty-statistics-collision-2024.csv` | 100,927 collisions, 44 columns |
| `data/raw/dft-road-casualty-statistics-collision-2025.csv` | 101,525 collisions, 44 columns |
| `data/raw/dft-road-casualty-statistics-road-safety-open-dataset-data-guide-2025.xlsx` | Code dictionary used to decode the data |
| `data/processed/collisions_2024_2025_prepared.csv.gz` | 202,452 rows × 68 columns, decoded and ready for analysis |
| `data/processed/missing_values_report.csv` | Missing values per column after decoding |
| `data/processed/data_dictionary.csv` | Meaning, type and categories of the analysis variables |
| `data/processed/UK_Road_Accidents_Cleaned_2024_2025.csv.gz` | 202,452 rows × 52 columns, cleaned dataset used for the analysis |

Contains public sector information licensed under the [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).

**Important note on severity:** police forces are moving to injury-based severity reporting, which records more injuries as serious. Its share rose from 58.8% (2024) to 86.5% (2025), so year-to-year comparisons use the DfT severity-adjusted values (`KSI_adjusted`) as well as the recorded values (`KSI`).

## How to reproduce

1. Put every file from `data/raw/` and `data/processed/` and the notebooks into one Google Drive folder named `Road_Accident_Project` (in *My Drive*).
2. Open each notebook in Google Colab and choose **Runtime → Run all**, in the order of the table above.
3. Allow Google Drive access when asked. Each notebook reads its inputs from, and saves its outputs to, that folder.

If a notebook cannot find a file, check the file path in its first code cell and point it to your folder. The two analysis notebooks read the cleaned file, so run `Member3_Data_Cleaning.ipynb` first.

**Requirements:** Python 3, pandas, NumPy, Matplotlib, Seaborn, SciPy, openpyxl (all preinstalled in Google Colab).
