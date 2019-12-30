
#  Evaluating Hospital Effectiveness with Government Data

## Motivation

The US health care system is often shrouded in mystery. Hospitals purposely hide their chargemaster lists, so it is impossible for free-market pressures to lower prices. Consumers are burdened with choosing the best health care without any metric to go by, other than hospital advertising. This project aims to find a way to allow consumers to find the best, most affordable hospital in order to allow economic pressure into the health care system.

### Data Sources
All data within the Data folder was extracted from https://www.medicare.gov/

KNN_df - Complete dataset containing imputed information with no NaN
pure_df - Incomplete (does not contain all providers) dataset with no imputed values and no NaN
null_df - Complete dataset containing all true values (no imputation) **with** NaN values

## Jupyter Notebooks

### OS-Obtaining & Scrubbing
Files in Data folder were cleaned: both NaN values and placeholder nulls were removed. Features about location and redundant names and footnotes were also removed.
To merge all five dataframes, each one was reformatted, so each provider could be assigned a single row. See example below:

### Pre-Processed 

(images/provider_prework.jpg) 

### Post-Processed

images/provider_postwork.JPG

Doing so reintroduced a lot of null values since each provider did not have the same amount of information present. Pseudolabeling was used to fill missing the missing target (Spending) variable while KNN imputation filled in the rest of the null values.

### EMN- Exploring, Modeling, and Interpretation

1. Half of pure data was used as test data, while the other half was in the train data along with the imputed information.
2. Features were scaled and outliers (points over 3 standard deviations) were dropped.
3. Stepwise selection and RFE ranked feature importance.

(images/rfe_feature_import.jpg)

4. Heatmap constructed from selected features to check multicollinearity

(images/corr_heatmap.jpg)

5. OLS model constructed and compared to test data with r2 = -3.83
Low R2 most likely due to imputation and small test data.

(images/OLS_error.jpg)

6. Determined Optimal components for 95% Variance: 62 Components

(images/PCA.jpg)

7. Pipeline Random Forest and XGBoost with PCA Analysis and evaluated against test data. 

(images/ML_error.jpg)

8. Retested again comprehensive dataframe with random split

(images/error_cheat.jpg)

## Conclusion
The investigation proved inconclusive as no model was able to predict the test data.
Potential Issues included:
1. Small quantity of target variable
2. Reintroduction of null values due to merging datasets
3. Imputation method oversimplified data
4. Too much data dropped in Obtaining and Scrubbing (due to small target variable)


