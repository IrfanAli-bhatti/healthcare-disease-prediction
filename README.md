# Disease Prediction: Breast Cancer Diagnosis from Cell Measurements

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/IrfanAli-bhatti/healthcare-disease-prediction/blob/main/disease_prediction_breast_cancer.ipynb)

## Problem
Breast cancer is one of the most common cancers in women. Measurements of cell nuclei from a fine needle aspirate can help tell malignant tumours from benign ones. **Can a machine learning model predict malignancy from these measurements, and which measurements matter most?** Because missing a cancer is worse than a false alarm, I focused on recall for malignant cases.

## Data
[Breast Cancer Wisconsin (Diagnostic)](https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic), UCI Machine Learning Repository: 569 patients, 30 features, no missing values.

## What I did
1. Checked data quality and class balance
2. Compared feature distributions between malignant and benign tumours
3. Studied correlations between features and diagnosis
4. Trained Logistic Regression and Random Forest (80/20 stratified split, 5-fold cross-validation)
5. Evaluated with accuracy, recall, precision, ROC-AUC and confusion matrices
6. Identified the most important features

## Findings

**1. The classes are not equal.** 357 tumours were benign (62.7%) and 212 malignant (37.3%). Because of this, accuracy alone can look good even if the model misses cancers, so I paid more attention to recall for malignant cases.

**2. Malignant tumours are clearly bigger and more irregular.** The average radius was 17.5 for malignant vs 12.2 for benign, and the average area was about double (978 vs 463). Concave points (dents in the cell outline) were three times higher in malignant tumours, while texture differed much less.

**3. Size and shape features are the strongest signals.** Mean concave points had the highest correlation with malignancy (0.78), followed by perimeter (0.74) and radius (0.73). Radius, perimeter and area move together because they all measure cell size, so many features carry the same information.

**4. Both models performed very well, but each missed 3 cancers.**

| Model | CV ROC-AUC | Test accuracy | Recall (malignant) | Precision (malignant) | Test ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.996 | 0.965 | 0.929 | 0.975 | 0.996 |
| Random Forest | 0.988 | 0.974 | 0.929 | 1.000 | 0.994 |

Out of 42 malignant tumours in the test set, both models missed 3. Random Forest gave no false alarms, and Logistic Regression gave one. In a clinic, those 3 missed cancers matter more than the overall accuracy.

**5. The model looks at the most abnormal cells.** The top Random Forest features were worst perimeter, worst area and worst concave points, which describe the largest and most irregular cells in each sample. This matches what the exploratory charts showed.

## Conclusion and limitations
Simple models can separate malignant from benign tumours with high accuracy using cell measurements. I would choose Logistic Regression because it is easier to explain to clinicians and performs as well as Random Forest here. The next step would be lowering the decision threshold to catch the 3 missed cancers, accepting a few more false alarms.

Limitations: the dataset is small and comes from one source, the test set has only 114 patients (one tumour changes recall by about 2 points), and the model was not tested on data from another hospital. A model like this can support doctors, but it cannot replace a diagnosis.

## Power BI dashboard
*(Screenshot to be added: `dashboard.png`. Build steps are in [POWERBI_GUIDE.md](POWERBI_GUIDE.md).)*

## How to run
Click the **Open in Colab** badge above, then **Runtime > Run all**. The data loads automatically.

## Tools
Python (pandas, NumPy, Matplotlib, seaborn, scikit-learn), Google Colab, Power BI

## Acknowledgement
Code and write-up prepared with help from an AI assistant (Claude). The notebook was run in Google Colab, and all numbers above come from that run.
