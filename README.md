# 📈 Sales Forecasting & Predictive Analytics - Walmart Dataset
---
## 📌 Project Overview
This project focuses on building, evaluating, and comparing machine learning models (**Linear Regression**, **Random Forest Regressor**, and **XGBoost Regressor**) to forecast weekly sales across **45 Walmart stores**. 

Using historical retail data spanning from **February 2010 to October 2012** (6,435 records), the pipeline implements calendar decomposition, dynamic lag creation, rolling statistics, and macroeconomic indicators. It applies **chronological train-test splitting (80-20)** to prevent lookahead bias and generates an **8-week multi-step recursive forecast** for Q4 holiday demand planning.

---

## ⚙️ Data Preprocessing & Feature Engineering

### 1. Data Cleaning & Integrity

* Audited 6,435 records across 45 stores with **0 missing values**.
* Parsed `Date` (`DD-MM-YYYY`) and sorted data chronologically by `Store` and `Date`.

### 2. Feature Engineering (19 Total Variables)

* **Calendar Features:** `Year`, `Month`, `Quarter`, `WeekOfYear`, `Day`, `Is_Holiday_Season` (Nov/Dec indicator).
* **Lag Features (Per-Store Shifts):** `Sales_Lag_1` (1-week past sales), `Sales_Lag_2` (2-week past sales), `Sales_Lag_4` (4-week past sales).
* **Rolling Statistics (Per-Store Shifts):** `Sales_Rolling_Mean_4` (4-week moving average demand), `Sales_Rolling_Std_4` (4-week sales volatility).
* **Macroeconomic Factors:** `CPI`, `Unemployment`, `Fuel_Price`, `Temperature`, `Holiday_Flag`.

### 3. Chronological Train-Test Split (80–20)

* **Training Set:** 4,995 samples (February 2010 – April 20, 2012).
* **Testing Set:** 1,260 samples (April 27, 2012 – October 26, 2012).

---

## 📊 Model Development & Evaluation Results

All models were evaluated on the **1,260 unseen test samples** using Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and $R^2$ Score:

| Model | MAE ($) $\downarrow$ | RMSE ($) $\downarrow$ | $R^2$ Score $\uparrow$ | Status |
| --- | --- | --- | --- | --- |
| 🏆 **Random Forest Regressor** | **$39,660.71** | **$56,866.82** | **0.9886 (98.86%)** | **Best Model** |
| 🥈 **XGBoost Regressor** | $43,015.76 | $60,878.78 | 0.9870 (98.70%) | Second Best |
| 🥉 **Linear Regression** | $51,250.47 | $71,430.08 | 0.9821 (98.21%) | Baseline |

---

## 📈 Visual Analytics & Diagnostic Highlights

1. **Historical Weekly Sales Trend (`01_historical_sales_trend.png`):** Captures seasonal demand spikes recurring annually during Q4 (Thanksgiving and Christmas).
2. **Actual vs. Forecasted Sales (`02_actual_vs_predicted_forecast.png`):** Demonstrates close alignment between actual store sales and Random Forest predictions over the 2012 test period.
3. **Feature Importance Analysis (`03_feature_importance.png`):** Confirms that `Sales_Rolling_Mean_4`, `Sales_Lag_1`, `Store`, and `CPI` constitute over **85%** of predictive weight.
4. **Residual Error Distribution (`04_residuals_distribution.png`):** Residuals are normally distributed and centered tightly around zero, indicating unbiased model performance.
5. **Future 8-Week Sales Forecast (`05_future_sales_forecast.png`):** Accurately projects future demand acceleration for November and December 2012, highlighting Thanksgiving (Week 47) and Christmas (Week 52) peaks reaching up to **$1.7M** weekly store averages.

---

## 💡 Business Insights & Strategic Recommendations

1. **Statistical Safety Stock Buffering:**
* Utilize the top model's test RMSE (**$56,866 per store**) as the baseline safety stock threshold to eliminate stockouts while controlling inventory holding costs.


2. **Proactive Q4 Supply Chain Ramp-Up:**
* Initiate warehouse inventory build-up **4 to 6 weeks prior** to late November to absorb the projected **35%–55%** seasonal demand surge during Thanksgiving and Christmas.


3. **Store-Tier Resource Allocation:**
* Allocate inventory and promotional budgets dynamically based on individual store baseline volume rather than uniform chain-wide distribution.


4. **Macroeconomic Sensitivity Monitoring:**
* Continuously adjust sales targets in regions experiencing rising unemployment and shifting CPI to preserve store margins.



---

## 🛠️ Tools & Technologies Used

* **Language:** Python
* **Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, Joblib
* **Environment:** Jupyter Notebook / VS Code

