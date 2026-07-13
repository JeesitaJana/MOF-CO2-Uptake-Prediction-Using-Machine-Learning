# Predicting CO₂ Uptake in Metal–Organic Frameworks Using Machine Learning

## Overview

Metal–Organic Frameworks (MOFs) are among the most promising materials for carbon capture due to their high porosity, tunable chemistry, and large surface areas. However, evaluating thousands of MOFs through experiments or molecular simulations is computationally expensive.

This project develops machine learning models capable of predicting CO₂ adsorption capacity directly from structural and chemical descriptors, significantly accelerating material screening.

The work reproduces a descriptor-based adsorption prediction workflow inspired by recent MOF machine learning studies and compares Deep Neural Networks (DNN) with XGBoost models.

---

## Objectives

- Predict CO₂ uptake of MOFs at **298 K** and **1 bar**
- Combine **geometric** and **RAC descriptors**
- Build regression models using:
  - Deep Neural Network (DNN)
  - XGBoost Regressor
- Identify key features influencing adsorption performance
- Compare descriptor-based machine learning approaches with graph-based methods reported in literature

---

## Dataset

Three independent datasets were integrated:

### 1. Geometric Features

Includes:

- Accessible Surface Area (ASA)
- Pore Volume
- Largest Cavity Diameter (LCD)
- Pore Limiting Diameter (PLD)

### 2. RAC Descriptors

Includes:

- Atomic environment descriptors
- Connectivity information
- Electronic structure descriptors

### 3. CO₂ Isotherm Data

Adsorption values extracted at:

- Temperature = **298 K**
- Pressure = **100000 Pa (1 bar)**

---

## Final Dataset Statistics

| Parameter | Value |
|------------|--------|
| Initial Geometric MOFs | 726 |
| RAC Feature MOFs | 10,142 |
| Common MOFs | 451 |
| Final Clean Dataset | 449 |
| Total Features | 190+ |

---

## Machine Learning Pipeline

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
 ┌───────────┬───────────┐
 ▼           ▼
DNN       XGBoost
 │           │
 └─────┬─────┘
       ▼
Performance Evaluation
```

---

## Deep Neural Network (DNN)

### Architecture

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

### Hyperparameters

| Parameter | Value |
|------------|--------|
| Optimizer | Adam |
| Learning Rate | 0.00075 |
| Dropout Rate | 0.2 |
| Hidden Layers | 3 |

---

## XGBoost Regressor

### Configuration

```python
n_estimators = 1000
learning_rate = 0.03
max_depth = 6
subsample = 0.8
colsample_bytree = 0.8
```

---

## Results

### Deep Neural Network

| Metric | Value |
|----------|---------|
| R² Score | 0.5665 |
| MAE | 0.723 |
| RMSE | 1.190 |

### XGBoost

| Metric | Value |
|----------|---------|
| R² Score | 0.8491 |
| MAE | 0.5136 |
| RMSE | 0.7018 |

---

## Best Performing Model

🏆 **XGBoost Regressor**

The XGBoost model significantly outperformed the Deep Neural Network, achieving higher predictive accuracy and lower prediction error across all evaluation metrics.

---

## Important Features

Feature importance analysis identified the following descriptors as major contributors to CO₂ adsorption prediction:

- `lc-I-1-all`
- `D_mc-Z-3-all`
- `mc-S-0-all`
- `mc-chi-3-all`
- Accessible Surface Area (ASA)

These findings suggest that both:

- **Chemical environment**
- **Pore structure characteristics**

play critical roles in determining adsorption performance.

---

## Key Findings

- XGBoost significantly outperformed deep learning on the available dataset.
- Descriptor-based machine learning models can effectively predict CO₂ adsorption.
- Chemical descriptors contributed more strongly than purely geometric features.
- Dataset size remains the primary limitation for deep learning performance.
- Machine learning provides a rapid alternative to expensive simulations and experiments for preliminary MOF screening.

---

## Limitations

- Only **449 MOFs** available after preprocessing.
- No graph-level crystal structure information included.
- Full MOF-CGCNN architecture was not reproduced.
- Limited hyperparameter optimization.
- Single gas adsorption condition considered.

---

## Future Work

- Implement **MOF-CGCNN**
- Explore **Graph Neural Networks (GNNs)**
- Use larger hypothetical MOF databases
- Predict multiple gas adsorption properties
- Add uncertainty quantification methods
- Perform automated hyperparameter optimization

---

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-Learn
- TensorFlow / Keras
- XGBoost
- Matplotlib
- Jupyter Notebook

---

## Project Structure

```text
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

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/mof-co2-prediction.git
cd mof-co2-prediction
```

Create a virtual environment:

```bash
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Usage

Run the training notebook:

```bash
jupyter notebook
```

Open:

```text
notebooks/MOF_CO2_Prediction.ipynb
```

Train and evaluate both models to reproduce the results.

---

## Citation

If you use this project in your research or academic work, please cite the corresponding repository and the original MOF machine learning studies that inspired this workflow.

---

## Author

**Jeesita Jana**  
B.Tech – Artificial Intelligence & Data Science (Medical Engineering)  
Amrita Vishwa Vidyapeetham

---

## License

This project is licensed under the MIT License.

```
MIT License

Copyright (c) 2026 Jeesita Jana

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files, to deal in the Software
without restriction, including without limitation the rights to use, copy,
modify, merge, publish, distribute, sublicense, and/or sell copies of the
Software.
```

---

## .gitignore

```gitignore
__pycache__/
.ipynb_checkpoints/
*.pkl
*.h5
*.keras
*.log
*.zip
*.tar
*.xz
.DS_Store
```