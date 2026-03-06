# Human Activity Recognition with Hidden Markov Models

A complete implementation of human activity recognition using Hidden Markov Models (HMMs) with smartphone sensor data (accelerometer and gyroscope).

## 👥 Team Members

- **Part 1** (Data Collection, Preprocessing, Feature Extraction): Jade ISIMBI TUZINDE
- **Part 2** (HMM Implementation, Viterbi, Baum-Welch, Evaluation): Davy NGAMIJE RUHUMULIZA

## 📋 Project Overview

This project implements a complete pipeline for recognizing human activities from smartphone sensor data using Hidden Markov Models. The system can classify four distinct activities:

- **Standing**
- **Walking** 
- **Jumping**
- **Still** (stationary)

### Key Features

✅ **Data preprocessing** with sensor fusion (accelerometer + gyroscope)  
✅ **Feature extraction** from time and frequency domains  
✅ **HMM implementation from scratch** (Viterbi & Baum-Welch algorithms)  
✅ **Supervised initialization** from labeled training data  
✅ **Covariance regularization** for numerical stability  
✅ **Complete evaluation** with confusion matrices and metrics  

## 🗂️ Project Structure

```
Hidden_Markov_Models/
├── notebooks/
│   ├── activity_recognition.ipynb          # Complete pipeline (Part 1 + Part 2)
│   └── part2_hmm_implementation_and_evaluation.ipynb  # Standalone Part 2
├── data/
│   ├── raw/                                # Raw sensor data (CSV files)
│   │   ├── raw_data/                       # Training data recordings
│   │   └── raw_data2/                      # Test data recordings
│   └── processed/                          # Preprocessed data and outputs
│       ├── train_observation_sequences.pkl
│       ├── test_observation_sequences.pkl
│       ├── trained_hmm_model.pkl
│       ├── feature_names.npy
│       ├── activity_to_id.npy
│       └── *.png                           # Visualizations
├── requirements.txt
└── README.md
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- Jupyter Notebook

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/ngamije30/Hidden_Markov_Models.git
   cd Hidden_Markov_Models
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the notebook**
   ```bash
   jupyter notebook notebooks/activity_recognition.ipynb
   ```

## 📊 Pipeline Overview

### Part 1: Data Collection & Feature Extraction

1. **Data Loading**
   - Load accelerometer and gyroscope CSV files
   - Merge sensor data by timestamp
   - Resample to target frequency (50 Hz)

2. **Windowing**
   - Sliding window approach (2-second windows, 50% overlap)
   - Extract features per window

3. **Feature Engineering**
   - **Time domain**: mean, variance, std, signal magnitude area (SMA), correlations
   - **Frequency domain**: FFT-based features (dominant frequency, spectral energy)
   - **Total**: 29-41 features per window

4. **Train/Test Split**
   - Stratified split by activity
   - Ensure all 4 activities represented

5. **Normalization**
   - Z-score standardization
   - Fit on training data only

### Part 2: HMM Implementation & Evaluation

1. **Model Architecture**
   - **States**: 4 hidden states (one per activity)
   - **Observations**: Feature vectors from Part 1
   - **Emissions**: Multivariate Gaussian per state

2. **Algorithms Implemented**
   - **Viterbi**: Find most likely state sequence (O(T·N²) complexity)
   - **Baum-Welch (EM)**: Parameter learning with convergence criterion (|ΔLL| < 1e-4)
   - **Forward-Backward**: Compute state occupation probabilities

3. **Key Implementation Features**
   - Supervised initialization from labeled data
   - Covariance regularization (ε·I) for numerical stability
   - Log-space computation to prevent underflow
   - Configurable hyperparameters (max_iter, tolerance)

4. **Evaluation Metrics**
   - Confusion matrix (4×4)
   - Accuracy, sensitivity, specificity per activity
   - Training convergence plots
   - Decoded sequence visualizations

## 📈 Results

The trained HMM model achieves robust performance on unseen test data:

- **Evaluation**: Confusion matrix showing classification accuracy across all 4 activities
- **Convergence**: Typical convergence in 7-15 iterations
- **Visualizations**: 
  - Training log-likelihood convergence
  - Transition probability matrix
  - Emission parameters per state
  - Decoded sequences (training & test)
  - Confusion matrix heatmap

All output visualizations are saved to `data/processed/`.

## 🔬 Technical Details

### HMM Parameters

- **Transition Matrix (A)**: 4×4 matrix of state transition probabilities
- **Emission Parameters (B)**: Gaussian (μ, Σ) per state
- **Initial Probabilities (π)**: Starting state distribution

### Training Configuration

- **Initialization**: Supervised from labeled data statistics
- **Max iterations**: 100
- **Convergence tolerance**: 1e-4 (log-likelihood change)
- **Regularization**: ε = 1e-6 added to covariances

### Feature Set

- Accelerometer: mean (x,y,z), variance (x,y,z), std, SMA, correlations
- Gyroscope: mean (x,y,z), variance (x,y,z), std, SMA
- FFT: dominant frequency, spectral energy (per axis)

## 📁 Data Files

### Input
- `raw_data/` and `raw_data2/`: Raw sensor recordings (Accelerometer.csv, Gyroscope.csv)

### Output
- `train_observation_sequences.pkl`: Training sequences [(observations, labels), ...]
- `test_observation_sequences.pkl`: Test sequences [(observations, labels), ...]
- `trained_hmm_model.pkl`: Trained HMM model
- `feature_names.npy`: List of feature names
- `activity_to_id.npy`: Activity name to ID mapping
- `evaluation_metrics.csv`: Per-activity performance metrics
- `*.png`: Visualization plots

## 🛠️ Implementation Notes

- **From scratch**: HMM algorithms implemented using NumPy (no hmmlearn)
- **Modularity**: Clean GaussianHMM class with docstrings
- **Numerical stability**: Log-space computation, normalization, regularization
- **Reproducibility**: Random seed control, saved models

## 📖 Usage Example

```python
import pickle
import numpy as np
from pathlib import Path

# Load trained model
with open("data/processed/trained_hmm_model.pkl", "rb") as f:
    hmm = pickle.load(f)

# Load test sequences
with open("data/processed/test_observation_sequences.pkl", "rb") as f:
    test_sequences = pickle.load(f)

# Predict activities
for obs_seq, true_labels in test_sequences:
    predicted_labels = hmm.predict(obs_seq)
    print(f"Predicted: {predicted_labels}")
    print(f"True: {true_labels}")
```

## 📝 Requirements

See `requirements.txt` for complete list. Key dependencies:

- numpy >= 1.21.0
- pandas >= 1.3.0
- scipy >= 1.7.0
- scikit-learn >= 1.0.0
- matplotlib >= 3.4.0
- seaborn >= 0.11.0

## 🤝 Contributing

This is an academic project. For issues or questions, please contact the team members.

## 📄 License

This project is part of an academic assignment.

## 🙏 Acknowledgments

- Professor and course staff for project guidance
- Smartphone sensor data collection using Physics Toolbox Sensor Suite app

---

**Last Updated**: March 6, 2026
