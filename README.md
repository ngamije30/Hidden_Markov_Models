# Modeling Human Activity States Using Hidden Markov Models

Motion data (accelerometer + gyroscope) is collected, preprocessed, and turned into observation sequences for a Hidden Markov Model that infers activity states: **standing**, **walking**, **jumping**, **still**.

---

## Repository structure

```
Hidden_Markov_Models/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── raw/                    # Raw sensor recordings (Sensor Logger CSV)
│   │   ├── raw_data/           # Member 1 recordings (activity_timestamp/)
│   │   └── raw_data2/          # Member 2 recordings (activity_n/)
│   └── processed/              # Part 1 outputs (run notebook to generate)
│       ├── train_observation_sequences.pkl
│       ├── test_observation_sequences.pkl
│       ├── scaler.pkl
│       ├── feature_names.npy
│       ├── activity_to_id.npy
│       ├── cleaned_labeled_windows.csv
│       ├── sample_data_per_activity.png
│       └── feature_distributions_by_activity.png
├── notebooks/
│   └── part1_data_preprocessing_and_features.ipynb   # Part 1: data + features
└── docs/
    ├── DATA_COLLECTION.md       # Report: phones, sampling rates, harmonization
    └── REPORT_SECTIONS_PART1.md # Report: copy-paste text for Part 1 sections
```

---

## Setup

From the **repository root**:

```bash
pip install -r requirements.txt
```

(Use the same Python environment as your Jupyter/Cursor kernel.)

---

## How to run

1. **Part 1 (data + features)**  
   Open and run **`notebooks/part1_data_preprocessing_and_features.ipynb`** (Run All).  
   - Reads from `data/raw/raw_data/` and `data/raw/raw_data2/`.  
   - Writes to `data/processed/` (observation sequences, scaler, plots, CSV).  
   Run from repo root or from `notebooks/`; paths are set up for both.

2. **Part 2 (HMM)**  
   Use the pickles and arrays in `data/processed/` to train and evaluate the HMM (Viterbi, Baum–Welch, metrics on unseen test data).

---

## Data format (raw)

Each recording is a **folder** containing:

- `Accelerometer.csv` — columns: `time`, `seconds_elapsed`, `x`, `y`, `z`
- `Gyroscope.csv` — same columns

Folder name implies activity (e.g. `standing_1-2026-03-03_08-40-50`, `walking_2`).  
At least **50 recordings** across the four activities; ≥1.5 min total per activity.

---

## Submission (project checklist)

- [ ] GitHub repo with this structure
- [ ] Filled and exported PDF form (link from instructions) in repo
- [ ] `data/raw/` (or a clear pointer) with well-labelled CSV dataset
- [ ] Python notebook(s) implementing HMM (Part 1 + Part 2)
- [ ] Short report (4–5 pages) with background, data/preprocessing, HMM setup, results, discussion
- [ ] Task allocation table and balanced commit history
