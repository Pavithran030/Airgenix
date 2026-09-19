# AIRGENIX – FINAL SUBMISSION DATA COLLECTION CHECKLIST

> **Purpose:** Collect the actual experiment files, logs, predictions, configurations, and metadata required to make the AirGenix paper fully reproducible and submission-ready.
>
> **Important:** Do not estimate or invent values. If an experiment was not performed, write **NOT PERFORMED**. If a value is unknown, write **UNKNOWN**.

## Recommended ZIP Structure

```text
AirGenix/
├── data/
├── preprocessing/
├── labels/
├── predictions/
├── experiments/
├── models/
├── logs/
├── results/
├── figures/
├── notebooks/
├── requirements.txt
├── environment.yml
├── references.bib
└── current_paper.tex
```

---

## 1. Dataset and Preprocessing

Provide actual preprocessing logs, scripts, and outputs.

- [ ] Total raw observations: ______________________________
- [ ] After duplicate removal: _____________________________
- [ ] After quality control: _______________________________
- [ ] Number of stations/locations: ________________________
- [ ] Number of countries: _________________________________
- [ ] Dataset start date: __________________________________
- [ ] Dataset end date: ____________________________________
- [ ] Sampling frequency: _________________________________
- [ ] Duplicate-removal rule: ______________________________
- [ ] Invalid-value rule: __________________________________
- [ ] Missing-value policy: ________________________________
- [ ] Interpolation method: ________________________________
- [ ] Maximum interpolation gap: ___________________________
- [ ] CAMS completion method: ______________________________
- [ ] CAMS used for: [ ] Training [ ] Validation [ ] Test [ ] All [ ] Other

### Required Files

- [ ] Preprocessing script
- [ ] Preprocessing log
- [ ] Cleaned dataset/sample
- [ ] Provenance mask/file
- [ ] Configuration file

---

## 2. 72-Hour Lookback + 72-Hour Forecast Window

- [ ] Lookback: **72 hours**
- [ ] Forecast horizon: **72 hours**
- [ ] Forecast stride: _________________________________
- [ ] Overlapping windows? [ ] Yes [ ] No
- [ ] Minimum valid input observations: __________________
- [ ] Minimum valid target observations: _________________
- [ ] Gap handling: ____________________________________
- [ ] Candidate windows: ________________________________
- [ ] Accepted windows: _________________________________
- [ ] Rejected windows: _________________________________
- [ ] Classification windows: ____________________________
- [ ] Forecasting windows: ______________________________
- [ ] Training windows: _________________________________
- [ ] Validation windows: _______________________________
- [ ] Test windows: ____________________________________

### Required Files

- [ ] Sequence-generation script
- [ ] Sequence/window log
- [ ] Window-count output
- [ ] Sequence metadata

---

## 3. Ten-Class Label Generation

Provide actual label-generation code and configuration.

| Class | Count |
|---|---:|
| Vehicular_Traffic | __________ |
| Vehicular_Aviation | __________ |
| Industrial_Heavy | __________ |
| Industrial_Light | __________ |
| Power_Generation | __________ |
| Agricultural_Crop | __________ |
| Agricultural_Animal | __________ |
| Waste_Burning | __________ |
| Construction | __________ |
| Natural | __________ |

- [ ] Total quality-controlled observations: ______________
- [ ] Complete-evidence observations: _____________________
- [ ] Accepted labeled observations: ______________________
- [ ] Rejected observations: ______________________________
- [ ] Ambiguous observations: _____________________________
- [ ] Incomplete-evidence observations: ___________________

### Label Rules

- [ ] Exact threshold for each class
- [ ] Pollutant-ratio thresholds
- [ ] Distance thresholds
- [ ] Temporal conditions
- [ ] Weather conditions
- [ ] Missing-evidence rule
- [ ] Contradictory-evidence rule
- [ ] Tie-breaking rule
- [ ] Hourly vs. sequence-level labeling

### Required Files

- [ ] Label-generation script
- [ ] Label configuration
- [ ] Label counts
- [ ] Labeled dataset/sample
- [ ] Label audit log

---

## 4. Label Validation / Manual Review

### If Performed

- [ ] Number manually reviewed: __________________________
- [ ] Sampling method: ___________________________________
- [ ] Number of reviewers: ________________________________
- [ ] Reviewer expertise: _________________________________
- [ ] Agreement percentage: ______________________________
- [ ] Cohen's kappa: _____________________________________
- [ ] Adjudication procedure: _____________________________

### If Not Performed

- [ ] **NOT PERFORMED**

### Required Files

- [ ] Validation sample
- [ ] Reviewer results
- [ ] Agreement calculation

