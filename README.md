# Customer Churn Prediction System

## Project Overview

The Customer Churn Prediction System is a machine learning project designed to predict whether a telecom customer is likely to discontinue their service (churn) or remain with the company. The project uses the Telco Customer Churn dataset and applies data preprocessing, exploratory data analysis (EDA), class balancing techniques, and machine learning models to build an effective predictive system.

The primary objective is to help telecom companies identify customers at risk of leaving and enable proactive retention strategies.

---

## Problem Statement

Customer churn directly impacts revenue and customer acquisition costs. Predicting churn allows businesses to:

- Identify high-risk customers
- Improve customer retention strategies
- Reduce revenue loss
- Enhance customer satisfaction through targeted interventions

---

hlyCharges | Numerical | Monthly payment amount |
| TotalCharges | Numerical | Total amount charged |
| Churn | Target | Customer left service |

---

# Project Workflow

```text
Data Collection
       │
       ▼
Data Understanding
       │
       ▼
Exploratory Data Analysis
       │
       ▼
Data Preprocessing
       │
       ▼
Train-Test Split
       │
       ▼
SMOTE Oversampling
       │
       ▼
Model Training
       │
       ▼
Cross Validation
       │
       ▼
Model Evaluation
       │
       ▼
Model Saving
       │
       ▼
Prediction System
```

---

# Data Cleaning and Preparation

## Removing Irrelevant Features

- The `customerID` column is removed because it does not contribute to prediction.


## Handling Missing Values

### Issue

- The `TotalCharges` column was stored as an object datatype and contained empty strings.

### Solution

Replace empty strings with zero and convert the column to float.


---

## Correlation Analysis

### Correlation Matrix

| Feature Pair | Correlation |
|-------------|-------------|
| Tenure & MonthlyCharges | 0.25 |
| Tenure & TotalCharges | 0.83 |
| MonthlyCharges & TotalCharges | 0.65 |

### Insights

- Strong correlation exists between tenure and TotalCharges
- Expected because total charges accumulate over time

---

# Data Preprocessing

## Target Encoding

Convert churn values into binary labels.

| Original | Encoded |
|-----------|----------|
| No | 0 |
| Yes | 1 |

---

## Feature Encoding

All categorical features are converted into numerical values using Label Encoding.


### Encoder Storage

Each encoder is stored in a dictionary for future inference.

---

# Train-Test Split

The dataset is divided into:

- Training Set: 80%
- Testing Set: 20%

---

# Handling Class Imbalance


The minority class is balanced using:

**SMOTE (Synthetic Minority Oversampling Technique)**

```python
from imblearn.over_sampling import SMOTE
```

### Before SMOTE

| Class | Count |
|---------|---------|
| 0 | 4,138 |
| 1 | 1,496 |

### After SMOTE

| Class | Count |
|---------|---------|
| 0 | 4,138 |
| 1 | 4,138 |

---

# Model Development

## Models Evaluated

### Decision Tree Classifier

### Random Forest Classifier

### XGBoost Classifier

---

# Model Validation

## Cross Validation

5-Fold Cross Validation was used.

### Results

| Model | Mean CV Accuracy |
|----------|----------------|
| Decision Tree | ~78% |
| Random Forest | ~84% |
| XGBoost | ~83% |

### Best Performing Model

**Random Forest Classifier**

---

# Final Model Training

The Random Forest model was trained on the complete SMOTE-balanced training dataset.

---

# Model Evaluation

Evaluation was performed on the untouched test dataset.

## Metrics Used

- Accuracy
- Confusion Matrix
- Precision
- Recall
- F1-Score

### Test Accuracy

**~78%**

### Important Observation

Accuracy alone is insufficient because of class imbalance.

Additional metrics such as:

- Recall
- Precision
- F1-Score

provide a better understanding of model performance.

---

# How to use the Prediction System


### Step 1

Load the trained model and label encoders.

### Step 2

Prepare new customer data.

```python
new_customer = {
    ...
}
```

### Step 3

Convert input into a DataFrame.

```python
pd.DataFrame([new_customer])
```

### Step 4

Apply saved label encoders.

```python
encoder.transform()
```

### Step 5

Generate prediction.

```python
prediction = model.predict(input_data)
```

### Step 6

Generate churn probability.

```python
probability = model.predict_proba(input_data)
```
---

# Technologies Used

| Category | Tools |
|-----------|--------|
| Programming Language | Python |
| Data Manipulation | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Machine Learning | Scikit-Learn |
| Imbalanced Learning | imbalanced-learn (SMOTE) |
| Gradient Boosting | XGBoost |
| Model Persistence | Pickle |

---

# Conclusion

This project successfully developed a telecom customer churn prediction system using machine learning. After performing data cleaning, exploratory data analysis, label encoding, class balancing with SMOTE, and evaluating multiple tree-based models, the Random Forest Classifier achieved the best cross-validation performance (~84%) and approximately 78% accuracy on unseen test data.

The final solution includes a complete inference pipeline capable of predicting churn for new customers and providing churn probability scores, making it suitable as a foundation for customer retention analytics and business decision support systems.