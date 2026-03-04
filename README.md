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
│       ├── feature_distributions_by_activity.png
│       ├── trained_hmm_model.pkl             # Part 2 output
│       ├── training_convergence.png           # Part 2 output
│       ├── transition_matrix.png              # Part 2 output
│       ├── emission_parameters.png            # Part 2 output
│       ├── decoded_sequences_training.png     # Part 2 output
│       ├── decoded_sequences_test.png         # Part 2 output
│       ├── confusion_matrix.png               # Part 2 output
│       └── evaluation_metrics.csv             # Part 2 output
├── part1_data_preprocessing_and_features.ipynb   # Part 1: data + features
├── part2_hmm_implementation_and_evaluation.ipynb # Part 2: HMM + evaluation
├── REPORT_TEMPLATE.md                             # Report template (fill in)
└── notebooks/
    └── part1_data_preprocessing_and_features.ipynb
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
   Open and run **`part1_data_preprocessing_and_features.ipynb`** (Run All).  
   - Reads from `data/raw/raw_data/` and `data/raw/raw_data2/`.  
   - Writes to `data/processed/` (observation sequences, scaler, plots, CSV).  
   Run from repo root; paths are set up accordingly.

2. **Part 2 (HMM implementation & evaluation)**  
   Open and run **`part2_hmm_implementation_and_evaluation.ipynb`** (Run All).  
   - Loads processed data from `data/processed/` (from Part 1)
   - Implements Viterbi algorithm and Baum-Welch training from scratch
   - Trains HMM on training sequences with convergence check
   - Evaluates on unseen test data
   - Generates all visualizations and metrics (transition matrix, confusion matrix, etc.)
   - Outputs: trained model, plots, metrics CSV

3. **Report**
   Use **`REPORT_TEMPLATE.md`** as your starting point
   - Fill in placeholders with your specific results
   - Insert generated figures from `data/processed/`
   - Export as PDF and add to repository

---

## Data format (raw)

Each recording is a **folder** containing:

- `Accelerometer.csv` — columns: `time`, `seconds_elapsed`, `x`, `y`, `z`
- `Gyroscope.csv` — same columns

Folder name implies activity (e.g. `standing_1-2026-03-03_08-40-50`, `walking_2`).  
At least **50 recordings** across the four activities; ≥1.5 min total per activity.

---

## Submission (project checklist)

- [ ] GitHub repo with complete structure
- [ ] Filled and exported PDF report (use REPORT_TEMPLATE.md)
- [ ] `data/raw/` with well-labelled CSV dataset (50 files)
- [ ] Part 1 notebook: `part1_data_preprocessing_and_features.ipynb`
- [ ] Part 2 notebook: `part2_hmm_implementation_and_evaluation.ipynb`
- [ ] All visualizations in `data/processed/`:
  - [ ] sample_data_per_activity.png
  - [ ] feature_distributions_by_activity.png
  - [ ] training_convergence.png
  - [ ] transition_matrix.png
  - [ ] emission_parameters.png
  - [ ] decoded_sequences_training.png
  - [ ] decoded_sequences_test.png
  - [ ] confusion_matrix.png
- [ ] evaluation_metrics.csv with sensitivity/specificity/accuracy table
- [ ] Task allocation table in report showing balanced contribution
- [ ] Balanced GitHub commit history (~50% each member)
