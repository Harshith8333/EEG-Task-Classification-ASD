# 🧠 EEG Research Project: Cognitive Task Classification in ASD

This repository contains the full pipeline for an EEG-based research project focused on **power spectral analysis**, **machine learning**, and **neural network classification** to distinguish cognitive tasks and ASD profiles.

---

## 📂 Folder Structure

```
EEG_Research_Project/

bash
Copy
Edit
EEG_Research_Project/
├── Scripts/                              # Python scripts for preprocessing
│   └── eeg_preprocessing_pipeline.py
│
├── ml_models/                            # Traditional ML models (SVM, KNN, RF, Ensemble)
│   ├── 01_asd_vs_td_classification.ipynb
│   ├── 01_asd_vs_td_classification.py
│   ├── 02_asd_vs_td_task_agnostic_model.ipynb
│   └── 02_asd_vs_td_task_agnostic_model.py
│
├── nn_models/                            # Neural Network versions of the same models
│   ├── 01_asd_vs_td_classification.ipynb
│   ├── 01_asd_vs_td_classification.py
│   ├── 02_asd_vs_td_task_agnostic_model.ipynb
│   └── 02_asd_vs_td_task_agnostic_model.py
│
├── preprocessing/                        # EEG data cleaning and noise removal
│   └── eeg_preprocessing_pipeline.ipynb
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
- Includes machine learning models (SVM, KNN, RF, and Ensemble) for:
  - Classifying participants (ASD vs TD) using task-specific features
  - Predicting ASD vs TD using task-agnostic EEG input (data from any task)
- Neural network models are under development for both use cases above.

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

## 🤖 Machine Learning Pipeline (ASD vs TD Classification)

1. **Data Loading** – Features loaded from preprocessed EEG tables
2. **Train-Test Split** – Stratified sampling with validation
3. **Feature Scaling** – Using `StandardScaler`

4. **Modeling Techniques**:
   - Support Vector Machine (SVM)
   - K-Nearest Neighbors (KNN)
   - Random Forest (RF)
   - VotingClassifier Ensemble (SVM + RF + KNN)

5. **Hyperparameter Tuning**:
   - KNN: Optimal `k` selected through manual accuracy comparison
   - SVM: Tuned kernel (`linear`, `rbf`) and regularization parameter `C`
   - Random Forest: Tuned `n_estimators`, `max_depth`, and `criterion`
   - Ensemble: Implemented **soft voting** using the best-performing base classifiers

6. **Best Feature Identification**:
   - Feature importances were calculated using **permutation importance**
   - Applied across all classifiers (SVM, KNN, RF) to measure accuracy drop when features were shuffled

7. **Visualizations**:
   -  Bar plot of the **top 2 most important EEG features** (from permutation importance)
   -  Bar plot of the **least 2 important EEG features** (from permutation importance)


8. **Evaluation Metrics**:
   - Accuracy, Precision, Recall, and F1-score using `classification_report`
   - Compared across all models to select the best-performing classifier

Notebooks:
- [`01_asd_vs_td_classification.ipynb`](ml_models/01_asd_vs_td_classification.ipynb) – Classifies ASD vs TD using EEG data
- [`02_asd_vs_td_task_agnostic_model.ipynb`](ml_models/02_asd_vs_td_task_agnostic_model.ipynb) – Predicts ASD vs TD using task-agnostic EEG input

---

## 🛠️ Requirements

Install dependencies:
```bash
pip install -r requirements.txt
```

---

## 🚀 Future Work

- Add two neural network models:
  1. **NN Model 1**: ASD vs TD classification using task-specific EEG features
  2. **NN Model 2**: ASD vs TD classification using EEG data from any task (task-agnostic binary model)
- Expand hyperparameter optimization and model comparison
- Visualize time-frequency features and statistical comparisons

---

## 🔗 References

- [MNE-Python Documentation](https://mne.tools/stable/index.html)
- [Welch’s Method](https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.welch.html)
