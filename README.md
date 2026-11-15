# Automatic Risk Assessment of School Violence Using Machine Learning
### A Web-Based Early-Warning System

> **Status: In progress** · Graduation project, B.Sc. Information Systems, King Khalid University
> Design and methodology complete; modeling and web application under development (expected [Month 2027]).

---

## Overview

Schools usually react to violence only after an incident has happened. Spotting the students who are moving toward one is much harder, and today it depends almost entirely on what individual teachers and counsellors happen to notice.

This project builds an **explainable, web-based decision-support system** that assesses school-safety risk indicators and prioritizes cases for review by authorized school counsellors. For each student, the system reports:

- the **estimated probability of each risk level** (e.g., 85% High, 12% Medium), and
- the **factors that contributed most** to that result, with the share of each.

This lets a counsellor see *why* a case was flagged. The system supports the judgement of qualified staff; it does not replace it, and it never triggers any action automatically.

---

## Dataset

- **Source:** [School Violence Risk Assessment Dataset (SVRA-10K, v2.0)](PASTE-KAGGLE-LINK-HERE) on Kaggle, released for academic use
- **Size:** 10,000 anonymous student records, no missing values
- **Features:** 15 risk and protective factors in three groups:
  - **Behavioral:** disciplinary incidents, physical fights, prior threats, reported weapon possession
  - **Academic:** GPA, attendance rate
  - **Social & psychological:** anger, empathy, depression score, bullying (victim / perpetrator), peer delinquency, substance use, parental involvement, exposure to domestic violence
- **Target:** four balanced risk levels: No Risk, Low, Medium, High

> **Note:** The dataset is **synthetic** (program-generated; it contains no real students). Results obtained on it must be validated on real, ethically approved local data before any practical use.

---

## Methodology

| Stage | What it covers |
|---|---|
| **1. Data & risk factors** | Document each factor, its meaning, range, and link to risk level |
| **2. Preprocessing** | Encode categorical features, stratified 80/20 train-test split, standardization fitted on training folds only (no data leakage) |
| **3. Modeling** | Train and tune **Logistic Regression**, **Random Forest**, and **SVM** with scikit-learn |
| **4. Web application** | Flask backend + MySQL database + counsellor dashboard |
| **5. Evaluation** | Stratified 5-fold cross-validation, held-out test set, calibration checks |

**Evaluation metrics:** accuracy, precision, recall, F1-score, ROC-AUC, confusion matrix, with **recall on the High-risk class** as the top priority, since a missed student costs more than a false alarm.

**Model selection:** macro F1-score, High-risk recall, probability calibration (reliability diagram, Brier score), and interpretability.

**Explainability:** Logistic Regression coefficients, Random Forest feature importance, and **SHAP values**, shown both for the dataset as a whole and for each individual student. Because the synthetic dataset's true generating weights are known, the explanations can be checked directly against them.

---

## Planned Web Application Features

- Secure login with **role-based access** (counsellor, administrator)
- Single-student form and **batch file upload** for entering the 15 factors
- Result page with risk probabilities and **ranked contributing factors**
- **Counsellor review step** for recording follow-up decisions
- **Dashboard** with school-wide statistics and charts
- Data protection: anonymous IDs, restricted access, and an audit log of every assessment

---

## Tech Stack

`Python` · `pandas` · `scikit-learn` · `SHAP` · `joblib` · `Flask` · `MySQL`

---

## Ethics & Responsible Use

This is an **academic prototype**. Its output is a risk *indicator* that calls for professional review, **not** a diagnosis or a prediction that a student will behave violently. Any future use with real student data would require school and ethics-committee approval, parental consent, and compliance with the Saudi Personal Data Protection Law.

---

## Roadmap

- [x] Problem definition, literature review, and system design
- [ ] Data preprocessing and exploratory analysis
- [ ] Model training, tuning, and comparison
- [ ] Explainability and calibration analysis
- [ ] Flask web application and dashboard
- [ ] Final evaluation and report

---

