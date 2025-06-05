## UKPN - Predicting Export Capacity of Low Carbon Technologies

# Introduction
As the UK transitions to a low-carbon energy future, the number of Low Carbon Technologies (LCT) installations is growing rapidly. These include:

Solar PV

EV Chargers

Heat Pumps

Battery Storage

Each LCT installation can contribute Export capacity — energy exported back to the grid.

For Distribution Network Operators (DNOs) like UK Power Networks, forecasting future Export capacity is critical to:

Anticipate grid load

Plan infrastructure upgrades

Support renewable energy integration

This project builds a machine learning model to predict the Export capacity of new LCT installations, based on installation attributes.

# Business Problem
Goal:
Given the attributes of a new LCT installation, predict the expected Export capacity (in kW).

This allows DNO planners to:

Forecast Export contributions from future installations

Identify Local Authorities or regions with high expected Export

Prioritize infrastructure investments

Manage risk areas where the model is less certain

# Dataset Overview
The project uses the UKPN Low Carbon Technologies Secondary dataset, which includes:

Installation attributes: Category, Type, LicenceArea, LocalAuthority

Technical attributes: LCT_Connections, Import, Export (target variable)

Location attributes: LocalAuthority

Key columns used in this project:

Category — Generation, EV, Heat Pump, Battery Storage

Type — Solar PV, EV Charger, etc.

LicenceArea — Area of operation

LocalAuthority — Local district

LCT_Connections — Number of LCT connections

Export — Target variable (kW exported back to grid)

# Approach
1. Data Exploration & Understanding
Performed Exploratory Data Analysis (EDA) to understand:

Distribution of Export capacity (skewed with long right tail)

Correlations between features and Export

Impact of Category and Type on Export

Identification of outliers and data quality issues

This helped guide feature engineering and model selection.

2. Data Cleaning & Feature Engineering
Dropped non-predictive columns (location codes, empty columns)

One-Hot Encoded categorical variables

Standardized processing pipeline for training and prediction

3. Model Selection
Three models were compared:

Model	Reason for Selection
Linear Regression	Simple, interpretable baseline
Random Forest	Captures non-linear relationships, robust to outliers
XGBoost	State-of-the-art model for tabular data, handles skew and interactions well

4. Validation Strategy
5-Fold Cross Validation used to assess model stability

Final performance evaluated on a held-out test set using:

Root Mean Squared Error (RMSE)

Mean Absolute Error (MAE)

# Results
Model Comparison
Model	CV Mean RMSE	CV Std RMSE	Test RMSE	Test MAE
Linear Regression	19.86	1.95	12.89	6.93
Random Forest	20.55	1.85	15.02	6.93
XGBoost	19.96	1.98	13.72	6.26

Final Model: XGBoost
XGBoost was selected as the final model because:

It provides the lowest Mean Absolute Error (MAE), which is most useful for business users

It handles the skewed distribution of Export well

It captures complex non-linear relationships between features and Export

The model predicts Export capacity with an average error of approximately 6.26 kW on unseen test data.

# Key Insights from Dataset
Export capacity is strongly driven by:

Category — Generation installations (especially Solar PV) contribute the most Export

Type — Solar PV is the dominant source of Export

LCT_Connections — Higher number of connections generally correlates with higher Export

LocalAuthority-level analysis:

Some LocalAuthorities have higher variance in Export, suggesting regional differences in technology adoption and installation practices.

The dataset suggests that:

Future Export growth will continue to be led by Generation/Solar PV

LCT_Connections is a reliable predictor of Export scaling

There is some variability at the LocalAuthority level which could be further explored or modeled

# Business Value
The model allows DNO planners to:

Forecast grid contributions from new LCT installations

Inform capacity planning and investment decisions

Identify potential grid stress points

Support renewable integration strategies

Quantify risk by highlighting regions where predictions are less certain

# Visualizations
Export Distribution:
outputs/visualizations/export_distribution.png

Export vs Category:
outputs/visualizations/export_vs_category.png

Correlation Heatmap:
outputs/visualizations/correlation_heatmap.png

True Export vs Predicted Export:
outputs/visualizations/true_vs_predicted.png

Residuals Distribution:
outputs/visualizations/residuals_distribution.png

Local Authorities with Highest Errors:
outputs/visualizations/local_authority_errors.png

# Project Pipeline
Deep EDA

Data Cleaning & Feature Engineering

Model Training & Comparison

5-Fold Cross Validation

Final Predictions on Test Set

Stakeholder-ready visualizations

# Credits
Dataset: UKPN Open Data

