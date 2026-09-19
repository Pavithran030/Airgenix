# AirGenix Repository Research Evidence Report

This report is based only on files present in this repository clone.
It distinguishes **Recorded values**, **Code-inferred values**, and **Missing / Not found** items.

---

## 1) Classification predictions, ground truth, confusion matrix, and test metrics

### Recorded
- Held-out test classification report in notebook output:
  - Agricultural: precision 0.95, recall 0.98, F1 0.96, support 4278
  - Burning: precision 0.77, recall 0.97, F1 0.86, support 1420
  - Industrial: precision 0.91, recall 0.96, F1 0.93, support 4675
  - Natural: precision 0.85, recall 0.94, F1 0.89, support 2412
  - Vehicular: precision 0.98, recall 0.86, F1 0.92, support 8489
  - Accuracy: 0.92
  - Macro avg: 0.89 / 0.94 / 0.91
  - Weighted avg: 0.93 / 0.92 / 0.92
  - Evidence: `/home/runner/work/Airgenix/Airgenix/notebooks/modeling/model_training_and_testing.ipynb:1273-1286`
- Confusion matrix is computed and plotted:
  - `cm = confusion_matrix(y_test, y_pred)`
  - Evidence: `.../model_training_and_testing.ipynb:1295-1303`
- Persisted summary metrics in model artifact:
  - test_accuracy = 0.9225815549497038
  - f1_score = 0.9229381756607735
  - precision = 0.9290490156604072
  - recall = 0.9225815549497038
  - Evidence: `/home/runner/work/Airgenix/Airgenix/models/model_info.json:3-8`

### Code-inferred
- Predictions and labels are held in-memory (`best_result['predictions']`, `y_test`) for evaluation.
  - Evidence: `.../model_training_and_testing.ipynb:810,1295-1297`

### Missing / Not found
- No standalone held-out prediction CSV with `true_class` and `predicted_class`.
- No standalone textual confusion-matrix table saved as CSV/TXT.

---

## 2) 72-hour input to 72-hour forecast sequence/window generation logic and counts

### Recorded
- The checklist specifies target requirements (lookback 72h, horizon 72h), but fields are blank.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/AirGenix_Final_Submission_Data_Checklist.md:59-83`

### Code-inferred
- No forecast-window code exists in notebooks currently present.

### Missing / Not found
- No 72h sequence generation script.
- No sequence/window logs.
- No accepted/rejected window counts.
- No training/validation/test window splits for forecasting.

---

## 3) Ten-class label-generation logic, counts, and accepted/rejected/ambiguous/incomplete evidence counts

### Recorded
- Implemented label generation is **5-class**, not ten-class:
  - Classes: Vehicular, Industrial, Agricultural, Burning, Natural
  - Scoring functions and assignment in notebook code.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/notebooks/feature_processing/final_dataset_preparation.ipynb:300-392,426-443`
- Label distribution:
  - Vehicular 42,445
  - Industrial 23,372
  - Agricultural 21,389
  - Natural 12,061
  - Burning 7,102
  - Evidence: `.../final_dataset_preparation.ipynb:417-421`
- Confidence distribution:
  - Low 60,050
  - Medium 26,418
  - High 19,901
  - Evidence: `.../final_dataset_preparation.ipynb:483-486`
- Per-class + confidence table in CSV:
  - Evidence: `/home/runner/work/Airgenix/Airgenix/datasets/data/final/label_summary.csv:1-16`

### Missing / Not found
- Ten-class taxonomy from checklist is not implemented in repository outputs.
  - Evidence (template only): `.../AirGenix_Final_Submission_Data_Checklist.md:86-102`
- Explicit counters for accepted/rejected/ambiguous/incomplete evidence not found as produced outputs.

---

## 4) AQI implementation (standard, pollutants, averaging, units, breakpoints, formula, missing handling, hourly/rolling)

