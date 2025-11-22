# Sweet Lift Taxi: High-Accuracy Hourly Demand Forecasting

## PROJECT HIGHLIGHTS

This project delivers a **proactive logistics solution** for the *Sweet Lift Taxi* service by implementing a sophisticated time series forecasting model. The goal was to accurately predict the number of taxi orders for the next hour, enabling efficient fleet allocation and operational cost reduction.

| Metric | Target Goal | **Achieved Result** | Status |
| :--- | :--- | :--- | :--- |
| **Test RMSE** | **< 48.0** | **41.62** | **🏆 Exceeded** |

---

## KEY OBJECTIVES

1.  **Prediction Accuracy:** Develop a model to minimize the Root Mean Squared Error (RMSE) to less than 48.0.
2.  **Feature Engineering:** Extract critical time series components (trend, seasonality, and rolling statistics) to create a robust tabular dataset.
3.  **Model Selection:** Compare high-performance boosting algorithms (LightGBM, Random Forest) to select the most accurate and efficient solution.
4.  **Chronological Validation:** Ensure model integrity by splitting the data strictly chronologically (90% Train / 10% Test) to simulate real-world future prediction.

---

## METHODOLOGY & TECHNICAL BREAKDOWN

### 1. Data Preparation & Time Series Analysis

* **Resampling:** The raw data was aggregated and resampled to an **hourly frequency (`1H`)** to match the prediction requirement.
* **Decomposition:** Utilized **Seasonal Decomposition** to clearly identify an **upward Trend** and a strong **24-hour Seasonality** pattern, confirming the need for time-based features.
* **Chronological Split Justification (90/10):** A **90% train set** was deliberately chosen over 70% to maximize the historical context available to the model, ensuring stable learning of complex seasonal and lagged relationships.

### 2. Feature Engineering

The following features were created to maximize predictive power, effectively transforming the time series problem into a supervised learning task:

* **Time Features:** `year`, `month`, `day`, `dayofweek`, `hour` (to capture seasonality).
* **Lag Features:** `lag_1` to `lag_24` (to capture the immediate preceding hours and the exact demand from the previous day).
* **Rolling Mean:** A **24-hour rolling mean** (shifted by 1) was calculated to smooth the recent history and capture the short-term **trend** without data leakage.

### 3. Model Evaluation

Two strong ensemble models were tuned using `GridSearchCV` combined with **`TimeSeriesSplit`** for reliable cross-validation.

| Model | **Test RMSE** | R² Score | Training Time (s) | Prediction Speed |
| :--- | :--- | :--- | :--- | :--- |
| **LightGBM Regressor** | **41.62** | *[Insert R²]* | 29.63 | **HIGH** |
| Random Forest Regressor | 44.27 | *[Insert R²]* | 14.01 | MEDIUM |

*Note: RMSE below 48.0 ensures an average error of less than 48 orders per hour.*

---

## FINAL CONCLUSION & BUSINESS IMPACT

The **LightGBM Regressor** model is the selected production candidate.

The model successfully **exceeded the business goal** by achieving an RMSE of **41.62**. This result provides high confidence in the hourly demand forecast.

### Business Value: Proactive Logistics

This model shifts Sweet Lift Taxi's fleet management from reactive to proactive, leading to direct cost savings and service improvements:

* **Optimal Resource Allocation:** The company can anticipate peak demand and **proactively position drivers** at the airport, reducing customer wait times.
* **Cost Efficiency:** Minimizing driver idle time during low-demand periods and reducing the reliance on surge pricing/incentives during unexpected peaks.
* **Enhanced Customer Experience (SLA):** Faster service directly improves customer satisfaction and strengthens the company's competitive edge.

---

## TECHNOLOGY STACK

* **Language:** Python 3.x
* **Key Libraries:** Pandas, NumPy
* **Modeling:** **LightGBM**, Scikit-learn (`GridSearchCV`, `TimeSeriesSplit`)
* **Analysis:** Statsmodels (`seasonal_decompose`)
* **Visualization:** Matplotlib, Seaborn