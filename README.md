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

5. **Model Training**:
   Several regression models were trained and evaluated to predict house prices. Below are the models and their respective \( R^2 \) scores:
   
   - **Linear Regression**: Poor performance; not used further.
   - **Ridge Regression**: \( R^2 = 0.9127 \)
   - **Lasso Regression**: \( R^2 = -0.0050 \); underperformed due to excessive regularization.
   - **Random Forest Regressor**: \( R^2 = 0.8924 \)
   - **XGBoost**: \( R^2 = 0.8778 \)
   - **LightGBM**: \( R^2 = 0.8619 \)

   Ridge Regression and Random Forest were the best-performing models, balancing simplicity and predictive power.

6. **Evaluation**:
   - Models were evaluated using the Root Mean Squared Logarithmic Error (RMSLE) and \( R^2 \) scores to compare performance.
   - Ridge Regression and Random Forest emerged as top performers, with potential for further tuning.

7. **Results**:
   - Ridge Regression and Random Forest provided strong predictions for house prices.
   - Further improvements can be made by hyperparameter tuning and model stacking.

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