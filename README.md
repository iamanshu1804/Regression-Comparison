# Regression Comparison

This project uses the **Algerian Forest Fires dataset** to predict the **Fire Weather Index (FWI)**, a numerical measure related to fire danger. It compares several regression models and checks which one gives the most accurate predictions.

## Project workflow

The work is split into two notebooks:

1. **`EDA.ipynb` - data cleaning and exploration**
   - Loads the original dataset.
   - Adds a numeric `Region` feature for the two forest regions.
   - Removes missing and invalid rows.
   - Cleans column names and converts columns to suitable numeric types.
   - Saves the cleaned data as `Cleaned_dataset.csv`.

2. **`Model_Training.ipynb` - model training and comparison**
   - Removes date columns (`day`, `month`, and `year`) from the modelling data.
   - Converts `Classes` into a numeric feature: `0` for *not fire* and `1` for *fire*.
   - Uses the remaining features to predict `FWI`.
   - Splits the data into training and testing sets using a 75/25 split.
   - Checks feature correlation and removes highly correlated features using a threshold of `0.85`.
   - Standardizes the features with `StandardScaler`.
   - Trains and evaluates:
     - Linear Regression
     - Lasso Regression
     - Lasso Regression with cross-validation
     - Ridge Regression
     - ElasticNet Regression
     - ElasticNet with cross-validation
   - Compares predictions using MAE, MSE, RMSE, R², and MAPE.
   - Displays metric bar charts, actual-versus-predicted graphs, and example prediction errors.

## Metrics in simple terms

- **MAE**: average size of the prediction error; lower is better.
- **MSE**: penalizes large errors more strongly; lower is better.
- **RMSE**: error in the same units as FWI; lower is better.
- **R²**: proportion of target variation explained by the model; closer to 1 is better.
- **MAPE**: average percentage error for non-zero actual FWI values; lower is better.

## Conclusion

On the current test split, **Linear Regression performed best overall**:

| Metric | Result |
|---|---:|
| MAE | 0.547 |
| MSE | 0.674 |
| RMSE | 0.821 |
| R² | 0.985 |
| MAPE | 41.83% |

This means the model explains approximately **98.5% of the variation** in the test-set FWI values, with an average error of about **0.55 FWI points**. Ridge Regression was a close second. The regularized Lasso and ElasticNet models performed worse on this dataset with their default settings, especially standard ElasticNet.

The results show that Linear Regression is the best choice among the tested models for this split. The comparison is still an evaluation on one held-out sample, so further tuning and additional validation would be useful before using the model in a real fire-risk system.

## How to run

Open the notebooks in Jupyter Notebook or VS Code and run the cells in order:

1. Run `EDA.ipynb` to recreate `Cleaned_dataset.csv`.
2. Run `Model_Training.ipynb` to train the models and view the comparison.

The repository also includes the original dataset (`Algerian_forest_fires_dataset_UPDATE.csv`) and the cleaned dataset (`Cleaned_dataset.csv`).
