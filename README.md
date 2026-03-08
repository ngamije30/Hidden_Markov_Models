# Human Activity Recognition with Hidden Markov Models

This project implements **Human Activity Recognition (HAR)** using **Hidden Markov Models (HMMs)** and smartphone **accelerometer and gyroscope sensor data**.

## Team Members

* **Part 1 – Data Collection & Feature Extraction:** Jade ISIMBI TUYIZERE
* **Part 2 – HMM Implementation & Evaluation:** Davy NGAMIJE RUHUMULIZA

## Project Overview

The system recognizes four activities from smartphone sensor data:

* Standing
* Walking
* Jumping
* Still

The pipeline includes **data preprocessing, feature extraction, HMM training, and evaluation**.

## Data Collection

Sensor data was collected using **Sensor Logger** on two smartphones:

* **iPhone 12 → `raw_data/` (training data)**
* **iPhone X → `raw_data2/` (test data)**

Sensors used:

* Accelerometer (x, y, z)
* Gyroscope (x, y, z)

Each activity was recorded in **5–10 second segments**, totaling **~1.5 minutes per activity**.
Raw sensor data (~100 Hz) was **resampled to 50 Hz** for processing.

## Project Structure

```
Hidden_Markov_Models/
├── notebooks/
│   ├── activity_recognition.ipynb
│   └── part2_hmm_implementation_and_evaluation.ipynb
├── data/
│   ├── raw/
│   │   ├── raw_data/     # iPhone 12 recordings (training)
│   │   └── raw_data2/    # iPhone 11 recordings (test)
│   └── processed/
├── requirements.txt
└── README.md
```

## Setup

### Clone the repository

```bash
git clone https://github.com/ngamije30/Hidden_Markov_Models.git
cd Hidden_Markov_Models
```

### Install dependencies

```bash
pip install -r requirements.txt
```

### Run the notebook

```bash
jupyter notebook notebooks/activity_recognition.ipynb
```

## Pipeline

### Part 1: Data Processing

* Load accelerometer and gyroscope data
* Resample to **50 Hz**
* Apply **2-second sliding windows (50% overlap)**
* Extract **time and frequency domain features**
* Normalize features using **Z-score standardization**

### Part 2: HMM Implementation

* **4 hidden states** (one per activity)
* **Gaussian emission probabilities**

Algorithms implemented from scratch:

* Viterbi algorithm
* Forward–Backward algorithm
* Baum–Welch (EM) training

Key features:

* Supervised initialization from labeled data
* Covariance regularization for numerical stability
* Log-space computations to prevent underflow

## Evaluation

Model performance is evaluated using:

* Confusion matrix
* Accuracy per activity
* Training convergence plots
* Decoded activity sequence visualizations

All results and plots are saved in:

```
data/processed/
```

## Requirements

Main libraries used:

* numpy
* pandas
* scipy
* scikit-learn
* matplotlib
* seaborn

## Contributors

* Jade ISIMBI TUYIZERE
* Davy NGAMIJE RUHUMULIZA