---

## 5. AQI Implementation

Provide the **exact AQI implementation used**.

- [ ] AQI standard: _______________________________________
- [ ] Issuing organization: _______________________________
- [ ] Standard/version/year: ______________________________
- [ ] Pollutants used: ____________________________________
- [ ] Averaging period for each pollutant: _______________
- [ ] Input units: ________________________________________
- [ ] Unit conversion: ___________________________________
- [ ] Breakpoint table: __________________________________
- [ ] AQI formula: _______________________________________
- [ ] Missing pollutant handling: _________________________
- [ ] Minimum pollutant requirement: ______________________
- [ ] Target: [ ] Hourly AQI [ ] Rolling-window AQI [ ] Other
- [ ] Future values used during preprocessing? [ ] Yes [ ] No

### Required Files

- [ ] AQI calculation code
- [ ] AQI configuration
- [ ] Breakpoint table
- [ ] AQI sample output

---

## 6. Classification Predictions

Upload actual held-out predictions.

### Preferred Columns

```text
window_id, station_id, country, timestamp, true_class,
predicted_class, class probabilities
```

- [ ] Prediction file: _________________________________
- [ ] Ground-truth file: _______________________________

### Verify

- [ ] Accuracy
- [ ] Precision
- [ ] Recall
- [ ] Macro F1
- [ ] Weighted F1
- [ ] Per-class Precision
- [ ] Per-class Recall
- [ ] Per-class F1
- [ ] Confusion Matrix
- [ ] Class support

---

## 7. AQI Forecast Predictions

### Preferred Columns

```text
window_id, station_id, country, forecast_origin,
target_timestamp, horizon, actual_AQI, predicted_AQI
```

- [ ] 24-hour predictions
- [ ] 48-hour predictions
- [ ] 72-hour predictions

| Forecast horizon | MAE | RMSE |
|---|---:|---:|
| 24 hours | __________ | __________ |
| 48 hours | __________ | __________ |
| 72 hours | __________ | __________ |

### Required Files

- [ ] AQI prediction file
- [ ] Ground-truth file
- [ ] Evaluation script
- [ ] Evaluation output

---

## 8. Preprocessing Ablation – Very Important

Run the same evaluation for:

- **A. OBSERVED-ONLY**
- **B. INTERPOLATED**
- **C. CAMS-COMPLETED**

| Metric | Observed-only | Interpolated | CAMS-completed |
|---|---:|---:|---:|
| Observations | __________ | __________ | __________ |
| Windows | __________ | __________ | __________ |
| Accuracy | __________ | __________ | __________ |
| Macro F1 | __________ | __________ | __________ |
| Weighted F1 | __________ | __________ | __________ |
| 24h MAE | __________ | __________ | __________ |
| 24h RMSE | __________ | __________ | __________ |
| 48h MAE | __________ | __________ | __________ |
| 48h RMSE | __________ | __________ | __________ |
| 72h MAE | __________ | __________ | __________ |
| 72h RMSE | __________ | __________ | __________ |

- [ ] **NOT PERFORMED**

> Do not invent values.

---

## 9. Country-Level Results

Only provide values if actual country-level predictions exist.

| Country | Test windows | Accuracy | Macro F1 | Weighted F1 | 24h MAE/RMSE | 48h MAE/RMSE | 72h MAE/RMSE |
|---|---:|---:|---:|---:|---|---|---|
| __________________ | __________ | __________ | __________ | __________ | __________ | __________ | __________ |

- [ ] **NOT PERFORMED**

> The paper will then avoid country-held-out/global-generalization claims.

---

## 10. Continental Results

Only provide values from actual predictions.

| Continent | Windows | Accuracy | Macro F1 |
|---|---:|---:|---:|
| Asia | ______ | ______ | ______ |
| Europe | ______ | ______ | ______ |
| North America | ______ | ______ | ______ |
| South America | ______ | ______ | ______ |
| Africa/Oceania | ______ | ______ | ______ |

- [ ] **NOT PERFORMED / NOT AVAILABLE**

---

## 11. Architectural Ablation

Complete one row or record for every experiment.

| Model/configuration | Parameters | Seed | Accuracy | Macro F1 | Weighted F1 | MAE | RMSE | Epochs | Training time |
|---|---|---|---:|---:|---:|---:|---:|---:|---|
| __________________ | __________ | ______ | ______ | ______ | ______ | ______ | ______ | ______ | ______ |

### Required Files

- [ ] Ablation results
- [ ] Configurations
- [ ] Logs

---

## 12. Baseline Models

Complete the following information for every baseline.

