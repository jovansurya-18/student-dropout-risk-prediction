# Student Dropout Risk Prediction

A supervised machine learning project exploring student dropout risk prediction using staged feature sets, XGBoost, neural networks, and model interpretability techniques.

## Overview

The objective of this project was to develop supervised learning models to predict student dropout using institutional data, enabling earlier identification of students who may be at risk and supporting earlier intervention.

A three-stage approach was used to investigate how predictive performance changes as additional student information becomes available throughout the student journey.

### Stages

- **Stage 1:** Applicant and course information
- **Stage 2:** Student and engagement data
- **Stage 3:** Academic performance data

XGBoost and neural network models were trained and evaluated at each stage.

## Methodology

The analysis followed a structured machine learning workflow:

- Exploratory data analysis
- Missing value analysis
- Duplicate checks
- Data type and cardinality checks
- Feature engineering
- Data preprocessing
- Train, validation, and test splitting
- Model training
- Hyperparameter tuning
- Model evaluation
- Feature importance analysis
- SHAP-based model interpretation

The dataset was split into training, validation, and test sets before encoding to help prevent data leakage. AUC was used as a key evaluation metric due to class imbalance in the target variable.

## Models

Two supervised learning approaches were implemented:

- **XGBoost**
- **Neural Network**

Baseline models were first evaluated, followed by hyperparameter tuning using the validation set. The best-performing configurations were subsequently evaluated on the test set.

## Stage 1 – Applicant and Course Information

Stage 1 used information available at an early point in the student journey, including applicant and course-related variables.

Preprocessing included:

- Engineering `DateofBirth` into `Age`
- Removing non-informative identifiers
- Excluding high-cardinality variables with more than 200 unique values
- Dropping columns with more than 50% missing values

The best-performing Stage 1 model was XGBoost, achieving a test AUC of **0.880**.

Feature importance and SHAP analysis were used to interpret the model. `Nationality` was identified as a particularly influential feature.

## Stage 2 – Student and Engagement Data

Stage 2 introduced additional student engagement information, including `AuthorisedAbsenceCount`.

The same preprocessing and modelling framework was retained to allow direct comparison with Stage 1.

Using the same XGBoost baseline hyperparameters, test AUC increased from **0.874 in Stage 1 to 0.888 in Stage 2**.

After hyperparameter tuning, the best Stage 2 XGBoost model achieved a test AUC of **0.894**.

SHAP analysis identified `AuthorisedAbsenceCount` as an important predictor.

## Stage 3 – Academic Performance Data

Stage 3 introduced academic performance variables:

- `AssessedModules`
- `PassedModules`
- `FailedModules`

These variables contained higher levels of missing data and therefore required imputation.

The best Stage 3 XGBoost model achieved a test AUC of **0.9992**.

SHAP and feature importance analysis identified `PassedModules` as the dominant feature, providing a strong predictive signal for dropout risk.

## Results

| Stage | Information Available | Best Model | Test AUC |
|---|---|---|---:|
| Stage 1 | Applicant & course information | XGBoost | 0.880 |
| Stage 2 | Student & engagement data | XGBoost | 0.894 |
| Stage 3 | Academic performance data | XGBoost | 0.9992 |

Model performance increased as more student information became available.

However, there is a trade-off between predictive performance and timing. Stage 1 and Stage 2 models provide earlier indicators of dropout risk, while Stage 3 provides substantially stronger predictive performance but relies on academic performance information that becomes available later in the student journey.

## Model Interpretability

Model interpretability was explored using:

- XGBoost feature importance
- SHAP violin plots
- Neural network loss curves
- Neural network AUC curves

SHAP analysis showed that newly introduced variables increasingly influenced model predictions as additional information was added at each stage.

In particular, academic performance features became the most influential predictors in Stage 3.

## Key Findings

- Predictive performance improved as more student information became available.
- Stage 1 demonstrated that applicant and course information can provide early indicators of dropout risk.
- Stage 2 showed that engagement information can improve predictive performance while still allowing relatively early intervention.
- Stage 3 produced the strongest predictive performance after academic performance variables were introduced.
- XGBoost consistently performed strongly across the three stages.
- SHAP analysis provided additional insight into which variables were driving model predictions.
- Earlier-stage models may provide a larger intervention window, while later-stage models provide stronger predictive signals.

## Business Implications

The findings suggest that institutions could use different models at different points in the student journey.

Stage 1 and Stage 2 models could be used to identify students who may require additional support earlier in their programme, such as academic guidance or engagement initiatives.

Stage 3 models could provide more precise identification of high-risk students once academic performance information becomes available.

Using predictive models across multiple stages could support student retention and more effective allocation of resources.

## Project Files

**Notebook:** Contains the exploratory data analysis, data preprocessing, feature engineering, model training, hyperparameter tuning, evaluation, and SHAP-based model interpretation.

**Report:** Provides the written analysis, methodology, model comparison, results, key findings, business implications, and recommendations.

## Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- XGBoost
- TensorFlow / Keras
- SHAP
- Jupyter Notebook

## Project Structure

```text
student-dropout-risk-prediction/
│
├── README.md
├── student_dropout_risk_prediction.ipynb
└── student_dropout_risk_prediction_report.pdf

## Author

**Jovan Surya**

Data Science, Machine Learning & AI
