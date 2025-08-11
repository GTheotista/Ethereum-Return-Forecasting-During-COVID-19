# Ethereum Return Forecasting During COVID-19

**Tools:** Python  
**Visualizations:** Matplotlib, Seaborn  
**Dataset:** [Yahoo Finance – Ethereum (ETH-USD)](https://finance.yahoo.com/quote/ETH-USD) and [Our World in Data – COVID-19 Vaccination Data](https://ourworldindata.org/covid-vaccinations)

---

## I. Business Problem Understanding

The COVID-19 pandemic has had a profound impact on global financial markets, including the cryptocurrency sector. Ethereum (ETH), as one of the largest cryptocurrencies by market capitalization, experienced substantial volatility during this period. Pandemic-related indicators — such as vaccination progress, booster dose administration, and vaccination rate trends — may have influenced investor sentiment and, consequently, short-term ETH price movements.

### Problem Statement
- **Investor Perspective:** ETH returns are influenced by a complex interplay of market and macro-health factors. Understanding the predictive power of COVID-19-related variables can help traders develop more informed and adaptive strategies.  
- **Analyst Perspective:** Financial analysts require a systematic, data-driven approach to quantify the contribution of pandemic-related metrics to ETH return forecasting.

### Goals
1. Develop a predictive model for Ethereum’s daily log returns using COVID-19 vaccination-related indicators.  
2. Apply a **Genetic Algorithm (GA)** for simultaneous feature selection and hyperparameter optimization of **LightGBM**.  
3. Assess model performance using both statistical accuracy metrics and financial market performance indicators.

### Business Impact
- Improves decision-making during periods of pandemic-driven market uncertainty.  
- Provides empirical evidence on the relationship between public health developments and cryptocurrency returns.  
- Supports portfolio strategies that adapt to elevated market volatility.

---

## II. Data Understanding & Preprocessing

### Data Sources
- **Financial Data:** Daily ETH-USD adjusted close prices from Yahoo Finance, transformed into log returns.  
- **COVID-19 Data:** Daily vaccination statistics from Our World in Data, focusing on six selected indicators:  
  - people_fully_vaccinated_per_hundred  
  - people_vaccinated_per_hundred  
  - total_boosters_per_hundred  
  - new_people_vaccinated_smoothed  
  - new_vaccinations_smoothed_per_million  
  - new_people_vaccinated_smoothed_per_hundred

### Key Steps
- **Date Synchronization:** Merged ETH returns and COVID-19 metrics on a unified daily date index.  
- **Feature Engineering:** For each COVID-19 metric, calculated 14-day rolling mean, median, 75th percentile, range, and first difference to capture recent trends.  
- **Data Splitting:** Applied an 80–20 time-series split to maintain chronological order in training and testing.

---

## III. Modeling

### Approach
- **Base Algorithm:** LightGBM Regressor  
- **Optimization Method:** Genetic Algorithm (GA) used to identify the optimal subset of features and fine-tune hyperparameters, including learning rate, number of leaves, and maximum tree depth.  
- **Validation Strategy:** 5-fold TimeSeriesSplit cross-validation to preserve temporal dependencies.

### Performance on Test Set
- RMSE: **0.04755**  
- MSE: **0.00226**  
- MAE: **0.03579**  
- MAPE: **10.79%**  
- Sharpe Ratio: **-0.4281**  
- Max Drawdown: **-0.4050**  
- Total Return: **-0.3330**  
- Directional Accuracy: **51.46%**

---

## IV. Conclusion and Recommendations

### Conclusion
- The GA-optimized LightGBM model achieved a **Directional Accuracy of approximately 51%**, only marginally above random chance, suggesting that COVID-19 vaccination-related metrics alone have limited predictive power for daily ETH returns.  
- While error metrics (RMSE: 0.04755, MAE: 0.03579) show modest prediction errors, the negative Sharpe Ratio (-0.4281) and negative Total Return (-33.3%) indicate poor financial viability for trading purposes.  
- The findings suggest that pandemic vaccination data, in isolation, is insufficient to produce strong predictive signals in a volatile cryptocurrency market.

### Recommendations
- **For Market Analysts:**  
  - Integrate COVID-19 metrics with broader macroeconomic and market sentiment variables (e.g., interest rates, inflation, global risk indices).  
  - Consider higher-frequency data (hourly or intra-day) to capture short-term market dynamics.  

- **For Traders:**  
  - Avoid reliance on vaccination data as a standalone trading signal.  
  - Combine technical indicators (e.g., moving averages, RSI, volatility measures) with fundamental data for a more comprehensive strategy.

---

## V. Next Steps
- Extend the study to include other major cryptocurrencies for cross-market comparison.  
- Incorporate lagged market variables and volatility features into the model.  
- Experiment with hybrid modeling approaches combining machine learning with econometric frameworks (e.g., ARIMAX, GARCH).  
- Incorporate alternative data sources, such as search engine trends or social media sentiment, to enhance predictive capability.