- **Model:** _____________________________________
- **Implementation/library:** _____________________
- **Version:** ____________________________________
- **Hyperparameters:** ____________________________
- **Learning rate:** ______________________________
- **Batch size:** _________________________________
- **Epochs:** ____________________________________
- **Optimizer:** __________________________________
- **Scheduler:** __________________________________
- **Early stopping:** _____________________________
- **Random seed:** ________________________________
- **Input features:** _____________________________
- **Sequence length:** ____________________________
- **Forecast horizon:** ___________________________
- **Parameter count:** ____________________________

---

## 13. Random Seeds and Repeated Runs

- **Number of independent runs:** __________________
- **Random seeds:** _______________________________

| Run | Seed | Best epoch | Validation | Test |
|---|---:|---:|---:|---:|
| Run 1 | ______ | ______ | ______ | ______ |
| Run 2 | ______ | ______ | ______ | ______ |
| Run 3 | ______ | ______ | ______ | ______ |

- [ ] **SINGLE RUN**

> Do not report mean ± standard deviation unless multiple independent runs actually exist.

---

## 14. TFT Model Configuration

- **Hidden dimension:** ____________________________
- **LSTM layers:** _________________________________
- **Attention heads:** _____________________________
- **Dropout:** ____________________________________
- **Embedding dimensions:** _______________________
- **Static feature dimension:** ___________________
- **Temporal feature dimension:** _________________
- **Optimizer:** __________________________________
- **Learning rate:** ______________________________
- **Weight decay:** _______________________________
- **Batch size:** _________________________________
- **Maximum epochs:** _____________________________
- **Early stopping patience:** ____________________
- **Loss function:** ______________________________
- **Quantile levels:** ____________________________
- **Output dimension:** ___________________________
- **Total parameter count:** ______________________
- **Classification head:** ________________________
- **Forecasting head:** ___________________________

---

## 15. Software / Hardware

- **Python:** _____________________________________
- **PyTorch:** ____________________________________
- **TensorFlow (if used):** _______________________
- **NumPy:** ______________________________________
- **Pandas:** _____________________________________
- **Scikit-learn:** _______________________________
- **PyTorch Lightning (if used):** ________________
- **CUDA:** _______________________________________
- **cuDNN:** ______________________________________
- **Operating system:** ___________________________
- **CPU:** ________________________________________
- **GPU:** ________________________________________
- **GPU VRAM:** ___________________________________
- **RAM:** ________________________________________

### Best Option

- [ ] `requirements.txt`
- [ ] `environment.yml`
- [ ] `pip freeze` output

---

## 16. Data Source Versions

- **OpenAQ API/version:** __________________________
- **OpenAQ retrieval date:** _______________________
- **Open-Meteo version/source:** ___________________
- **Open-Meteo retrieval date:** ___________________
- **OpenStreetMap retrieval date:** _________________
- **Overpass retrieval date:** ______________________
- **Nominatim retrieval date:** _____________________
- **CAMS dataset/product/version:** _________________
- **CAMS retrieval date:** __________________________

---

## 17. Weather Forecast Uncertainty

### Synthetic Perturbation

- **Variables:** ___________________________________
- **Perturbation:** [ ] ±10% [ ] ±20% [ ] Other
- **Random seed:** _________________________________
- **Number of repetitions:** _______________________
- **Results:** _____________________________________

### Real Archived Forecast-vs-Observation Validation

- [ ] YES
- [ ] NO

If YES, upload forecast and observation files.

---

## 18. Attribution Analysis

### Integrated Gradients

- [ ] Performed
- [ ] Not performed
- **Baseline:** ___________________________________
- **Number of test samples:** _____________________
- **Aggregation method:** _________________________
- **Results:** ____________________________________

### Attention Analysis

- [ ] Performed
- [ ] Not performed
- **Extraction method:** __________________________
- **Aggregation method:** _________________________

> Attribution will be described as predictive/model diagnostics, not causal evidence.

---

## 19. Figures

Upload original high-resolution figures.

- [ ] System architecture
- [ ] Methodology flowchart
- [ ] Data pipeline
- [ ] Confusion matrix
- [ ] Forecast vs. observed plot
- [ ] Geographic map
- [ ] Ablation chart
- [ ] Other: ______________________

**Preferred formats:** PDF / EPS / SVG / PNG at 300+ DPI.

### Figure Verification

For every figure:

- [ ] Correct labels
- [ ] Correct units
- [ ] Correct legend
- [ ] Correct caption
- [ ] Correct numbering
- [ ] Matches actual data
- [ ] Readable in IEEE two-column format

---

## 20. References

### Upload

- [ ] `references.bib`
- [ ] Current bibliography
- [ ] Zotero export
- [ ] EndNote export

