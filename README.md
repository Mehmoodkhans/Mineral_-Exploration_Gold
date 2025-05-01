
# Mineral exploration drillholes Western Australia

## Objective

The goal of this project is to predict the presence of gold in Western Australian mineral exploration drillholes using structured geological and spatial data. The project emphasizes data cleaning, feature engineering, and interpretable machine learning to support mineral targeting and decision-making in exploration.

Key objectives include:
- Cleaning and standardizing raw drillhole data, especially handling invalid or extreme values in depth and date fields.
- Creating a binary gold classification label (`HAS_GOLD`) to indicate presence (1) or absence (0) of gold, enabling supervised learning.
- Developing a detailed `GOLD_CATEGORY` feature to reflect the priority and presence of gold in multi-commodity targets.
- Engineering robust time-based features from exploration date ranges, including project duration and temporal patterns.
- Capping unrealistic depth values in `MAXDEPTH` to eliminate noise and improve visual and model clarity.
- Exploring statistical relationships and patterns between drilling depth and gold presence.
- Building and evaluating machine learning classifiers to predict gold occurrence from engineered features.
- Performing **feature importance analysis** to identify which variables most strongly influence gold prediction, providing insights for future drilling focus.


## Data Source
The data for this project was sourced from Kaggle:Mineral Exploration Drillholes Western Australia
The dataset comes in a zip archive named Mineral_exploration_drillholes_WA.zip, containing various CSV files with drilling data from Western Australia.

## PipelineThe project follows a structured data processing pipeline to ensure efficient and consistent handling of the exploration data.

**Main File:**  
Mineral_exploration_drillholes_WA.zip (the archive containing all datasets)

**Files Inside and Their Usage:**  
- 'MINERAL_Expl_Drillholes_Openfile.csv'  
- Shape: (3,147,214 rows x 14 columns)   
- This is the primary file used for the analysis, containing detailed records of drillhole data.We start by cleaning and preprocessing this file to extract relevant features.


**Steps:**
1. **Data Cleaning** — The first step is to clean and preprocess the data to ensure that it is usable for modeling:
> Removed invalid MAXDEPTH values by replacing negative depths with NaN and dropping rows with missing values.
> Capped extreme values in MAXDEPTH (values above 3500m) to maintain realistic logical ranges.
> Handled missing values in key columns such as GOLD_CATEGORY and other features with missing or anomalous entries.
> Converted date fields like PERIOD_FROM and PERIOD_TO into datetime format and created duration features for each drilling project. 

2. **Outlier Removal** — We addressed outliers and extreme values to improve the dataset's integrity
> Removed extreme values for MAXDEPTH by capping depths above 3500m.
> Applied outlier detection techniques to other features where necessary (such as capping or trimming unusually large values).
> Ensured that depth values above the 99th percentile in MAXDEPTH were excluded, reducing their potential skewing effect on statistical analyses and machine learning models.

3. **Visualization** — Visualizing key data relationships allowed us to better understand patterns, distributions, and potential outliers:
> Visualized depth distributions to observe how MAXDEPTH varies between drillholes with and without gold presence.
> Used histograms and boxplots to highlight the distribution of key numerical features such as MAXDEPTH, PROJECT_DURATION, and GOLD_CATEGORY.
> Created scatter plots and pair plots to investigate correlations between geological features and gold discovery, helping to refine the feature set.


## Libraries Used
- pandas — Data manipulation and analysis
- numpy — Numerical computations
- scikit-learn — Machine learning models, preprocessing, and evaluation
- matplotlib — Data visualization
- seaborn — Statistical data visualization
- xgboost — Gradient boosting for classification
- lightgbm — Fast gradient boosting framework
- catboost — Gradient boosting for categorical data
- zipfile — Handling ZIP archives
- warnings — Suppressing non-essential warnings


##  Model Performance Comparison

| Model                   | Accuracy  | Precision | Recall   | F1 Score |
|------------------------|-----------|-----------|----------|----------|
| Decision Tree Classifier | 0.999682 | 0.999682  | 0.999682 | 0.999682 |
| Random Forest            | 0.914496 | 0.917888  | 0.914496 | 0.913962 |
| Limited Decision Tree    | 0.867145 | 0.872546  | 0.867145 | 0.865841 |
| Gradient Boosting        | 0.858926 | 0.861299  | 0.858926 | 0.858054 |
| XGBoost                  | 0.848571 | 0.852421  | 0.848571 | 0.847280 |
| LightGBM                 | 0.847398 | 0.852190  | 0.847398 | 0.845905 |
| CatBoost                 | 0.827190 | 0.830843  | 0.827190 | 0.825632 |


## ⭐ Feature Importance Summary

Key important features across models:

- Across multiple tree-based models, the most influential features for predicting Gold presence were
-  LATITUDE 
-  LONGITUDE
-  PERIOD_FROM
-  OPERATOR 
-  PROJECT. 

These spatial and operational features consistently ranked high in feature importance. Other attributes such as ANUMBER, OBJECTID, COLLARID, and PERIOD_TO also contributed, though with comparatively lower impact across models.
