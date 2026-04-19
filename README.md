<img width="2323" height="3022" alt="eda_dashboard (1)" src="https://github.com/user-attachments/assets/6152dd37-1435-47b2-9c76-d6162f86b20c" /># bike-rental-demand-analysis
Time series analysis and demand forecasting for Capital Bikeshare — includes EDA, seasonal decomposition, lag feature engineering, and an XGBoost model evaluated against a seasonal naive baseline.
# 🚲 Bikeshare Demand Forecasting

Time series analysis and hourly demand forecasting for Capital Bikeshare using the 
UCI Bike Sharing Dataset (17,000+ hourly records). The project covers end-to-end 
ML pipeline from EDA to model evaluation.

---

## 📁 Dataset
- **Source**: [UCI Machine Learning Repository — Bike Sharing Dataset](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset)
- **Size**: 17,379 hourly records across 2011–2012
- **Features**: Weather conditions, calendar info, temperature, humidity, windspeed

---

## 🔍 What's Inside

### 1. Exploratory Data Analysis
- Rental demand trend over two years
- Hourly patterns split by workday vs weekend
- Seasonal and monthly demand distributions
- Weather and temperature impact on rentals
- Demand heatmap across hour × weekday

### 2. Time Series Decomposition
- Additive decomposition into **Trend + Seasonality + Residual**
- Weekly periodicity clearly isolated

### 3. Autocorrelation Analysis
- ACF plot up to 48 hourly lags
- Strong signals at lag 1, 24, and 168 — confirming hourly, daily, and weekly memory

### 4. Feature Engineering
| Feature Type | Examples |
|---|---|
| Lag features | lag_1, lag_24, lag_48, lag_168 |
| Rolling stats | roll_mean_3, roll_std_24 |
| Cyclical encoding | hour_sin/cos, month_sin/cos |
| Domain flags | is_rush_am, is_rush_pm |

### 5. Modeling
- **Algorithm**: XGBoost Regressor
- **Split**: Time-aware (train: Jan 2011 – Mar 2012 / test: Apr – Dec 2012)
- **Baseline**: Seasonal Naive (same hour + weekday, 4-week trailing median)

---

## 📊 Results

| Model | MAE | RMSE |
|---|---|---|
| Seasonal Naive (Baseline) | 28.1 | 42.9 |
| **XGBoost** | **24.1** | **37.6** |

> XGBoost achieves **14.4% lower MAE** and **12.4% lower RMSE** vs the baseline.

---

## 🖼️ Visualizations

### EDA Dashboard
<img width="698" height="901" alt="image" src="https://github.com/user-attachments/assets/87a77383-cb01-4ea7-a1b2-ec8374865501" />



### Time Series Decomposition
<img width="2585" height="1581" alt="decomposition" src="https://github.com/user-attachments/assets/ff323226-94a8-4585-b8c5-79175826e18a" />


### Feature Importance
<img width="1806" height="1026" alt="feature_importance" src="https://github.com/user-attachments/assets/c6c7e682-acb5-433d-8bff-4fd2907b797f" />


### Model Results
<img width="2318" height="2369" alt="model_results" src="https://github.com/user-attachments/assets/770d91e5-c998-4e2e-9544-fe5ee4e33bf0" />


---

## 🛠️ Tech Stack
- Python 3.12
- XGBoost
- Scikit-learn
- Statsmodels
- Pandas / NumPy
- Matplotlib / Seaborn


## 💡 Key Takeaways
- Hourly and weekly lag features are the strongest predictors of rental demand
- Time-aware splitting is critical — random splits leak future data and inflate metrics
- A strong seasonal baseline must be beaten before claiming model value
- Rush-hour flags and cyclical encodings meaningfully improve predictions
