# Energy Price Day Ahead Forecast - Datathon Project

## Objective
Forecast System Price for the UK electricity market on October 1st, 2024, using 30-minute intervals.

**Objective**:  
Predict energy renewals based on time series data including balancing, demand, generation, and price.

---

## 2. Setup and Imports
- Imported necessary libraries such as `pandas`, `numpy`, `seaborn`, `matplotlib`, `plotly`, `statsmodels`, and `xgboost`.
- Suppressed warnings and set a consistent plotting style.

---

## 3. Data Ingestion & Pre-processing
- Loaded datasets: `balancing_data.csv`, `demand_load_data.csv`, `generation_data.csv`, and `price_data.csv`.
- Converted the `GMT Time` column to datetime format and sorted the data.
- Merged all datasets into a single DataFrame (`merged_df`) using an inner join on `GMT Time`.
- Converted all columns to numeric values and set `GMT Time` as the index.

---

## 4. Exploratory Data Analysis (EDA)
### 4.1 Data Visualization
- Plotted time series for all features to observe trends and patterns.
- Observed that Net Imbalance Volume (NIV) correlates with Bid and Offer Acceptances.

### 4.2 Correlation Analysis
- Created a heatmap to visualize correlations between variables.
- Identified potential features for predicting energy prices.

### 4.3 Price by Time of Day and Season
- Grouped price data by hour and season to analyze trends.
- Created a line plot to visualize price variations by time of day and season.

---

## 5. Time Series Analysis of Price
### 5.1 Focus on 2024 Data
- Filtered data from January 1, 2024, onwards for analysis.
- Checked for missing values and performed basic descriptive statistics.

### 5.2 Additive Decomposition
- Decomposed the price data into trend, seasonal, and residual components.
- Visualized the decomposition results using subplots.

### 5.3 Stationarity Check
- Used the Augmented Dickey-Fuller (ADF) test to check for stationarity in the price data and residuals.

### 5.4 Autocorrelation Analysis
- Plotted ACF and PACF for the price data and residuals to analyze autocorrelation.

---

## 6. SARIMA Model
### 6.1 Grid Search for Best Parameters
- Conducted a grid search over SARIMA parameters to find the best model based on BIC.
- Sorted and displayed the top models by BIC.

### 6.2 Model Evaluation
- Split data into training (80%) and testing (20%) sets.
- Evaluated the model using RMSE and MAE.
- Visualized predictions vs. actual values.

### 6.3 Residual Analysis
- Analyzed residuals for the best SARIMA model using time series plots, ACF, and QQ plots.

### 6.4 Future Predictions
- Refit the best SARIMA model on the full dataset.
- Predicted prices for October 1, 2024, and saved the results to `Sarima_price_prediction.csv`.

---

## 7. XGBoost Model
### 7.1 Feature Selection
- Identified important features using XGBoost's feature importance scores.

### 7.2 Model Training and Evaluation
- Trained an XGBoost regressor using data from 2024.
- Evaluated the model using RMSE, MAE, and R² scores.

### 7.3 Using Lagged Features
- Added lagged values of price as features to improve predictions.
- Used time series cross-validation to evaluate the model across multiple folds.

### 7.4 Future Predictions
- Predicted prices for October 1, 2024, using lagged features.
- Saved the results to `XGBoost_Price_predictions.csv`.

---

## 8. Results
- **SARIMA Model**: Achieved an RMSE of 34.7469 for the forecast.
- **XGBoost Model**: Evaluated using lagged features and achieved predictions for future prices. Achieved RMSE of 29.2

---

## 9. Outputs
- Forecast results for SARIMA and XGBoost models were saved as CSV files:
  - `Sarima_price_prediction.csv`
  - `XGBoost_Price_predictions.csv`
