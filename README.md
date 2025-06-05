UKPN - Predicting Export Capacity of Low Carbon Technologies
🌍 Introduction
As the UK transitions to a low-carbon energy future, the number of Low Carbon Technologies (LCT) being installed on the grid is growing rapidly — including:

Solar PV

EV Chargers

Heat Pumps

Battery Storage

Each installation can contribute Export capacity — energy exported back to the grid.

For Distribution Network Operators (DNOs) like UK Power Networks, it is critical to:

✅ Understand how much energy these new technologies will contribute
✅ Anticipate grid load
✅ Plan infrastructure upgrades

This project builds a machine learning model to predict the Export capacity of new LCT installations, based on installation attributes.

🎯 Business Problem
The core business question is:

“Given the attributes of a new LCT installation, how much Export capacity should we expect?”

By answering this, DNO planners can:

✅ Forecast grid contributions from LCT
✅ Prioritize network investments
✅ Identify locations of potential grid stress

🛠️ Approach
1️⃣ Data Exploration & Understanding
Performed Exploratory Data Analysis (EDA) to understand:

Distribution of Export capacity → right-skewed with outliers

Key drivers of Export:

Category (Generation dominates)

Type (Solar PV → highest Export)

LCT_Connections → strong correlation with Export

Why?
→ Understand data quality
→ Guide feature selection
→ Anticipate modeling challenges (skew, outliers)

2️⃣ Data Cleaning & Feature Engineering
Dropped unused columns (non-predictive / high cardinality)

One-Hot Encoded categorical variables

Why?
→ Ensure models can effectively handle categorical data
→ Avoid overfitting on sparse features

3️⃣ Model Selection
Compared 3 models:

Model	Why I chose it
Linear Regression	Baseline model — easy to interpret
Random Forest	Captures non-linear relationships, robust to outliers
XGBoost	State-of-the-art for tabular data, handles skewed targets, highly tunable

Why this is relevant:
Export capacity is driven by complex interactions (Category, Type, Location, LCT_Connections).
We need models that can capture non-linearity and handle skew — XGBoost is ideal for this.

4️⃣ Validation Strategy
Used 5-Fold Cross Validation to ensure model stability

Evaluated on unseen test set using:

Root Mean Squared Error (RMSE)

Mean Absolute Error (MAE)

Why this is relevant:
→ To avoid overfitting
→ To provide a realistic estimate of model performance
→ Business users want to know: “How accurate is this model on new data?”

📈 Results
Model Comparison:

Model	CV Mean RMSE	CV Std RMSE	Test RMSE	Test MAE
Linear Regression	19.86	1.95	12.89	6.93
Random Forest	20.55	1.85	15.02	6.93
XGBoost	19.96	1.98	13.72	6.26

Final Model: XGBoost
Why?

✅ Most robust to skewed Export distribution
✅ Lowest Mean Absolute Error → key for business usability
✅ Captures non-linear effects between Category, Type, and LCT_Connections

🔍 Key Insights
✅ Export capacity is primarily driven by:

Category (Generation → highest Export)

Type (Solar PV → dominant)

LCT Connections (higher → more Export)

✅ XGBoost predicts Export with average error ~6.26 kW — highly usable for:

Grid planning

Forecasting aggregate Export by region

Prioritizing infrastructure upgrades

📊 Visualizations
Export Distribution
outputs/visualizations/export_distribution.png

Export vs Category
outputs/visualizations/export_vs_category.png

Correlation Heatmap
outputs/visualizations/correlation_heatmap.png

True Export vs Predicted Export
outputs/visualizations/true_vs_predicted.png

Residuals Distribution
outputs/visualizations/residuals_distribution.png

Local Authorities with Highest Errors
outputs/visualizations/local_authority_errors.png

🚀 Business Value
✅ Enable data-driven grid forecasting
✅ Help planners estimate Export from future LCT installations
✅ Identify risk areas for further analysis
✅ Support strategic investment decisions
