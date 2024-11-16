# House Pricing ML

This repository contains a machine learning project aimed at predicting house prices based on various features. The project is inspired by the [Kaggle House Prices - Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) competition.

## Project Overview
The primary goal of this project is to build a regression model that accurately predicts the sale prices of residential homes based on their characteristics. By leveraging advanced regression techniques, this project aims to deliver reliable price predictions that can assist real estate professionals.

## Key Steps
1. **Exploratory Data Analysis (EDA)**:
   - Analyze the dataset to understand distributions, correlations, and missing values.
   - Identify key trends and patterns using visualizations.
2. **Feature Engineering**:
   - Transform and preprocess features for better model performance.
   - Handle missing data, encode categorical variables, and scale numeric features.
3. **Modeling**:
   - Train multiple regression models including Linear Regression, Random Forest, XGBoost, and LightGBM.
   - Optimize hyperparameters using cross-validation.
4. **Evaluation**:
   - Assess models using the Root Mean Squared Logarithmic Error (RMSLE).
   - Compare performance and select the best-performing model.
5. **Results**:
   - Generate predictions for the test set.
   - Provide insights and recommendations based on model performance.

## Dataset
The dataset is sourced from Kaggle and includes:
- **Training Data**: 79 features with a target variable, `SalePrice`.
- **Test Data**: Features only, for model evaluation.
- For a full description of the features, refer to the [Kaggle data description](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data).

## Evaluation Metric
The evaluation metric used is **Root Mean Squared Logarithmic Error (RMSLE)**:

$$
RMSLE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (\log(\text{Prediction}_i + 1) - \log(\text{Actual}_i + 1))^2}
$$

For more information, refer to the [Kaggle evaluation section](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/overview/evaluation).