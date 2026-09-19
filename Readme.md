Bearing RUL Prediction — XJTU-SY (Random Forest Baseline)
Predicts Remaining Useful Life (%) for rolling bearings using hand-crafted vibration features + Random Forest, on the XJTU-SY dataset.

Data
- Pre-segmented `.npy` arrays: `x{tr|te}{condition}_{bearing}.npy` (raw signal windows, shape `n_snapshots × 32768 × 2`) and matching `y*.npy` (per-snapshot RUL %, shape `n_snapshots × 1`).
- Train/test split is pre-defined by filename (`tr`/`te`).
- RUL labels are near-linear (100% → 0% evenly per bearing) rather than physically derived.


Usage
Update the path constants at the top of each code file for your local setup.

Features

24 features per snapshot (12 per channel, horizontal + vertical):
Time domain— mean, std, rms, peak, skewness, kurtosis, crest/shape/impulse factor, peak-to-peak
Frequency domain— freq mean/std/peak, spectral energy

## Roadmap

-Currently investigating cause of R² ≈ 1 on test set (suspect: linear RUL labels + monotonic feature trends leaking time info; verify no train/test bearing overlap)
-Hyperparameter tuning (grid/random search)
-Richer features (envelope spectrum, wavelet energy, fault characteristic frequencies)
-Use `condition` as a model input, not just metadata
-Try alternative RUL labeling (e.g. piecewise/nonlinear degradation curve)
-Compare against other models (SVR, XGBoost, LSTM)
-Ensemble/switching model: combine multiple models, dynamically weighting or switching between them based on degradation stage, to produce one more accurate RUL curve

