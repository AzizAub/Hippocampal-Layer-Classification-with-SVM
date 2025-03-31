# Hippocampal Layer Classification with SVM

This repository provides an implementation of a Support Vector Machine (SVM) pipeline for classifying hippocampal neural signals into distinct anatomical layers: Stratum Oriens (SO), Stratum Pyramidale (SP), Stratum Radiatum (SR), and Stratum Lacunosum-Moleculare (SLM). The classifier utilizes features extracted from theta-filtered LFP signals using Continuous Wavelet Transform (CWT), followed by dimensionality reduction with Principal Component Analysis (PCA).

## Overview

Accurate identification of hippocampal layers is crucial for neuroscience research and potential clinical applications. Our model was trained exclusively on wild-type (WT) mouse data and achieved:
- **97% accuracy** on validation data from WT mice.
- **66% accuracy** on external data, highlighting the need for model generalization.

To improve this tool, we invite contributions of hippocampal theta-filtered LFP recordings for retraining and expanding the robustness of the model.

---

## Repository Structure

```
.
├── main.py               # Training pipeline: CWT -> PCA -> SVM + saving models
├── Checker.py            # Classification script for external .mat data using pretrained models
├── pca_modelHLayers_without_TG_data.joblib
├── scaler_modelHLayers_without_TG_data.joblib
├── svm_modelHLayers_without_TG_data.joblib
├── requirements.txt      # Python dependencies
└── README.md             # This file
```

---

## Usage Instructions

### 1. Prepare Your Data

- Your data should be stored in `.mat` files and contain a key `'thetaeeg'` with a 1D array representing the theta-filtered LFP signal.
- Recommended: Extract theta frequency band using MATLAB and save to `.mat` format.

### 2. Check Data Using Pretrained Model

Run:
```bash
python Checker.py
```

This script loads:
- `pca_modelHLayers_without_TG_data.joblib`
- `scaler_modelHLayers_without_TG_data.joblib`
- `svm_modelHLayers_without_TG_data.joblib`

It processes each `.mat` file in the target directory, extracts features via CWT, reduces them with PCA, normalizes with the saved scaler, and predicts the hippocampal layer label per window.

### 3. Train the Model (Optional)

To train the model on new data, modify the `DATA_DIR` in `main.py` and run:

```bash
python main.py
```

---

## Requirements

Install required Python packages with:

```bash
pip install -r requirements.txt
```

`requirements.txt`:
```
numpy
scipy
scikit-learn
matplotlib
pywt
joblib
seaborn
```

---

## Contribution

We welcome contributions from the neuroscience and machine learning community. To enhance the model's robustness and generalizability, please contribute theta-filtered LFP signals (in `.mat` format) labeled by hippocampal layer. This will help advance research and enable earlier, more precise investigations into disorders such as RASopathies.