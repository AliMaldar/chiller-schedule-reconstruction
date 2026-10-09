# Chiller Operating-Schedule Reconstruction

Research code for *Reconstructing Chiller Operating Schedules from 15-min Aggregate Building Electricity: A Cross-Building Learning Framework*.

## Method

The pipeline reconstructs electrical chiller operating states and daily/monthly schedules from **15-minute whole-building electricity**, weather, and calendar context. Measured chiller electricity is used to construct supervised reference labels, **not as a prediction input**. The original implementation uses 41 contextual H/V/G features, event-aware neural-network training, five seeds per fold, and **leave-one-system-out (LOSO)** evaluation across seven systems. A fixed 0.5 ensemble threshold precedes daily event extraction and schedule-level scoring.

The validation notebook adds hierarchical bootstrap uncertainty, controlled ablations, and reference-definition sensitivity analyses.

## Run

1. Install Python dependencies: `python -m pip install -r requirements.txt`.
2. Supply **authorized** input data and private season configuration as specified in [DATA_SCHEMA.md](DATA_SCHEMA.md).
3. From the repository root, launch `jupyter lab` and run the notebooks in order:
   - [`01_main_analysis.ipynb`](01_main_analysis.ipynb) — reference construction, training, inference, and evaluation.
   - [`02_validation_extensions.ipynb`](02_validation_extensions.ipynb) — uncertainty, ablations, and reference sensitivity.

The validation notebook imports the main notebook by **cell index**. Do not reorder, insert, or delete notebook cells. Set `TASK1_WORKDIR` to the repository root if Jupyter is started elsewhere (otherwise the default is the current directory).

## Data availability

The dataset, private run configuration, checkpoints, and outputs are **not distributed**. Original measurements are confidential; reproducing the reported results requires authorized data and the corresponding private configuration. The notebooks have no stored execution results. The repository does not independently reproduce the paper's private-data scores.
