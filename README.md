# MPD Cu-Au Porphyry — 2023 Drill Program Analysis

An end-to-end data science pipeline applied to the 2023 Kodiak Copper 
MPD drill program near Merritt, BC — built on publicly available data 
from BC ARIS Assessment Report 42616.

26 drillholes. 5908 intervals. Six machine learning models. The goal: 
can geological logging data alone predict high-grade Cu mineralization 
before assay results come back from the lab?

---

## Background

The MPD project sits in the Nicola Belt of south-central BC — one of 
Canada's most prospective porphyry copper belts. Kodiak Copper's 2023 
drill program tested multiple target areas across the property, with 
the AXE West Zone emerging as the strongest Cu-Au target.

This project applies a full data science workflow to the public drill 
data — from raw PDF appendices through to a binary classification model 
that predicts high-grade Cu intervals from core logging observations alone.

---

## Project Structure

```
Exploration Analytics/
├── Data/
│   ├── raw/                        # Original CSV appendices from ARIS report
│   ├── clean/                      # Cleaned interval tables from Notebook 02
│   ├── interim/                    # Merged parquet file from Notebook 03
│   └── processed/                  # Final merged_intervals.csv for analysis
├── Maps/
│   └── Regional_Geology_Map.png    # Geology overlay used in spatial analysis
├── Notebooks/
│   ├── 00_project_overview.ipynb
│   ├── 01_data_importing_and_overview.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_sql_data_merging_and_analysis.ipynb
│   ├── 04_data_visualization_and_spatial_analysis.ipynb
│   └── 05_machine_learning.ipynb
├── Outputs/
│   ├── 3D_drillpad_b_holes.png
│   ├── representative_holes_map.html
│   ├── section_1_axe_002_004_003.png
│   └── section_2_axe_008_011_001.png
└── requirements.txt
```
---

## Notebooks

**00 — Project Overview**
Geological background, data sources, analytical methods, and key findings. Start here for the full project narrative.

**01 — Data Importing and Overview**
Imports seven raw CSV appendices from the ARIS report, manually transcribes collar coordinates from the PDF, standardizes column names, and exports minimally processed tables for cleaning.

**02 — Data Cleaning**
Restores drillhole structure corrupted by Excel merged cells, converts depth and sample fields to numeric, separates lithology, alteration, and mineralization into distinct tables, and exports four clean CSVs for SQL merging.

**03 — SQL Data Merging and Analysis**
Uses DuckDB to merge geological interval tables with assay results via a depth-based range join — handling the interval overlap problem that makes standard joins unsuitable for drillhole data. Exploratory SQL analysis identifies SKN + MM as the strongest grade combination and confirms AXE-23-011 as the top-ranked hole.

**04 — Data Visualization and Spatial Analysis**
Scores and ranks all 26 drillholes across four geological criteria, builds 3D drillhole geometry, generates plan-view and cross-section visualizations, and validates findings against Kodiak's published interpretation. Contains a clickable interactive plan-view map with geology overlay — open the notebook to access it.

**05 — Machine Learning**
Trains and evaluates six binary classification models — Logistic Regression, SVM, Random Forest, Bagging, Gradient Boosting, and XGBoost — to predict high-grade Cu intervals from geological logging data alone. Random Forest selected as the best model (AUC 0.8421, Recall 0.7117). Feature importances confirm the model independently recovered the same geological controls identified in Notebooks 03 and 04.

---

## Key Findings

- SKN alteration hosted in MM (Monzonite) is the strongest grade combination in the dataset — average Cu > 0.90% across 68 intervals
- Alteration intensity is a systematic grade predictor not addressed in Kodiak's published report
- AXE-23-011 is the standout hole of the program — highest composite score, strongest Cu p90 (0.55%), dominant skarn lithology (73%)
- High-grade Cu-Au mineralization clusters between 1200–1300m elevation in the AXE West Zone
- Random Forest recovered 71% of genuine high-grade intervals on unseen data with an AUC of 0.8421 — the model learned what the geology already indicated

---

## Tech Stack

Python (Pandas, NumPy, Scikit-learn, XGBoost, Matplotlib, Seaborn, Plotly, Folium) · SQL · DuckDB · Jupyter · Git
---

## Data Source

All data sourced from the BC Assessment Report Information System (ARIS), 
Assessment Report 42616 — publicly available through the Province of 
British Columbia.

[View Report on BC ARIS](https://apps.nrs.gov.bc.ca/pub/aris/Detail/42616)

---

## Author

**Max Charles** — Domain-driven data scientist with a background in 
exploration geology.

[GitHub](https://github.com/max-charles-ds) · 
[LinkedIn](https://www.linkedin.com/in/maxsveencharles/)