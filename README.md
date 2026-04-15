# Road Accident Severity Classification

## Overview

This project aims to predict accident severity using the French BAAC (Bulletin d’Analyse des Accidents Corporels) dataset. The goal is to classify whether an accident results in a severe injury based on environmental conditions, user characteristics, and vehicle attributes.

The project focuses on building a baseline classification model and analyzing the trade-offs between different evaluation strategies, particularly through threshold adjustment.

## Data

- Source: French BAAC dataset (open government data)
- Scope: Road traffic accidents
- Unit of analysis: Individual road users involved in accidents

### Feature Categories

**Environmental / Road Conditions**
- `month`, `hour`
- `light`, `weather`
- `intersection`

**User Characteristics**
- `user_type` (driver, passenger, pedestrian)
- `sex`
- `age`
- `has_safety` (use of safety equipment)

**Vehicle Attributes**
- `vehicle_type`
- `impact`
- `maneuver`

### Target Variable

- `is_severe`: Binary variable indicating whether the injury is severe  
  (derived from official severity classification)

## Methodology

### Data Preparation

- Merging accident, user, and vehicle datasets
- Cleaning missing and inconsistent values
- Feature engineering (grouping categorical variables, deriving age and time)

### Modeling

- Train-test split (80/20) with stratification to preserve class distribution
- Preprocessing using `ColumnTransformer`:
  - One-hot encoding for categorical features
  - Numerical features passed directly
- Baseline model: Logistic Regression

### Threshold Adjustment

Instead of using the default threshold (0.5), the classification threshold is lowered to **0.3** in order to improve the detection of severe cases.

## Results

- Accuracy: 0.67
- ROC-AUC: 0.77

**Confusion Matrix**

- 3881 vs 6874
- 1192 vs 12574

### Interpretation

- The model shows a **moderate ability to distinguish** between severe and non-severe cases (AUC ≈ 0.77)
- Lowering the threshold significantly:
  - **reduces false negatives** (fewer missed severe cases)
  - **increases true positives** (more severe cases correctly identified)
- However, this leads to more **false positives**, illustrating a trade-off between recall and precision

## Key Insights

- Model performance should not be evaluated using accuracy alone
- Threshold selection plays a crucial role in classification tasks
- In safety-critical contexts, **prioritizing recall (detecting severe cases)** may be more important than minimizing false alarms

## Limitations

- The dataset lacks detailed contextual features (e.g., road infrastructure, behavior)
- Relationships between variables may be nonlinear, which is not fully captured by logistic regression
- Results depend on feature engineering choices and threshold selection

## Future Work

- Explore nonlinear models (e.g., Random Forest, Gradient Boosting)
- Incorporate richer spatial or contextual features
- Perform more systematic threshold optimization

## Tech Stack

- Python
- Pandas
- Scikit-learn
