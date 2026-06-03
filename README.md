
# Project: Predicting Rocket League Outcomes using Random Forest
### Reproducible Research Project — Smithies et al. (2021)

> Smithies, T. D., Campbell, M. J., Ramsbottom, N., & Toth, A. J. (2021). A Random Forest approach to identify metrics that best predict match outcome and player ranking in the esport Rocket League. *Scientific Reports*, 11, 19285. https://doi.org/10.1038/s41598-021-98879-9

---
## Team Members

- Kacper Geisshirt (443171)  
- Shagufta Shaheen (477654)  
- Zahra Eshtiaghi (476679)
- Celia Mlambo (476670)  

---
## Overview

This project reproduces the analysis of Smithies et al. (2021) in Python (scikit-learn, scipy, seaborn), replicating an R workflow originally built on the `randomForest`, `rfPermute`, and `rfUtilities` packages.

The original study applied Random Forest machine learning models to over 21,000 1v1 Rocket League matches to identify two categories of in-game metrics:

- **Performance Indicators (PIs):** metrics that predict match outcome (goal difference) *within* a given rank
- **Rank Indicators (RIs):** metrics that distinguish player skill level *across* different ranks

Four rank groups were studied: Bronze, Gold, Diamond, and Grand Champion (GC).

Our goal was to reproduce the paper's three analyses, all figures and tables, and to document any honest deviations driven by language differences or data availability.


---

## Key Results from the Original Paper

**Performance Indicators (PIs) — what predicts winning within a rank:**
- Shots taken
- Shots conceded
- Saves made
- Time spent goalside of the ball

**Rank Indicators (RIs) — what distinguishes player rank:**
- Time spent at supersonic speed
- Time spent on the ground
- Shots conceded
- Time spent goalside of the ball

Difference-score models (player stats relative to opponent) achieved R² > 0.80 in predicting goal difference across all ranks, outperforming raw-score models in every case.

---
## Repository Structure

```
Project_Reproducible_Research/
├── README.md                              ← this file
├── .gitignore
│
└── RR/                                    ← project root; run all commands from here
    ├── pyproject.toml                     ← shared project dependencies
    ├── uv.lock                            ← locked dependency versions
    ├── .python-version                    ← Python version for the virtual environment
    │
    ├── data_files/                        ← raw and processed input data
    │   ├── Raw score data/                ← per-player match metrics (28 features)
    │   │   ├── allranks_raw.xlsx
    │   │   ├── bronze_raw.xlsx
    │   │   ├── diamond_raw.xlsx
    │   │   ├── gc_raw.xlsx
    │   │   ├── gold_raw.xlsx
    │   │   └── Data for RI analysis/
    │   ├── Difference score data/         ← opponent-relative metrics (26 features)
    │   │   ├── GC_diff.xlsx
    │   │   ├── allrank_diff.xlsx
    │   │   ├── bronze_diff.xlsx
    │   │   ├── diamond_diff.xlsx
    │   │   └── gold_diff.xlsx
    │   ├── Metadata text files/           ← column descriptions for all datasets
    │   │   ├── allranks_raw_metadata.txt
    │   │   ├── bronze_raw_metadata.txt
    │   │   ├── diamond_raw_metadata.txt
    │   │   ├── gc_raw_metadata.txt
    │   │   ├── gold_raw_metadata.txt
    │   │   ├── allrank_diff_metadata.txt
    │   │   ├── bronze_diff_metadata.txt
    │   │   ├── diamond_diff_metadata.txt
    │   │   ├── GC_diff_metadata.txt
    │   │   ├── gold_diff_metadata.txt
    │   │   └── RI_analysis_raw_metadata.txt
    │   ├── Mean_decrease_accuracy_paper.png   ← paper's original Fig. 4 for comparison
    │   └── Workflow_chart.jpg                 ← paper's original Fig. 6
    │
    ├── notebooks/                         ← main analysis notebooks
    │   ├── 1.Cleaning_notebook.ipynb      ← data processing pipeline
    │   ├── 2.EDA.ipynb                    ← exploratory analysis + Optuna ntree search
    │   ├── 3.Regression.ipynb             ← Random Forest regression (PI identification)
    │   ├── 4.Classification.ipynb         ← Random Forest classification (RI identification)
    │   └── 5.Project_Results_Summary.ipynb ← consolidated results vs paper
    │
    ├── outputs/                           ← all generated artefacts
    │   ├── ntree_optimization_summary.csv ← optimal ntree and OOB metrics per dataset
    │   ├── RI_mean_decrease_accuracy.png  ← reproduced Fig. 4 (MDA bar chart)
    │   ├── analyst_figures/               ← all figures and tables from Zahra's pipeline
    │   └── rfpermute_saved_results/       ← saved rfPermute-style importance CSVs
    │       └── per_dataset/               ← one CSV per rank × score-type combination
    │
    └── Analyst Part- Zahra Eshtiaghi/    ← analyst pipeline (separate dependencies)
        ├── Analysis_Statistics_Visualizations.ipynb
        ├── analyst_requirements.txt
        └── analyst_figures/
```

---




## Instructions for reproduction

For notebooks folder:
1. Download or clone the repository locally.
2. Open the RR folder as the project root in your code editor of choice.
3. In a terminal opened at RR, run uv sync. This should install project dependencies.
4. Pick the interpreter from .venv
5. Run notebooks in which ever order, they are all independent. Warning - computation will take a LONG time.

The instructions for the analyst part are included in the Analyst Part- Zahra Eshtiaghi folder.



## Reference

Smithies, T. D., Campbell, M. J., Ramsbottom, N., & Toth, A. J. (2021). A Random Forest approach to identify metrics that best predict match outcome and player ranking in the esport Rocket League. *Scientific Reports*, 11, 19285. https://doi.org/10.1038/s41598-021-98879-9


## Reference
Smithies, T.D., Campbell, M.J., Ramsbottom, N. et al. (2021)  
https://www.nature.com/articles/s41598-021-98879-9
