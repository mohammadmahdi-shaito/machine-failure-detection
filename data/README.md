# Dataset

Source: [UCI AI4I 2020 Predictive Maintenance Dataset](https://archive.ics.uci.edu/dataset/601/ai4i+2020+predictive+maintenance+dataset).

Attribution: AI4I 2020 Predictive Maintenance Dataset [Dataset]. (2020). UCI Machine Learning Repository. https://doi.org/10.24432/C5HS5C. License: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Related paper: S. Matzka, “Explainable Artificial Intelligence for Predictive Maintenance Applications,” 2020. The CSV is used without modification.

The official ZIP was downloaded for this project. `ai4i2020.csv` is the raw input and `ai4i2020.zip` is the original archive. Both are ignored by Git. No substitute or generated data are used.

Manual download:

1. Open the source page above and click **Download**.
2. Extract the ZIP and copy `ai4i2020.csv` here, at `data/ai4i2020.csv`.
3. Preserve the header, bytes, and row order. Avoid saving through a spreadsheet editor. The notebook records a SHA-256 fingerprint for exact input checking.

Direct official ZIP: https://archive.ics.uci.edu/static/public/601/ai4i+2020+predictive+maintenance+dataset.zip

Expected raw header, verified by the notebook:

```text
UDI,Product ID,Type,Air temperature [K],Process temperature [K],Rotational speed [rpm],Torque [Nm],Tool wear [min],Machine failure,TWF,HDF,PWF,OSF,RNF
```

UCI documents 10,000 synthetic observations. Temperatures use random walks and wear accumulates across observations. Related ordered observations may make random-split estimates optimistic. This is a classification benchmark, not future-event forecasting.
