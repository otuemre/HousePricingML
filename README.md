# House Pricing ML

This repository contains a machine learning project aimed at predicting house prices based on various features. The project is inspired by the [Kaggle House Prices - Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) competition.

---

## Project Overview

The primary goal of this project is to build a regression model that accurately predicts the sale prices of residential homes based on their characteristics. By leveraging advanced regression techniques, this project aims to deliver reliable price predictions that can assist real estate professionals.

---

## Key Steps

1. **Exploratory Data Analysis (EDA)**:
   - Checked the dataset structure and types using `df.info()` and `df.describe()`.
   - Analyzed missing values to identify features with significant null entries (e.g., `LotFrontage`, `Alley`).
   - Examined unique values for categorical features to prepare for encoding.
   - Calculated correlations between numerical features and the target variable, `SalePrice`.
2. **Feature Engineering** (Planned):
   - Handle missing values using strategies such as imputation or feature removal.
   - Encode categorical variables and scale numerical variables for better model compatibility.
3. **Modeling** (Planned):
   - Train and evaluate multiple regression models, including Linear Regression, Random Forest, XGBoost, and LightGBM.
   - Use hyperparameter optimization techniques to improve performance.
4. **Evaluation** (Planned):
   - Assess model performance using the Root Mean Squared Logarithmic Error (RMSLE).
   - Compare models to identify the best-performing one.
5. **Results** (Planned):
   - Generate predictions for the test set and summarize findings.

---

## Dataset

The dataset is sourced from Kaggle and includes:
- **Training Data**: 79 features describing various attributes of houses, with the target variable, `SalePrice`.
- **Test Data**: Contains the same features but excludes the target variable for evaluation.
- **Feature Descriptions**: Detailed explanations of the features can be found in the [Kaggle data description](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data).

### Insights So Far:
- Significant missing values observed in features like `LotFrontage` and `Alley`, which will require preprocessing.
- Categorical features like `MSZoning` and `Street` have manageable cardinality, suitable for encoding.
- Correlation analysis revealed strong relationships between `SalePrice` and features like `OverallQual` and `GrLivArea`.

---

## Evaluation Metric

The evaluation metric used is **Root Mean Squared Logarithmic Error (RMSLE)**, designed to equally penalize errors for expensive and inexpensive houses:

$$
RMSLE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (\log(\text{Prediction}_i + 1) - \log(\text{Actual}_i + 1))^2}
$$

This metric ensures proportional fairness across price ranges, and minimizing it is the primary objective of this project. For further details, refer to the [Kaggle evaluation section](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/overview/evaluation).