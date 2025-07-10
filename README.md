# 🧠 EEG-Based ASD Classification Using Machine Learning and Neural Networks

This project focuses on analyzing brainwave activity in children with Autism Spectrum Disorder (ASD) during cognitive tasks. We built a complete pipeline from preprocessing EEG data to training machine learning and neural network models that classifies whether a child is ASD or typically developing (TD).

---

## 📁 Project Structure

```
EEG_Research_Project/
├── scripts/              # Preprocessing utilities
├── ml_models/            # Traditional ML models (SVM, KNN, RF, Ensemble)
├── nn_models/            # Neural network models
├── preprocessing/        # EEG data cleaning and PSD computation
├── docs/                 # Final research paper with embedded figures and tables
├── README.md             # Project overview
├── requirements.txt      # Environment setup
├── LICENSE
└── .gitignore
```

---

## 🎯 What This Project Does

This study explores how EEG signals can be used to detect ASD in children, especially during academic tasks like Block Matching, Block Sorting, and Number Matching. We extracted frequency based features using the Welch method, trained multiple models, and compared their performance.

---

## 🧒 Data and Tasks

- EEG data was collected from children aged 4–15 using the MUSE headband.
- Electrodes used: AF7, AF8, TP9, TP10
- Sample rate: 256 Hz
- Tasks performed:
  - Block Matching (BM)
  - Block Sorting (BS)
  - Number Matching (NM)

---

## ⚙️ EEG Preprocessing Steps

1. **Import CSV EEG Data** with `RAW` columns
2. **Clean Missing Values** using forward/backward fill and mean
3. **Convert to MNE Format** at 256 Hz
4. **Apply ICA** to remove noise and muscle artifacts
5. **Compute Band Power** (Delta, Theta, Alpha, Beta, Gamma) via Welch’s method
6. **Save Clean Features** to CSV for modeling
7. **Time–Frequency Analysis (TFA)** – Generated visual spectrograms from raw EEG to explore task-specific changes in power across time and frequency bands. These plots helped interpret brainwave dynamics but were not used directly as ML inputs.


---

## 🤖 Machine Learning Models

We trained and tuned the following classifiers:

- **Support Vector Machine (SVM)**
- **K-Nearest Neighbors (KNN)**
- **Random Forest (RF)**
- **Soft Voting Ensemble** (SVM + KNN + RF)

### Feature Importance:
- We used **permutation importance** across all models to find key EEG features.
- Plotted:
  - Top 2 most influential features
  - Least impactful features

### Evaluation Metrics:
- Accuracy
- Precision
- Recall
- F1-Score

---

## 🧠 Neural Network Models

Two NN models were developed using TensorFlow/Keras:

1. **Model 1** – Classifies ASD vs TD using EEG data from specific tasks
2. **Model 2** – Classifies ASD vs TD using EEG data regardless of the task (task-agnostic)

Each model is structured using fully connected layers with training curves and performance summaries.

---

## 📓 Notebooks and Scripts

```
ml_models/
├── 01_asd_vs_td_classification.ipynb — ML Model 1
├── 01_asd_vs_td_classification.py
├── 02_asd_vs_td_task_agnostic_model.ipynb — ML Model 2
└── 02_asd_vs_td_task_agnostic_model.py

nn_models/
├── 01_asd_vs_td_classification.ipynb — NN Model 1
├── 01_asd_vs_td_classification.py
├── 02_asd_vs_td_task_agnostic_model.ipynb — NN Model 2
└── 02_asd_vs_td_task_agnostic_model.py
```

---

## 🛠 How to Set Up

```bash
pip install -r requirements.txt
```

---

## 🔍 Key Findings

- Frontal brain regions (AF7, AF8) were highly important in differentiating ASD vs TD.
- Traditional ML models (especially ensemble) achieved ~92% accuracy.
- Neural networks showed consistent performance across tasks (~83%).

---

## 🔗 References

- [MNE-Python Documentation](https://mne.tools/stable/index.html)
- [Welch’s Method (SciPy)](https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.welch.html)
