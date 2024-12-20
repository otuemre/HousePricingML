# House Pricing ML

This repository contains a machine learning project aimed at predicting house prices based on various features. The project is inspired by the [Kaggle House Prices - Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) competition.

---

## Key Steps

1. **Exploratory Data Analysis (EDA)**:
   - Checked dataset structure and summary statistics using `df.info()` and `df.describe()`.
   - Analyzed missing values, identifying features with significant null entries like `LotFrontage` and `Alley`.
   - Examined unique values for categorical features (e.g., `MSZoning`, `Street`) to plan for encoding.
   - Visualized key insights:
     - Heatmap to explore correlations between numerical features and `SalePrice`.
     - Distribution analysis of `SalePrice`, revealing positive skewness.
     - Scatterplots and boxplots to analyze relationships between features and `SalePrice`.

2. **Handling Missing and Categorical Data**:
   - Missing values in features like `PoolQC`, `Alley`, and `GarageType` were replaced with meaningful defaults (e.g., `"NoFeature"`) based on feature context.
   - Numerical features with missing values, such as `LotFrontage`, were imputed using medians.
   - Categorical features were encoded:
     - **Nominal features** using one-hot encoding to create binary columns.
     - **Ordinal features** using ordinal encoding based on predefined category order.

3. **Feature Engineering**:
   - Addressed skewness in numerical features using log transformations to normalize distributions.
   - Created new features to enhance predictive potential:
     - `TotalBathrooms`: Combines all bathroom-related features into one.
     - `TotalSF`: Total usable square footage of the property.
     - `GrLivAreaToLotArea`: Ratio of above-ground living area to lot area.
     - `GarageAreaToLotArea`: Garage size relative to lot area.

4. **Scaling Numerical Features**:
   - Standardized all numerical features using `StandardScaler` to ensure they have a mean of 0 and a standard deviation of 1.
   - This step enhances model compatibility, especially for algorithms sensitive to feature magnitudes (e.g., SVM, k-NN).

5. **Model Training and Evaluation**:
   Several regression models were trained and evaluated using various metrics, including \( R^2 \), RMSE, and RMSLE. Below are the models and their performances:

   | Model             | MAE                         | MSE  | RMSE | RMSLE | \( R^2 \) |
   |-------------------|-----------------------------|------|------|-------|-----------|
   | Linear Regression | Poor Performance (Not Used) | -    | -    | -     | -         |
   | Ridge Regression  | 0.10                        | 0.04 | 0.20 | 0.12  | 0.89      |
   | LightGBM          | 0.10                        | 0.05 | 0.22 | 0.12  | 0.88      |
   | XGBoost           | 0.11                        | 0.05 | 0.22 | 0.12  | 0.87      |
   | Random Forest     | 0.12                        | 0.06 | 0.24 | 0.13  | 0.85      |

   - **Ridge Regression** emerged as the best-performing model with the lowest RMSE and highest \( R^2 \), showcasing excellent predictive accuracy while maintaining simplicity.
   - **LightGBM** and **XGBoost** delivered competitive results, demonstrating their strengths in handling complex relationships.
   - **Random Forest Regressor**, while robust, underperformed compared to the other models.

6. **Next Steps**:
   - **Hyperparameter Tuning**: Optimize models like Ridge Regression, LightGBM, and XGBoost to further enhance their performance.
   - **Model Stacking**: Experiment with combining predictions from multiple models to create an ensemble for improved accuracy.
   - **Feature Importance Analysis**: Use tree-based models to identify key features impacting house prices.

---

## Dataset

The dataset is sourced from Kaggle and includes:
- **Training Data**: 79 features describing various attributes of houses, with the target variable, `SalePrice`.
- **Test Data**: Contains the same features but excludes the target variable for evaluation.
- **Feature Descriptions**: Detailed explanations of the features can be found in the [Kaggle data description](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data).

---

## Insights So Far:
- Features like `LotFrontage` and `Alley` have significant missing values, requiring imputation or removal.
- Categorical features such as `MSZoning` and `Neighborhood` show meaningful groupings for `SalePrice`.
- Numerical features like `GrLivArea` and `OverallQual` exhibit strong positive correlations with `SalePrice`.
- The target variable `SalePrice` is positively skewed, suggesting potential log transformation during preprocessing.

---

## Evaluation Metric

The evaluation metric used is **Root Mean Squared Logarithmic Error (RMSLE)**, designed to equally penalize errors for expensive and inexpensive houses:

$$
RMSLE = \sqrt{\frac{1}{n} \sum_{i=1}^n (\log(\text{Prediction}_i + 1) - \log(\text{Actual}_i + 1))^2}
$$

This metric ensures proportional fairness across price ranges, and minimizing it is the primary objective of this project. For further details, refer to the [Kaggle evaluation section](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/overview/evaluation).

---

## Visualizations So Far

- **Correlation Heatmap**: Highlights relationships between numerical features and `SalePrice`.
- **Distribution Analysis**: Reveals the skewness of `SalePrice` and potential outliers.
- **Feature Relationships**: Scatterplots and boxplots demonstrate how numerical and categorical features relate to `SalePrice`.
- **Missing Value Analysis**: Bar plot prioritizes features with significant missing data.
