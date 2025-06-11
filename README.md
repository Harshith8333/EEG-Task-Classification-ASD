# 🧠 EEG Research Project: Cognitive Task Classification in ASD

This repository contains the full pipeline for an EEG-based research project focused on **power spectral analysis** and **machine learning classification** to distinguish cognitive tasks and ASD profiles.

---

## 📂 Folder Structure

```
EEG_Research_Project/
├── figures/              # Visual outputs (e.g., PSD plots, scalp maps)
├── ml_models/            # Placeholder for ML/NN models (to be added)
├── preprocessing/        # EEG preprocessing notebooks
│   └── ATM3_clean_final.ipynb
├── scripts/              # Python scripts for preprocessing and feature extraction
│   └── eeg_preprocessing_and_features.py
├── tables/               # CSVs with extracted features and results
├── README.md             # Project overview and structure
├── requirements.txt      # Dependencies
├── LICENSE               # Usage license
└── .gitignore            # Git exclusions
```

---

## 🎯 Project Summary

This project involves:
- Preprocessing EEG data collected via MUSE headset.
- Extracting power spectral features (Delta, Theta, Alpha, Beta, Gamma) using **Welch’s method**.
- Future steps include training ML & Neural Network models to:
  - Classify participants (ASD vs TD)
  - Predict cognitive tasks (Block Matching, Sorting, Number Matching)

---

## 🔬 EEG Preprocessing Pipeline

The EEG preprocessing pipeline involves the following steps:

1. **Raw EEG Loading** – Read multiple CSV files containing `RAW_` EEG columns
2. **NaN and Inf Handling** – Use forward-fill, backward-fill, and mean replacement for missing data
3. **Conversion to MNE Format** – Create `RawArray` using MNE with 256 Hz sampling
4. **Artifact Handling via ICA** – Use Independent Component Analysis to detect and remove muscle artifacts using high-frequency PSD checks
5. **Power Spectral Density Calculation** – Apply Welch’s method to compute absolute band power across Delta, Theta, Alpha, Beta, and Gamma bands
6. **Export to CSV** – Save averaged power features per file for downstream ML/NN use

---

## 🛠️ Requirements

Install dependencies:
```bash
pip install -r requirements.txt
```

---

## 🚀 Future Work

- Implement and upload machine learning (SVM, KNN, RF) and ensemble models
- Develop neural network models for multi-class classification
- Add performance dashboards (accuracy, confusion matrix, ROC curves)

---

## 🔗 References

- [MNE-Python Documentation](https://mne.tools/stable/index.html)
- [Welch’s Method](https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.welch.html)
