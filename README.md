# House Pricing ML

[![Python](https://img.shields.io/badge/Python-3.9-blue)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.5.2-orange)](https://scikit-learn.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.10.0-orange)](https://www.tensorflow.org/)
[![LightGBM](https://img.shields.io/badge/LightGBM-4.5.0-green)](https://lightgbm.readthedocs.io/)
[![XGBoost](https://img.shields.io/badge/XGBoost-2.1.2-red)](https://xgboost.readthedocs.io/)
[![Pandas](https://img.shields.io/badge/Pandas-2.2.3-blue)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/NumPy-1.26.4-blue)](https://numpy.org/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-3.9.2-yellow)](https://matplotlib.org/)
[![Seaborn](https://img.shields.io/badge/Seaborn-0.13.2-blue)](https://seaborn.pydata.org/)

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
   - Missing values in features like `PoolQC`, `Alley`, and `GarageType` were replaced with meaningful defaults (e.g., "NoFeature") based on feature context.
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

5. **Model Training and Evaluation (TensorFlow & scikit-learn)**:
   - Several regression models were trained and evaluated using various metrics, including \( R^2 \), RMSE, and RMSLE. Below are the scikit-learn models and their performances:

     | Model                   | Default  | RandomizedSearchCV | GridSearchCV |
     |-------------------------|----------|--------------------|--------------|
     | Ridge Regression        | 0.806927 | N/A                | 0.806529     |
     | LightGBM                | 0.882784 | 0.889637           | 0.888717     |
     | XGBoost                 | 0.865421 | 0.888977           | 0.886378     |
     | RandomForestRegressor   | 0.868972 | 0.860351           | 0.851057     |

     - **LightGBM** emerged as the best-performing model, showing consistent performance after hyperparameter tuning with both **RandomizedSearchCV** and **GridSearchCV**.
     - **XGBoost** and **Ridge Regression** delivered competitive results, with slight trade-offs in complexity versus performance.
     - **Random Forest Regressor**, while robust, underperformed compared to other models after tuning.

   - A **TensorFlow sequential neural network** was implemented and outperformed traditional models:
     - **Architecture**:
       - Input layer matching the number of features.
       - Three hidden layers with ReLU activation.
       - Output layer with one neuron for regression.
     - **Regularization**:
       - Early stopping based on validation loss.
       - Learning rate scheduling to improve convergence.
     - **Evaluation**:
       - Achieved a test loss of **0.293** and a mean absolute error (MAE) of **0.384**.

6. **Model Stacking**:
   By combining the predictions of base models (**Ridge Regression**, **LightGBM**, **XGBoost**, and **RandomForestRegressor**) using a meta-model (**Ridge Regression**), the **stacking regressor** achieved an excellent score of **0.9215**. This approach effectively captured complementary patterns from each model, outperforming all individual models.

---

## Kaggle Submission

- The final stacking model and the TensorFlow model were used to generate predictions for the test dataset.
- The submission file was created with predicted house prices and uploaded to Kaggle.
- Achieved a leaderboard score of **0.62562** with TensorFlow, improving over prior attempts with scikit-learn models.

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

---

## Future Improvements

1. **Feature Importance Analysis**:
   - Use tree-based models like LightGBM or XGBoost to identify key features driving predictions.
   - Visualize feature importances to interpret model results better.

2. **Additional Feature Engineering**:
   - Experiment with creating new features, such as interactions between existing ones, to capture complex relationships.

3. **Advanced Model Ensembling**:
   - Explore more sophisticated ensembling techniques, such as blending or boosting, to further improve predictive performance.

4. **Advanced Neural Network Architectures**:
   - Experiment with deeper or more complex TensorFlow architectures, incorporating techniques like dropout and batch normalization.

5. **Deployment**:
   - Deploy the trained TensorFlow model as a web application or API for real-world usability.

---

## Acknowledgments

- The dataset used in this project is sourced from the [Kaggle House Prices - Advanced Regression Techniques competition](https://www.kaggle.com/c/house-prices-advanced-regression-techniques).

---

## License

This project is licensed under the terms of the [MIT License](LICENSE.md).