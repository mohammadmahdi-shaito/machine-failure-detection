# Machine Failure Detection from Sensor Data

A beginner portfolio project for an inMind Academy application using Python, pandas, Matplotlib, and scikit-learn on the official synthetic UCI AI4I 2020 dataset.

Stage 1 implements inspection, training-only exploration, and reproducible splits. No models are trained. Later stages will compare a majority-class baseline, logistic regression, and random forest; evaluate precision, recall, F1, and confusion matrices; and investigate validation-set thresholds. Those resume claims remain pending.

## Run Stage 1

Use Python 3.12. From the repository root in PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m notebook
```

Open `notebooks/failure_detection.ipynb`, select the virtual environment's Python kernel, and run all cells in order. Launching from the root or `notebooks/` is supported. With uv, use `uv venv .venv --python 3.12` and `uv pip install --python .venv/Scripts/python.exe -r requirements.txt` for setup.

For noninteractive execution from the root:

```powershell
.\.venv\Scripts\python.exe -m nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=180 notebooks/failure_detection.ipynb
```

The CSV belongs at `data/ai4i2020.csv`; see [data instructions](data/README.md). The notebook saves three training-only PNG plots, schema and split summaries, original-row assignments, and dataset-hash metadata in `results/`. Keep split assignments and metadata together. Changed data or assignments stop execution rather than silently overwrite the experiment.

## Decisions and scope

The target is `Machine failure`. Predictors: `Type`, `Air temperature [K]`, `Process temperature [K]`, `Rotational speed [rpm]`, `Torque [Nm]`, `Tool wear [min]`. UDI and Product ID are excluded identifiers. TWF, HDF, PWF, OSF, RNF describe failure outcomes and would leak the answer, so they are excluded.

Stratified 60/20/20 training/validation/test splits use random_state=42 twice and preserve original zero-based row indices. Training guides exploration and eventual fitting; validation will guide model and threshold selection; test is reserved for final evaluation. Only basic file checks and partition counts describe all rows. No rows are automatically deleted.

These synthetic data support benchmark classification, not future breakdown forecasting or demonstrated real factory performance. Relationships between ordered observations can make random-split results optimistic.

See [PROJECT_STATUS.md](PROJECT_STATUS.md) for actual results and checks. GitHub changes are pushed only when explicitly requested.