### Verify

- [ ] Authors
- [ ] Title
- [ ] Year
- [ ] Journal/conference
- [ ] Volume/issue
- [ ] Pages/article number
- [ ] DOI
- [ ] URL
- [ ] OpenAQ reference
- [ ] Open-Meteo reference
- [ ] OpenStreetMap reference
- [ ] CAMS reference
- [ ] TFT reference
- [ ] Baseline references
- [ ] AQI reference

---

## 21. ICICSCS 2026 Official Material

Upload the latest versions of:

- [ ] CFP
- [ ] Author guidelines
- [ ] Paper template
- [ ] Submission guidelines
- [ ] IEEE template supplied by the conference
- [ ] Copyright instructions
- [ ] AI policy, if separately provided

---

## 22. Final Author Information

- **Paper title:** _________________________________
- **Author 1:** ___________________________________
- **Author 2:** ___________________________________
- **Author 3:** ___________________________________
- **Author order confirmed:** [ ] YES
- **Department:** __________________________________
- **Institution:** _________________________________
- **City:** _______________________________________
- **Country:** ____________________________________
- **Email addresses:** _____________________________
- **ORCID (if required):** _________________________

> Do not change the title or author order unless explicitly requested.

---

## 23. Generative-AI Usage

Select what actually happened:

- [ ] AI used only for grammar/language correction
- [ ] AI used to restructure/rewrite manuscript text
- [ ] AI generated technical text
- [ ] AI generated code
- [ ] AI generated figures
- [ ] AI assisted with data analysis
- [ ] Multiple of the above

- **AI system/tool:** ______________________________
- **Sections/content affected:** ___________________
- **Description:** _________________________________

> The final disclosure must accurately describe actual AI use.

---

## 24. Master File Checklist

- [ ] Current LaTeX
- [ ] References
- [ ] Dataset / representative data
- [ ] Preprocessing scripts
- [ ] Preprocessing logs
- [ ] Sequence-generation script
- [ ] Sequence/window counts
- [ ] Label-generation script
- [ ] Label counts
- [ ] Label audit
- [ ] Classification predictions
- [ ] Classification ground truth
- [ ] AQI predictions
- [ ] AQI ground truth
- [ ] Provenance masks
- [ ] Observed-only results
- [ ] Interpolated results
- [ ] CAMS-completed results
- [ ] Country-level predictions/results
- [ ] Continental results
- [ ] Architectural ablations
- [ ] Baseline results
- [ ] Training logs
- [ ] Random seeds
- [ ] Model configuration
- [ ] `requirements.txt`
- [ ] `environment.yml` / `pip freeze`
- [ ] Figures
- [ ] Reference database
- [ ] ICICSCS 2026 guidelines
- [ ] AI-use information

---

## 25. Final Verification I Will Perform

- [ ] Every abstract number matches saved results
- [ ] Every table number matches saved results
- [ ] Every figure matches saved results
- [ ] Exact sequence-window count
- [ ] Exact ten-class counts
- [ ] Rejected/ambiguous/incomplete counts
- [ ] Exact AQI standard
- [ ] AQI averaging periods
- [ ] AQI units
- [ ] AQI breakpoints
- [ ] AQI missing-value policy
- [ ] Observed/interpolated/CAMS ablation
- [ ] Country metrics if available
- [ ] No unsupported global-generalization claim
- [ ] Baseline hyperparameters
- [ ] Random seeds
- [ ] Repeated-run statistics if available
- [ ] Software versions
- [ ] Hardware details
- [ ] Model parameter count
- [ ] Attribution wording
- [ ] Reference verification
- [ ] Equation/variable consistency
- [ ] Figure quality
- [ ] IEEE/ICICSCS formatting
- [ ] Six-page target
- [ ] No overfull boxes
- [ ] No clipped figures
- [ ] No clipped tables
- [ ] No unresolved references
- [ ] Correct headers/footers
- [ ] Correct author block
- [ ] Correct title
- [ ] Correct AI disclosure

---

## 26. What to Do Now

### Step 1
Collect the actual experiment files and logs.

### Step 2
Put them into one folder.

### Step 3
Zip the complete folder.

### Step 4
Upload the ZIP here.

### Step 5
Calculate and verify the missing scientific results.

### Step 6
Update the LaTeX without inventing experimental values.

### Step 7
Compile and inspect the final paper.

### Step 8
Provide:

1. Final `.tex`
2. Final compiled PDF
3. Final verification checklist
4. Any remaining unresolved items

---

## Final Rule

> If an experiment was not performed, report **NOT PERFORMED**. Never create a value just to satisfy a reviewer.
