# IMDb 5000+ Movies & Multiple Genres analysis

This repository currently contains a Jupyter notebook only; it does **not** include the CSV dataset, a packaged environment, or an automated analysis pipeline. The notebook's results have not been rerun as part of this maintenance change.

## Dataset setup

The notebook expects the pre-cleaned file `IMDb_All_Genres_etf_clean1.csv`. Obtain the source data from the [IMDb 5000+ Movies & Multiple Genres Kaggle dataset](https://www.kaggle.com/datasets/rakkesharv/imdb-5000-movies-multiple-genres-dataset) and prepare that CSV locally. The dataset is intentionally not checked into this repository.

From the repository root, either:

1. Place the file at `data/IMDb_All_Genres_etf_clean1.csv`, or
2. Set `IMDB_DATASET_PATH` to the full or working-directory-relative path to the file.

For example, in a shell before launching Jupyter:

```sh
export IMDB_DATASET_PATH="$HOME/datasets/IMDb_All_Genres_etf_clean1.csv"
jupyter lab
```

Run the notebook from the repository root when using the default `data/` location. If the file is missing, the notebook reports the expected path and how to configure it. Dataset retrieval, Kaggle authentication, and preprocessing are not automated here; no Kaggle API key is needed in notebook source code.

## Modeling caveats

The notebook used two features derived directly from `Total_Gross`, the regression target (`Total_Gross * Rating` and `Total_Gross / Runtime`). Those predictors have been removed from the primary regression feature list to avoid target leakage, and the decision-tree cross-validation/grid search now uses the training split rather than the held-out test rows. This is a focused correction, not a full methodological review; data-dependent code paths and all model results remain unvalidated because the dataset is not included. Do not treat the notebook's prior cached scores as current evidence.

## Environment

The notebook uses Python data-science libraries including pandas, NumPy, Matplotlib, Seaborn, Plotly, Cufflinks, SciPy, and scikit-learn. No dependency lockfile is supplied, and versions have not been validated against this notebook. Install compatible versions in an isolated environment and record the versions you use before relying on results. The dataset is required to execute the analysis.

## Security and notebook outputs

Notebook cell outputs and execution counts have been cleared to avoid publishing cached dataset rows, plots, or execution artifacts; rerunning the notebook will regenerate them locally. Keep datasets, Kaggle configuration files, and credentials out of commits. Use Kaggle's supported local credential configuration or a secret manager rather than embedding tokens in cells.

If a Kaggle API credential was ever exposed in this repository, **revoke it and issue a replacement in your Kaggle account**. This repository change cannot rotate credentials. Removing content from the current branch does not erase existing Git history; if a secret was committed, coordinate GitHub's sensitive-data/history cleanup with the repository owner after revocation. No claim is made that historical credentials have been rotated or that model performance has been validated.
