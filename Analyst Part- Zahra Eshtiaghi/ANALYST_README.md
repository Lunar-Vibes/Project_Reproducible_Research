# Analyst Part — Statistics & Visualizations

Author: Zahra Eshtiaghi
Reproduction of Smithies et al. (2021), *A Random Forest approach to identify
metrics that best predict match outcome and player ranking in the esport
Rocket League* (`s41598-021-98879-9.pdf`).

This file documents **my part of the project** (the Analyst role) and explains
the **standard conventions** a reproducible-research repo should follow.

---

## 1. What the Analyst part contains

| File | Type | What it is |
|------|------|------------|
| `Analysis_Statistics_Visualizations.ipynb` | notebook | Main analyst deliverable, already executed — every figure is embedded so it can be read without re-running. |
| `analyst_run.py` | script | Core statistics + figures (Analysis 1, Table 1, Fig 3, Fig 4, Fig 5, confusion matrix). One-command reproducible run. |
| `analyst_extra.py` | script | Extra reproductions: Fig 1, Fig 2b note, Table 2, Fig 6. |
| `build_notebook.py` | script | Rebuilds the notebook from source code. |
| `analyst_requirements.txt` | config | Pinned Python dependencies for the analyst pipeline. |
| `analyst_figures/` | folder | All output PNG figures (300 dpi) and CSV tables. |
| `update.txt` | report | Full reproducibility report + every difference from the paper. |

## 2. How to run

```bash
pip install -r analyst_requirements.txt
python analyst_run.py        # core analysis -> analyst_figures/
python analyst_extra.py      # Fig 1, Fig 2b, Table 2, Fig 6
```

All randomness uses `RANDOM_STATE = 123` (same seed as the modelling
notebooks), so results are identical on every run. To reproduce the paper's
heavier classifier (964 trees instead of the fast default 200):

```bash
ANALYST_NTREES=964 python analyst_run.py
```

## 3. What could and could not be reproduced

| Paper item | Status | Note |
|------------|--------|------|
| Fig 2a, 3a, 3b, 4, 5, 6 | FULL | Reproduced in Python. |
| Table 1, Table 2 | FULL | Numbers match paper (R² within 0.001). |
| Fig 1 | PARTIAL | Needs the whole-population MMR data (season 14), not in the OSF archive. A sample-composition chart is shipped instead. |
| Fig 2b (IGSD) | NOT REPRODUCIBLE | IGSD column is absent from every OSF file; rebuilding it would mean inventing Psyonix' scoring formula. A documented placeholder is shipped. |

Full detail is in `update.txt`.

---

## 4. "Standard conventions" — what my teammate is asking about

A reproducible-research repo should follow a **standard project structure** so
that anyone (a grader, a new teammate) can understand and re-run it *without
asking the author*. The key conventions are:

1. **Separation of concerns** — raw data, source code, outputs and figures
   each live in their own folder. They are never mixed in the root.
2. **Raw data is read-only** — `data/raw/` is never edited; cleaned data is
   written to `data/processed/`. This protects the original input.
3. **Code vs notebooks** — reusable logic lives in `.py` files under `src/`;
   notebooks (`notebooks/`) are for exploration and presentation only.
4. **Outputs are regenerable** — anything in `outputs/` or `images/` can be
   deleted and recreated by running the code, so these are usually listed in
   `.gitignore` and not committed.
5. **Consistent naming** — lowercase, `snake_case`, **no spaces** in file or
   folder names; figure names describe their content (`fig3a_PI_heatmap_raw.png`).
6. **Pinned dependencies** — a `requirements.txt` so the environment is
   reproducible.
7. **One clear entry point** — a `main.py` or a documented "how to run" so the
   whole project reproduces with one command.
8. **README + .gitignore** — README explains the project; `.gitignore` keeps
   large/generated files out of git.

### Recommended layout for the Analyst part

Right now my analyst files sit flat in the repo root. Following the standard
conventions above, they would be organised like this:

```
analysis/
├── notebooks/
│   └── Analysis_Statistics_Visualizations.ipynb   # presentation notebook
├── src/
│   ├── analyst_run.py                             # core analysis
│   ├── analyst_extra.py                           # Fig 1, 2b, Table 2, Fig 6
│   └── build_notebook.py                          # rebuilds the notebook
├── outputs/
│   ├── figures/   # all PNG plots   (regenerable -> .gitignore)
│   └── tables/    # all CSV tables  (regenerable -> .gitignore)
├── requirements.txt                               # pinned dependencies
├── update.txt                                     # reproducibility report
└── README.md                                      # this file
```

Mapping from the current flat layout to the structure above:

| Current (flat in root) | Standard location |
|------------------------|-------------------|
| `Analysis_Statistics_Visualizations.ipynb` | `analysis/notebooks/` |
| `analyst_run.py`, `analyst_extra.py`, `build_notebook.py` | `analysis/src/` |
| `analyst_figures/*.png` | `analysis/outputs/figures/` |
| `analyst_figures/*.csv` | `analysis/outputs/tables/` |
| `analyst_requirements.txt` | `analysis/requirements.txt` |
| `update.txt`, `ANALYST_README.md` | `analysis/` |

> Note: moving the files also means updating the path variables at the top of
> each script (`FIG_DIR`, `ARCHIVE`, `MODEL_RESULTS`). The scripts already use
> `pathlib` so the change is small, but it must be done together so the whole
> team's paths stay consistent. We decided to keep the files flat for now and
> agree on the structure with the team first.
