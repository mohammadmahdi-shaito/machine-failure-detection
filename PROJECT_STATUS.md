# Project status

Stage 1 is complete and executed. No models have been trained.

## Completed implementation

- Preserved the existing Python ignore rules and expanded the starter README. No additional project instructions were found inside the repository.
- Downloaded and extracted the actual official UCI AI4I 2020 archive into `data/`. The raw file is unchanged and ignored by Git.
- Added a readable notebook covering actual schema inspection, missingness, duplicates, target counts, leakage exclusions, stratified splitting, split assertions, and training-only exploration.
- Added pinned direct dependencies, dataset attribution and manual download instructions, and run instructions.

## Input checks executed

- Actual CSV: 10,000 rows and 14 columns; target counts 9,661 non-failures and 339 failures (3.39%).
- Python standard-library CSV inspection: zero empty cells, zero full-row duplicates, zero duplicates after excluding identifiers, and zero duplicate predictor combinations. No rows were removed.
- SHA-256: `dc6630cd9b1f0f853922fad78a1b6436570d3f1ec863f1dd5c4340ac56bc8a8e`.
- The raw file includes a UTF-8 BOM; pandas reads the first column as `UDI`.
- pandas confirmed shape (10,000, 14), no missing values, and all duplicate counts above. Product ID and Type are object columns; air/process temperatures and torque are float64; UDI, speed, wear, target, and five failure-mode labels are int64. Complete per-column counts and dtypes are in `results/schema.csv`.

## Split design

Stratified 60/20/20 training/validation/test, random_state=42 for both operations. Original zero-based CSV data-row indices are stored in `results/split_assignments.csv`, together with source hash and software versions in `results/split_metadata.json`. Later stages must reuse those assignments. All assertions for non-overlap, complete coverage, sizes, both classes, and agreement with existing assignments passed, including repeated execution.

| Split | Non-failures | Failures | Total | Failure rate |
| --- | ---: | ---: | ---: | ---: |
| Training | 5,797 | 203 | 6,000 | 3.3833% |
| Validation | 1,932 | 68 | 2,000 | 3.4% |
| Test | 1,932 | 68 | 2,000 | 3.4% |

## Files

- `README.md`: project scope, concepts, limitations, setup and execution.
- `requirements.txt`: pinned direct notebook/analysis dependencies.
- `.gitignore`: existing rules preserved; local raw CSV/ZIP ignored.
- `data/README.md`: official source, attribution, license, manual download.
- `notebooks/failure_detection.ipynb`: Stage 1 analysis and splitting.
- `results/`: generated schema, assignments, split summary, metadata and three plots after execution.
- `PROJECT_STATUS.md`: this record.

## Execution, checks, and unresolved issues

- Installed Python 3.12.13 in `.venv` and all dependencies from `requirements.txt`. Direct analysis versions: pandas 2.2.3, Matplotlib 3.9.2, scikit-learn 1.5.2. Direct requirements are pinned; transitive packages are not fully locked.
- Executed the complete notebook successfully and reran it against existing split files. Final code cells have stored outputs and no errors. No preprocessing or models were fitted.
- Inspected all three generated PNGs. Corrected a title encoding issue and used shared torque histogram bins; reran successfully. Training plots show strong class imbalance, a right tail in rotational speed, roughly bell-shaped torque, and Type L as the most common category. These exploratory associations do not establish causation.
- Python syntax checks passed for every code cell. `git diff --check` passed. Raw CSV/ZIP, environment, and generated caches are ignored; analysis outputs remain available for review.
- The initial sandboxed Jupyter startup stalled with profile permissions. Execution succeeded outside the sandbox after approval. Windows emitted a non-fatal ZMQ event-loop warning. There are no unresolved Stage 1 data or analysis blockers; this environment required permission to launch its notebook kernel.

Synthetic benchmark results do not establish real factory performance or future breakdown forecasting. Relationships between ordered observations can make random-split results optimistic. Validation and test sensor distributions are deliberately not explored.

Later stages must implement and evaluate the majority-class baseline, logistic regression, random forest, and threshold investigation before those resume claims are supported. The user explicitly requested committing and pushing Stage 1 to the configured GitHub repository after local completion.
