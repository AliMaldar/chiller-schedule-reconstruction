# Chiller Operating-Schedule Reconstruction

Research code for *Reconstructing Chiller Operating Schedules from 15-min Aggregate Building Electricity: A Cross-Building Learning Framework*.

## Method

The framework reconstructs chiller electrical operating states and daily/monthly schedules from **15-minute whole-building electricity**, weather, and calendar context. Measured chiller electricity supplies supervised reference labels but **is not used at inference**.

The main experiment uses 41 contextual H/V/G features, event-aware MLP training, five seeds per fold, and **leave-one-system-out (LOSO)** evaluation across seven systems. A fixed 0.50 ensemble threshold precedes daily event decoding and schedule-level assessment.

Additional analyses include hierarchical-bootstrap uncertainty, feature and weighting ablations, reference-definition sensitivity, and comparisons with **L2 logistic regression** and **histogram gradient boosting**. Both baselines use the same 41 features and LOSO assignments; the MLP comparison uses its saved predictions without retraining.

## Run

1. Install dependencies: `python -m pip install -r requirements.txt`.
2. Provide **authorized** measurements and private configuration as described in [DATA_SCHEMA.md](DATA_SCHEMA.md).
3. Launch `jupyter lab` from the repository root and run the relevant notebooks:
   - [`01_main_analysis.ipynb`](01_main_analysis.ipynb) — reference labels, features, MLP training, inference, and evaluation.
   - [`02_validation_extensions.ipynb`](02_validation_extensions.ipynb) — uncertainty estimates, ablations, and reference sensitivity.
   - [`03_baseline_comparison.ipynb`](03_baseline_comparison.ipynb) — logistic regression and gradient boosting versus frozen MLP predictions.

Run `01` before `02`. Notebook `02` imports cells from `01` by index; **do not reorder, insert, or delete cells in `01`**. Set `TASK1_WORKDIR` to the repository root if running outside it.

Notebook `03` requires the saved feature, reference-state, prediction, metric, and run-manifest outputs from `01`. Set `TASK1_RESULTS_DIR` to the directory containing `Run_Manifest_FINAL_PAPER.json` (normally `<repository-root>/results`). It trains only the two baselines and writes results under `baseline_comparison/` in that directory.

## Data availability

The confidential measurements, private configuration, checkpoints, and experimental outputs are **not included**. Reproducing the reported results requires authorized access to the original data and configuration. The released notebooks contain no saved execution outputs.