### Recorded
- Dashboard threshold table includes PM2.5/PM10/NO2/CO/SO2/O3 category cutoffs.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/enviroscan_dashboard.py:294-302`
- AQI category function uses **PM2.5 only**:
  - `get_aqi_category(pm25)`
  - Evidence: `.../enviroscan_dashboard.py:341-356`
- Gauge bins also PM2.5-based.
  - Evidence: `.../enviroscan_dashboard.py:675-696`
- Units displayed in report text as `µg/m³` for pollutants.
  - Evidence: `.../enviroscan_dashboard.py:867-872`
- Missing handling:
  - PM2.5 missing -> AQI Unknown
  - Parameter/value missing -> status Unknown
  - Evidence: `.../enviroscan_dashboard.py:343-344,361-363`

### Missing / Not found
- No multi-pollutant AQI sub-index formula implementation found.
- No explicit averaging period implementation (e.g., 24h/8h AQI averaging logic).
- No rolling AQI target-generation pipeline found.

---

## 5) Observed-only, interpolated, CAMS-completed preprocessing variants and results

### Recorded
- One preprocessing path exists (imputation and cleaning logic).
  - Evidence: `/home/runner/work/Airgenix/Airgenix/notebooks/feature_processing/data_cleaning_feature_engineering.ipynb:265-318`
  - Evidence: `/home/runner/work/Airgenix/Airgenix/notebooks/feature_processing/final_dataset_preparation.ipynb:107-117`

### Missing / Not found
- No ablation outputs for observed-only vs interpolated vs CAMS-completed.
- CAMS appears only as checklist placeholders.
  - Evidence: `.../AirGenix_Final_Submission_Data_Checklist.md:240-263,411-412`

---

## 6) Country-level predictions/results

### Recorded
- Country-level section exists only as a blank checklist template.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/AirGenix_Final_Submission_Data_Checklist.md:268-276`

### Missing / Not found
- No country-level prediction result files.
- Final dataset schema does not include `country` column in header.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/datasets/data/final/enviroscan_final_dataset.csv:1`

---

## 7) Actual TFT training configuration and parameter count

### Missing / Not found
- No TFT implementation/configuration files found.
- TFT section appears only as blank checklist requirements.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/AirGenix_Final_Submission_Data_Checklist.md:353-374`

---

## 8) Baseline model configurations/results

### Recorded
- Decision Tree training/tuning and results in notebook output.
  - Evidence: `.../model_training_and_testing.ipynb:834-854,860-891`
- Random Forest tuning and results.
  - Evidence: `.../model_training_and_testing.ipynb:912-932,938-973`
- XGBoost tuning and results.
  - Evidence: `.../model_training_and_testing.ipynb:994-1014,1021-1063`
- Model comparison summary table output.
  - Evidence: `.../model_training_and_testing.ipynb:1090-1093`

### Missing / Not found
- Explicit parameter-count values per baseline are not reported.

---

## 9) Random seeds and number of runs

### Recorded
- Seed = 42 used in numpy, data split, SMOTE, CV, and model/search random_state.
  - Evidence: `.../model_training_and_testing.ipynb:74,585-590,656,756,868,948,1033,1048`

### Code-inferred
- Workflow appears as a single train/test run with CV-based hyperparameter search.

### Missing / Not found
- No repeated independent-run table with multiple seeds and variance reporting.

---

## 10) Software environment and hardware

### Recorded
- Python/package requirements listed.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/requirements.txt:5-35`
- Notebook kernel metadata shows Python 3.11.8.
  - Evidence: `.../model_training_and_testing.ipynb:1572-1586`
  - Evidence: `.../final_dataset_preparation.ipynb:656-662`
- README prerequisite states Python 3.9+.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/README.md:56-57`

### Missing / Not found
- No explicit CPU/GPU/RAM/CUDA/cuDNN runtime hardware record.

---

## 11) Weather uncertainty / perturbation experiment

### Missing / Not found
- No synthetic perturbation or archived forecast-vs-observation experiment output files found.
- Only checklist placeholders.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/AirGenix_Final_Submission_Data_Checklist.md:416-433`

---

## 12) Integrated Gradients and attention outputs

### Missing / Not found
- No Integrated Gradients or attention-analysis outputs/code found.
- Only checklist placeholders.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/AirGenix_Final_Submission_Data_Checklist.md:437-452`

