<img width="1000" height="308" alt="image" src="https://github.com/user-attachments/assets/61f31dec-1093-4817-9d81-6a3c5a9293d5" />

# Walmart Sales Forecasting — Business Intelligence Final Assignment

**Student ID:** CIT-23-02-0358  
**Dataset:** Walmart Store Sales (Kaggle — Time Series)  
**Tools:** Python (Jupyter Notebook) · Power BI  

---

## Project Overview

This project performs end-to-end business intelligence analysis on Walmart's historical weekly sales data. The goal is to clean and explore the data, build a time series forecasting model, and visualise insights — culminating in an interactive Power BI dashboard.

---

## Repository Contents

| File | Description |
|------|-------------|
| `CIT-23-02-0358_BI_Final_Assignment.ipynb` | Main Jupyter Notebook covering all 5 tasks |
| `BI_Final_Assignment.pbix` | Power BI dashboard file |
| `Walmart_Sales_Forecasting__Time_Series_` | Supporting dataset/export |
| `train.csv` | Historical weekly sales data *(required — not included)* |
| `features.csv` | Economic indicators & holiday flags *(required — not included)* |
| `stores.csv` | Store type and size metadata *(required — not included)* |
| `test.csv` | Test split for forecasting *(required — not included)* |

---

## Dataset Description

Three source datasets are merged for analysis:

- **train.csv** — weekly sales per store and department, with holiday flag
- **features.csv** — temperature, fuel price, markdowns (promotions), CPI, unemployment
- **stores.csv** — store type (A/B/C) and store size

---

## Project Structure (Notebook Tasks)

### Task 1 — Data Cleaning & Pre-processing
- Merged `train`, `features`, and `stores` on `Store`, `Date`, and `IsHoliday`
- Filled missing markdown values with `0` (no promotion assumed)
- Imputed missing `CPI` and `Unemployment` with column means
- Removed duplicate rows
- Converted data types: `Type` → category, `IsHoliday` → bool, `Date` → datetime
- Extracted temporal features: `Year`, `Month`, `Week`, `Day`
- Detected and removed outliers in `Weekly_Sales` using the IQR method
- Engineered a `Total_Markdown` feature (sum of MarkDown1–5)
- Exported the cleaned dataset to `walmart_merged.csv`

### Task 2 — Exploratory Data Analysis (EDA)
- Descriptive statistics (mean, std, quartiles)
- Grouped statistics: average sales by store type and by holiday status
- Visualisations: sales distribution histogram, boxplots by store type and holiday, time series trend plot, correlation heatmap, regression plots (sales vs markdown, sales vs fuel price)
- Inferential statistics: independent t-test (holiday vs non-holiday sales effect), Pearson correlation significance test between markdown and sales, sampling estimation

### Task 3 — Model Building
- Aggregated weekly sales across all stores for time series modelling
- 80/20 train/test split on the time series
- Seasonal decomposition (additive model, period = 12) to inspect trend, seasonality, and residuals
- Built a **SARIMA(1,1,1)(1,1,1,52)** model using `statsmodels`
- Generated forecasts for the test set and for the next 12 weeks
- Visualised train, actual test, and forecast series

### Task 4 — Data Visualisation
- Time series of total weekly sales over time
- Monthly sales bar chart (seasonality pattern)
- Sales breakdown by store type
- Holiday vs non-holiday boxplot
- Correlation heatmap
- Regression plots (markdown and fuel price vs sales)
- SARIMA forecast vs actual overlay chart

### Task 5 — Model Evaluation
- **RMSE** (Root Mean Squared Error) — magnitude of prediction error
- **MAE** (Mean Absolute Error) — interpretable business metric
- **R² Score** — proportion of variance explained
- **MAPE** (Mean Absolute Percentage Error) — percentage accuracy
- Residual analysis: time plot and histogram of residuals (checking for random distribution around zero)

---

## Dependencies

```
pandas
numpy
matplotlib
seaborn
scipy
statsmodels
scikit-learn
math (stdlib)
```

Install with:

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn
```

---

## How to Run

1. Place `train.csv`, `features.csv`, `stores.csv`, and `test.csv` in the same directory as the notebook.
2. Open `CIT-23-02-0358_BI_Final_Assignment.ipynb` in Jupyter.
3. Run all cells sequentially (Kernel → Restart & Run All).
4. Cleaned datasets (`walmart_merged.csv`, `walmart_merged_test.csv`) will be saved to the working directory.
5. Open `BI_Final_Assignment.pbix` in Power BI Desktop to explore the dashboard.

---

## Key Findings

- **Store Type A** generates the highest average weekly sales.
- **Holiday weeks** show a statistically significant difference in sales compared to non-holiday weeks.
- **Total Markdown promotions** have a positive but modest correlation with weekly sales.
- The SARIMA model captures the seasonal weekly sales pattern, with performance evaluated via RMSE, MAE, R², and MAPE.

---

## Notes

- The SARIMA model uses a seasonal period of `s=52` (weekly data, yearly seasonality).
- Outlier removal is performed before model training to reduce noise.
- Power BI visuals complement the Python analysis with interactive filtering by store, date, and store type.
