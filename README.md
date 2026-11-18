# Earthquake Damage Prediction

**Project Code:** PRCP-1015

## Project Overview

This project predicts building damage severity using
structural, construction, and geographic characteristics
from the Nepal earthquake building-damage dataset.

### Damage Grades

- Grade 1: Low damage
- Grade 2: Moderate damage
- Grade 3: Severe damage

## Dataset

- Total buildings: 260,601
- Input features: 38
- Target: damage_grade
- Missing values: None detected

## Methodology

1. Data inspection and validation
2. Exploratory Data Analysis (EDA)
3. Feature preprocessing
4. Stratified train-validation splitting
5. Baseline model development
6. CatBoost hyperparameter optimization
7. Feature importance analysis
8. Geographic generalization experiments
9. Model evaluation and export

## Machine Learning Models

| Model | Accuracy | Macro F1 |
|---|---:|---:|
| Majority Class Baseline | 0.5689 | 0.2417 |
| SGD Classifier | 0.7277 | 0.6396 |
| Random Forest | 0.6045 | 0.3359 |
| Initial CatBoost | 0.7487 | 0.6975 |
| Tuned CatBoost | **0.7505** | **0.7015** |

Results above use the original random validation split.

## Selected Model

CatBoost Classifier

- Iterations: 549
- Depth: 8
- Learning rate: 0.07
- Training records: 208,480
- Validation records: 52,121
- Validation accuracy: 75.05%
- Validation macro F1: 0.7015
- Grade 3 recall: 63.93%

## Visualizations

### Model Comparison

![Model Comparison](earthquake_project_outputs/model_comparison.png)

### Confusion Matrix

![Confusion Matrix](earthquake_project_outputs/confusion_matrix.png)

## Geographic Generalization

Additional experiments tested prediction on unseen
geographic regions.

Three-fold geographic cross-validation:

| Feature Set | Pooled Macro F1 | Grade 3 Recall |
|---|---:|---:|
| With geographic identifiers | 0.3389 | 0.0067 |
| Without geographic identifiers | 0.4421 | 0.2290 |

These experiments revealed that model performance
decreases substantially on geographically unseen regions.

Removing geographic identifiers improved macro F1 and
Grade 3 recall in all three geographic folds, although
performance remained insufficient for reliable
severe-damage screening.

## Limitations

- The original random split contains geographic regions
  represented in both training and validation.
- Geographic generalization is substantially weaker.
- Severe damage is frequently misclassified as moderate.
- Unusual age values such as 995 need further investigation.
- Hyperparameter selection and model comparison mean
  the random validation result is not an untouched test score.
- This model is a research prototype, not a validated
  safety-critical structural assessment system.

## Saved Model

The trained model is available at:

`earthquake_project_outputs/catboost_tuned_model.cbm`

Feature names and categorical metadata are stored in:

`earthquake_project_outputs/model_metadata.json`

## Setup

Install dependencies:

```bash
pip install -r requirements.txt
```

Open and run the project Jupyter Notebook using the
corresponding dataset CSV files.

Training cells are not required to load the saved model
for inference.

## Future Improvements

- Improve performance on unseen geographic regions.
- Explore class weighting and probability calibration.
- Evaluate across additional geographic partitions.
- Investigate age anomalies and feature engineering.
- Obtain an independent test dataset for final evaluation.

## Conclusion

The tuned CatBoost classifier achieved the best random
validation results among the tested configurations.

Geographic experiments revealed substantial limitations
in generalizing to new regions, demonstrating the
importance of robust validation in damage prediction.