---

## 13) Actual figures

### Recorded files present
- `/home/runner/work/Airgenix/Airgenix/assets/images/CONFUSION_MATRIX- GBoost.png`
- `/home/runner/work/Airgenix/Airgenix/assets/images/MODELCOMPARISONSUMMARY_trainvstest.png`
- `/home/runner/work/Airgenix/Airgenix/assets/images/SystemArchitectureDiagram.jpg`
- `/home/runner/work/Airgenix/Airgenix/assets/images/DataFlowDiagram.jpg`
- `/home/runner/work/Airgenix/Airgenix/assets/images/MLPipelineDiagram.jpg`
- EDA images in: `/home/runner/work/Airgenix/Airgenix/datasets/data/final/`

### Referenced in report text
- Confusion matrix and model comparison references in README.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/README.md:340,352`

---

## 14) Bibliography/reference files

### Recorded
- README includes a references section with citations/URLs.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/README.md:460-469`

### Missing / Not found
- No `.bib` bibliography file found.
- No LaTeX paper source (`.tex`) found.

---

## 15) Official ICICSCS 2026 materials

### Missing / Not found
- No CFP/author-guidelines/template/submission-guideline files for ICICSCS 2026 found.
- Only checklist request section exists.
  - Evidence: `/home/runner/work/Airgenix/Airgenix/AirGenix_Final_Submission_Data_Checklist.md:515-526`

---

## Additional repository-traced artifacts

### Current project report files
- `/home/runner/work/Airgenix/Airgenix/EnviroScan_Project_Report.pdf` (binary PDF present)
- `/home/runner/work/Airgenix/Airgenix/README.md` (textual report-like narrative)
- `/home/runner/work/Airgenix/Airgenix/AirGenix_Final_Submission_Data_Checklist.md` (submission evidence checklist template)

### Dataset pipeline counts (recorded outputs)
- Combined raw-like records loaded: 978,897
  - Evidence: `/home/runner/work/Airgenix/Airgenix/notebooks/data_ingestion/AQ_weather_data_extraction_all_locations.ipynb:808`
- Transformed rows: 109,501
  - Evidence: `.../AQ_weather_data_extraction_all_locations.ipynb:1308,1400`
- Cleaned rows: 106,369
  - Evidence: `/home/runner/work/Airgenix/Airgenix/notebooks/feature_processing/data_cleaning_feature_engineering.ipynb:159-163`
- Final labeled dataset rows: 106,369
  - Evidence: `/home/runner/work/Airgenix/Airgenix/notebooks/feature_processing/final_dataset_preparation.ipynb:554-557,616`

---

## Summary status by requested artifact

- (1) Classification predictions/metrics/confusion matrix: **Partially available** (metrics and plotted confusion matrix present; standalone prediction files absent).
- (2) 72h→72h window generation and counts: **Not found**.
- (3) Ten-class labels and evidence counts: **Not found** (only 5-class implementation present).
- (4) Exact AQI standard/formula/averaging: **Partially available** (PM2.5-threshold category logic present; full AQI formula pipeline absent).
- (5) Observed/interpolated/CAMS ablation: **Not found**.
- (6) Country-level results: **Not found**.
- (7) TFT config/parameter count: **Not found**.
- (8) Baselines config/results: **Available** (DT/RF/XGB in notebook).
- (9) Random seeds and run count: **Partially available** (seed=42 usage present; repeated-run evidence absent).
- (10) Software/hardware: **Partially available** (software versions present; hardware absent).
- (11) Weather uncertainty experiment: **Not found**.
- (12) Integrated Gradients/attention outputs: **Not found**.
- (13) Figures: **Available**.
- (14) Bibliography/reference files: **Partially available** (README references; no `.bib`).
- (15) ICICSCS 2026 official material: **Not found**.
