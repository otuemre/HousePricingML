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

   | Model                   | Default  | RandomizedSearchCV | GridSearchCV |
   |-------------------------|----------|--------------------|--------------|
   | Ridge Regression        | 0.806927 | N/A                | 0.806529     |
   | LightGBM                | 0.882784 | 0.889637           | 0.888717     |
   | XGBoost                 | 0.865421 | 0.888977           | 0.886378     |
   | RandomForestRegressor   | 0.868972 | 0.860351           | 0.851057     |

   - **LightGBM** emerged as the best-performing model, showing consistent performance after hyperparameter tuning with both **RandomizedSearchCV** and **GridSearchCV**.
   - **XGBoost** and **Ridge Regression** delivered competitive results, with slight trade-offs in complexity versus performance.
   - **Random Forest Regressor**, while robust, underperformed compared to other models after tuning.

6. **Next Steps**:
   - **Model Stacking**: Experiment with combining predictions from multiple models to create an ensemble for improved accuracy.
   - **Feature Importance Analysis**: Use tree-based models to identify key features impacting house prices.
   - **Further Fine-Tuning**: Perform additional parameter tuning or explore advanced algorithms for potential improvements.

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
