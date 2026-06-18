Data setup:
    To run this repository, please download the dataset from the provided Google Drive link and place the CSV files inside a folder named data/ in this root directory.
    link: https://drive.google.com/drive/folders/1PmLapJI1VSDgvl_AxARNKwM1MCd3WFX0?usp=sharing

# 🧠 Part 3: Predictive Modelling

## 📖 Overview
This folder contains the core machine learning pipeline for the D2C Churn Prediction project. The goal of this phase is to take the cleaned, engineered data snapshot and train a predictive algorithm capable of identifying customers with a high probability of churning within the next 60 days.

We established a baseline using Logistic Regression and advanced to a **Random Forest Classifier**. Crucially, the entire pre-processing step (imputation, scaling, encoding) and the algorithm were bundled into a single unified Scikit-Learn `Pipeline` for seamless production deployment.
---
## 💾 Data Setup
To run this repository locally, you will need to map the original dataset:
1. Download the dataset from this [Google Drive Link](https://drive.google.com/drive/folders/1PmLapJI1VSDgvl_AxARNKwM1MCd3WFX0?usp=sharing).
2. Place the downloaded `.csv` files inside a folder named `data/` in the root directory of this project.
---

## 📁 Directory Structure
```text
Part_3_Model/
├── data/                   # Directory containing the cleaned training dataset
├── churn_model.ipynb       # Jupyter Notebook containing EDA, training, and evaluation
├── error_analysis.md       # Business-focused analysis of model False Positives vs. False Negatives
├── model_card.md           # Formal ethical and technical documentation of the ML model
├── metrics.json            # Automated JSON export of the model's final performance scores
└── README.md               # This file