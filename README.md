# Predicting CO₂ Uptake in Metal–Organic Frameworks Using Machine Learning

## Overview

Metal–Organic Frameworks (MOFs) are among the most promising materials for carbon capture because of their exceptionally high porosity, tunable chemistry, and large surface areas. However, experimentally evaluating or simulating thousands of MOF structures is computationally expensive and time-consuming.

This project develops machine learning models to predict **CO₂ adsorption capacity** directly from structural and chemical descriptors, enabling rapid screening of promising MOF candidates.

The project is a **descriptor-based partial reproduction study** inspired by recent MOF machine learning research. It compares a **Deep Neural Network (DNN)** and an **XGBoost Regressor** using geometric descriptors and Revised Autocorrelation (RAC) descriptors extracted from publicly available MOF datasets.

---

# Objectives

- Predict CO₂ uptake of MOFs at **298 K** and **1 bar**
- Integrate geometric descriptors and RAC descriptors
- Develop regression models using:
  - Deep Neural Network (DNN)
  - XGBoost Regressor
- Identify important features affecting CO₂ adsorption
- Compare descriptor-based machine learning with graph-based approaches reported in literature

---

# Dataset

The final dataset was created by integrating three independent datasets.

## 1. Geometric Features

Includes structural properties such as:

- Accessible Surface Area (ASA)
- Pore Volume
- Largest Cavity Diameter (LCD)
- Pore Limiting Diameter (PLD)
- Density
- Void Fraction

---

## 2. RAC Descriptors

Chemical descriptors including:

- Atomic environment descriptors
- Connectivity information
- Electronic structure descriptors
- Chemical environment descriptors

---

## 3. CO₂ Isotherm Data

Adsorption values extracted at:

- Temperature: **298 K**
- Pressure: **100000 Pa (1 bar)**

---

# Final Dataset Statistics

| Parameter | Value |
|-----------|------:|
| Initial Geometric MOFs | 726 |
| RAC Feature MOFs | 10,142 |
| Common MOFs | 451 |
| Final Clean Dataset | 449 |
| Total Features | 190+ |

---

# Machine Learning Pipeline

```text
Raw Data
    │
    ▼
Descriptor Extraction
    │
    ▼
Dataset Merging
    │
    ▼
Cleaning & Missing Value Removal
    │
    ▼
Feature Scaling
    │
    ▼
Train / Validation / Test Split
    │
    ▼
Model Training
 ┌───────────────┬───────────────┐
 │               │
 ▼               ▼
Deep Neural   XGBoost
 Network      Regressor
 │               │
 └───────┬───────┘
         ▼
Performance Evaluation
```

---

# Deep Neural Network (DNN)

## Architecture

```text
Input Layer
     │
Dense(1000, ReLU)
     │
Dropout(0.2)
     │
Dense(1000, ReLU)
     │
Dropout(0.2)
     │
Dense(700, ReLU)
     │
Output Layer
```

## Hyperparameters

| Parameter | Value |
|-----------|-------|
| Optimizer | Adam |
| Learning Rate | 0.00075 |
| Hidden Layers | 3 |
| Dropout Rate | 0.2 |
| Loss Function | Mean Squared Error |

---

# XGBoost Regressor

## Configuration

| Parameter | Value |
|-----------|------:|
| n_estimators | 1000 |
| learning_rate | 0.03 |
| max_depth | 6 |
| subsample | 0.8 |
| colsample_bytree | 0.8 |

XGBoost was selected because it performs particularly well on medium-sized tabular datasets while also providing feature importance analysis.

---

# Results

## Deep Neural Network

| Metric | Value |
|--------|------:|
| R² Score | 0.5665 |
| MAE | 0.7230 |
| RMSE | 1.1895 |

---

## XGBoost Regressor

| Metric | Value |
|--------|------:|
| R² Score | 0.8491 |
| MAE | 0.5136 |
| RMSE | 0.7018 |

---

# Best Performing Model

🏆 **XGBoost Regressor**

XGBoost significantly outperformed the Deep Neural Network, achieving higher predictive accuracy and lower prediction error across all evaluation metrics.

---

# Important Features

Feature importance analysis identified the following descriptors as the strongest predictors of CO₂ adsorption:

- lc-I-1-all
- D_mc-Z-3-all
- mc-S-0-all
- mc-chi-3-all
- Accessible Surface Area (ASA)

These findings indicate that both:

- Chemical environment
- Pore structure characteristics

are critical factors governing CO₂ adsorption performance.

---

# Key Findings

- XGBoost significantly outperformed deep learning on the available dataset.
- Descriptor-based machine learning can accurately predict CO₂ adsorption in MOFs.
- Chemical descriptors contributed more strongly than purely geometric descriptors.
- Dataset size remains the major limitation for deep learning performance.
- Machine learning provides a rapid alternative to expensive molecular simulations for preliminary MOF screening.

---

# Limitations

- Only **449 MOFs** remained after preprocessing.
- No graph-level crystal structure information was incorporated.
- The complete MOF-CGCNN architecture from the reference paper was not reproduced.
- AP-RDF and CMD descriptors used in the original study were unavailable.
- Hyperparameter optimization was limited.
- Only a single adsorption condition (298 K, 1 bar) was considered.

---

# Relationship to the Reference Paper

This repository is a **descriptor-based partial reproduction** of a recent MOF adsorption prediction study.

Compared with the original publication, this work differs in:

- Dataset size
- Descriptor family
- Machine learning models

Therefore, this project should be interpreted as a descriptor-based replication study rather than a complete reproduction of the published MOF-CGCNN framework.

---

# Future Work

- Implement MOF-CGCNN
- Explore Graph Neural Networks (GNNs)
- Incorporate larger hypothetical MOF databases
- Predict multiple gas adsorption properties
- Apply uncertainty quantification techniques
- Perform automated hyperparameter optimization

---

# Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- TensorFlow / Keras
- XGBoost
- Matplotlib
- Jupyter Notebook

---

# Project Structure

```text
MOF-CO2-Uptake-Prediction-Using-Machine-Learning/
│
├── data/
│   ├── geometric_features.csv
│   ├── rac_features.csv
│   └── co2_isotherms.csv
│
├── notebooks/
│   └── MOF_CO2_Prediction.ipynb
│
├── models/
│   ├── xgboost_model.pkl
│   └── dnn_model.keras
│
├── results/
│   ├── feature_importance.png
│   ├── parity_plot.png
│   └── metrics.csv
│
├── README.md
├── LICENSE
└── requirements.txt
```

---

# Installation

## Clone the repository

```bash
git clone https://github.com/JeesitaJana/MOF-CO2-Uptake-Prediction-Using-Machine-Learning.git
cd MOF-CO2-Uptake-Prediction-Using-Machine-Learning
```

## Create a virtual environment

```bash
python -m venv venv
```

## Activate the environment

### Linux / macOS

```bash
source venv/bin/activate
```

### Windows

```bash
venv\Scripts\activate
```

## Install dependencies

```bash
pip install -r requirements.txt
```

---

# Usage

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
notebooks/MOF_CO2_Prediction.ipynb
```

Run all notebook cells to train and evaluate both machine learning models.

---

# Citation

If you use this repository in your research or academic work, please cite:

- This repository
- The original MOF machine learning studies that inspired this workflow

---

# Author

**Jeesita Jana**  
B.Tech – Artificial Intelligence & Data Science (Medical Engineering)  
Amrita Vishwa Vidyapeetham

---