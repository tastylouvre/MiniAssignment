# Audit Risk Classification Notebook

## 1. Project Overview

This project is an ACC102 **Track 2 – GitHub Data Analysis Project**.  
It uses Python to build a small and readable workflow for **audit risk classification** based on the `audit.csv` dataset.

The main idea is simple: use financial and audit-related indicators to predict whether a case is more likely to be **high risk (`Risk = 1`)** or **normal risk (`Risk = 0`)**.  
The notebook is written for a business-facing audience, especially **junior auditors, accounting students, and managers** who want a basic screening tool that helps highlight which cases may deserve closer review.

This project is not meant to replace professional judgement.  
Instead, it is designed as an **early warning tool** that supports audit planning.

---

## 2. Dataset

- **File used:** `audit.csv`
- **Source:** Kaggle (Audit Risk dataset)
- **Access date:** April 2026
- **Target variable:** `Risk`

### Key variables used in the final notebook
- `Sector_score`
- `LOCATION_ID`
- `PARA_A`
- `PARA_B`
- `TOTAL`
- `numbers`
- `Money_Value`
- `District_Loss`
- `PROB`
- `History`

### Why this dataset was selected
I chose this dataset because it is clearly related to **audit risk and fraud screening**, which fits the accounting context of ACC102.  
It is also suitable for this module because the dataset is not too large, has a clear binary target, and allows meaningful Python work such as cleaning, feature design, visualisation, and basic modelling.

---

## 3. Main Methods

The notebook follows a full workflow from data input to final output:

1. **Data loading and checking**  
   Read the CSV file, inspect data types, missing values, and class balance.

2. **Leakage review**  
   Exclude variables that are too close to the final audit judgement, such as direct risk scores and summary risk measures.

3. **Feature design**  
   Create a few simple engineered variables, for example:
   - `Money_Value_missing`
   - `log_Money_Value`
   - `PARA_sum`
   - `PARA_gap`
   - `PARA_product`
   - `Risk_exposure_proxy`
   - `Loss_history_interaction`

4. **Preprocessing pipeline**  
   - numeric features: imputation + scaling  
   - categorical feature (`LOCATION_ID`): imputation + one-hot encoding

5. **Model comparison**  
   Compare:
   - Logistic Regression
   - Random Forest
   - Gradient Boosting

6. **Evaluation**  
   Use cross-validation and a hold-out test set.  
   The main metric is **recall**, because missing a risky audit case is usually more costly than raising a few false alarms.

7. **Model interpretation**  
   Use permutation importance to show which variables matter most in the final model.

---

## 4. Key Findings

- The dataset has generally good quality, with only a very small amount of missing data.
- Even after removing the most leakage-prone variables, the remaining features still contain useful information for risk screening.
- A tree-based model performed better than the simpler baseline model in this notebook.
- Money-related, history-related, and combined exposure features appeared to be important signals in the final model.
- The model is most useful as a **screening support tool**, not as final audit evidence.

---

## 5. How to Run

### Files needed
Make sure the repository contains:
- `ACC102.ipynb` (or your final notebook filename)
- `audit.csv`
- `requirements.txt`
- `README.md`

### Recommended steps
1. Open the project folder in Jupyter Notebook or JupyterLab.
2. Check that `audit.csv` is in the **same folder** as the notebook.
3. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```
4. Open the notebook and choose **Run All**.

---

## 6. Repository / Demo Links

- **GitHub repository:** add your link here
- **Demo video:** add your Mediasite link here

---

## 7. Limitations and Next Steps

### Limitations
- Some remaining variables may still contain indirect audit judgement.
- The notebook uses only one dataset, so the results may not generalise widely.
- There is no time-based validation in the current dataset.
- The classification threshold was not tuned based on business cost.

### Possible next steps
- tune the decision threshold
- test class-weight sensitivity
- compare leakage-controlled and leakage-prone models
- add calibration analysis
- build a small interactive version later if extending to Track 4
