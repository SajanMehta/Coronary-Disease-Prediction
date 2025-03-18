# Coronary Disease Prediction Using NHANES Data

This project analyzes **coronary disease risk factors** using **NHANES medical survey data**.\
Both **Supervised** and **Unsupervised** techniques were used to provide doctors with more information to make decisions on.

## Overview
**Goal:** This project helps physicians identify patients who are at risk for Coronary Heart Disease (CHD) and may benefit from further testing. Since CHD testing is both invasive and expensive, a machine learning-based screening tool can help prioritize high-risk patients and reduce unnecessary procedures.\
**Impact:** Testing is both invasive and expensive. If doctors can determine which patients do not need further testing, they can save them both money, and the need to have these invasive tests done.

## Repository Structure
📂 Coronary-Disease-Prediction\
--> 📂 data                  *Raw Data*\
--> 📂 models                *Pickle Files of the Models*\
--> 📂 notebooks             *Data Prep and Modeling Notebooks*\
--> 📂 prepared data         *Combined, Training, and Holdout Data*\

## Dataset Details
The dataset is sourced from the **National Health and Nutrition Examination Survey (NHANES)**. 
We use patient **demographics, cholesterol levels, blood pressure, glucose, and medical history** to predict coronary disease.

* **Rows:** 2,395 patients (after cleaning)
* **Columns:** 20+ health-related features
* **Target Variable:** `Coronary_dz` (1 = Disease, 0 = No Disease)

## Data Preprocessing
We performed the following steps before modeling:
* **Feature Engineering:** Created hypertension classes, metabolic syndrome predictors, and cholesterol ratio features.
* **Handling Missing Data:** Removed patients with missing coronary disease labels.
* **Balancing the Dataset:** Compared **undersampling vs. SMOTE**.
* **Dimensionality Reduction:** Used **PCA** to analyze variance explained.

## Machine Learning Models
We trained and compared multiple models:
| Model | Precision (Class 0) | Recall (Class 1) |
|---------|----------------|----------------|
| Logistic Regression | **0.97** | **0.74** |
| Random Forest | 0.96 | 0.51 |
| Gradient Boosting | 0.96 | 0.49 |
| Decision Tree | 0.95 | 0.63 |

**Best Model:** Logistic Regression Optimized through RandomSearchCV. This model achieves 97% precision in correctly identifying non-CHD cases while balancing a 74% recall for CHD cases, making it an effective screening tool.

## Key Results
* **Aspirin** is a strong predictor but behaves differently across individuals—some patients take it preventatively, while others take it due to an existing heart condition, making its impact on CHD risk complex.
* **SMOTE** slightly improved recall, but **undersampling gave even better results.**
* **SHAP Analysis shows** that **Aspirin, LDL Cholesterol, and Glucose** contribute most to predictions.

## Feature Importance & SHAP Analysis
We used **SHAP (Shapley Additive Explanations)** to interpret feature contributions.
The top 5 most important features in the best model:
* LDL Cholesterol
* Triglycerides
* Glucose
* Hypertensive Crisis
* Aspirin

**See full SHAP visualization in `notebooks/NHANES_Coronary_Disease_Sajan.ipynb`**

## Real-World Implications
* **97%** of the time, the model will correctly classify the negative cases correctly. When Paired with the **Risk Grouping** shown by the **KMeans/tSNE** chart, Doctors will have extra tools in their belt in fighting Coronary Disease while saving their patients time and money. Additionally, this model can be used to share with patients which factors are the most important in increasing their individual risk for Coronary Heart Disease, as their numbers can be run through the model, risk grouping, and SHAP analysis.
* **Caution:** While this model appears to classify very well, **Bayes Theorem** would tell us to be wary. In fact, in a true positive case for coronary disease, there is a *26% chance* the model would classify that patient as negative. Hopefully, when combined with the risk grouping, and doctors own professional advice, this model would still have some use case.

## Next Steps
**Data/Features:**
* **VO2 max** could be a strong indicator of their cardiovascular health.
* **Strength Levels** could be an indicator in a similar way, and I'd really like to see what SHAP importances look like between those two.
* **Heart Rate Variability** is a measure of cardiovascular health as well, with lower HRV showing more stress on the heart.

**Modeling:**
* Stacking Model, taking the output classification or likelihood as an input in another model.
* Averaging Probabilities between Logistic Regression and Decision Tree classifier and test for improved performance.
* Deep Learning Implementation

**Deployment:**
* Deploy the model in an app with the features as inputs.
* Fit individuals into the risk level groups.
* Provide each individual's classification for Coronary Disease.
* Show Feature Importance SHAP plot for each individual, to show what they need to work on.

## Contributions
This project was developed by **Sajan Mehta** as part of an applied data science portfolio.

Data Source: [NHANES CDC Data](https://wwwn.cdc.gov/nchs/nhanes/continuousnhanes/default.aspx?BeginYear=2019)
LinkedIn: [Link to Profile](https://www.linkedin.com/in/sajan-mehta/)

  

