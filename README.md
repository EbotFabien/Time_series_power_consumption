#  Time Series Analysis: Household Power Consumption
## Forecasting & Anomaly Detection

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Status](https://img.shields.io/badge/Status-Completed-success)
![License](https://img.shields.io/badge/License-MIT-green)

---

##  Project Overview

This project performs a comprehensive time series analysis on household electric power consumption data. We explore the data, decompose it into trend and seasonal components, build forecasting models, detect anomalies, and evaluate how data cleaning affects forecast accuracy.

**Dataset:** [UCI Machine Learning Repository - Individual Household Electric Power Consumption](https://archive.ics.uci.edu/ml/datasets/individual+household+electric+power+consumption)

---

##  Dataset Description

| Attribute | Description |
|-----------|-------------|
| **Period** | December 2006 - November 2010 (~4 years) |
| **Frequency** | Per-minute readings → Aggregated to daily |
| **Records** | 2,075,259 rows → 1,442 days |
| **Target Variable** | Global Active Power (kilowatts) |

### Features
| Column | Description | Unit |
|--------|-------------|------|
| Global_active_power | Total active power consumed | kW |
| Global_reactive_power | Total reactive power | kW |
| Voltage | Average voltage | Volts |
| Global_intensity | Average current intensity | Amperes |
| Sub_metering_1 | Kitchen energy (dishwasher, oven, microwave) | Wh |
| Sub_metering_2 | Laundry room energy (washing machine, dryer) | Wh |
| Sub_metering_3 | Water heater & air conditioner | Wh |

---

##  Objectives

1. **Explore** the time series data and identify patterns
2. **Test stationarity** using the Augmented Dickey-Fuller (ADF) test
3. **Decompose** the series into trend, seasonal, and residual components
4. **Forecast** future power consumption using ARIMA, SARIMA, and Prophet
5. **Detect anomalies** using multiple methods (Z-Score, ARIMA Residuals, Isolation Forest)
6. **Re-forecast** after cleaning anomalies and compare model performance

---

##  Methodology

### 1. Data Preprocessing
- Loaded raw per-minute data (2M+ records)
- Aggregated to daily averages
- Handled missing values using linear interpolation

### 2. Exploratory Data Analysis
- Visualized time series patterns
- Analyzed distribution and seasonality
- Performed ADF test for stationarity
- Generated ACF/PACF plots

### 3. Decomposition
- **Classical Decomposition** (Additive)
- **STL Decomposition** (Robust)
- Period = 7 days (weekly seasonality)

### 4. Forecasting Models
| Model | Description |
|-------|-------------|
| **ARIMA(1,1,1)** | AutoRegressive Integrated Moving Average |
| **SARIMA(1,1,1)(1,1,1,7)** | Seasonal ARIMA with weekly pattern |
| **Prophet** | Facebook's forecasting tool with yearly + weekly seasonality |

### 5. Anomaly Detection
| Method | Type | Description |
|--------|------|-------------|
| **Z-Score** | Statistical | Flags values > 3 standard deviations from mean |
| **ARIMA Residuals** | Statistical | Flags large deviations from model predictions |
| **Isolation Forest** | Machine Learning | Isolates anomalies using random forests |

### 6. Consensus Approach
- Combined results from all 3 methods
- Only flagged points detected by **2+ methods** as true anomalies

---

##  Results

### Forecasting Performance (RMSE)

| Model | Original | After Cleaning | Improvement |
|-------|----------|----------------|-------------|
| ARIMA | 0.6259 | 0.6265 | -0.09% |
| SARIMA | 1.1062 | 1.0699 | +3.28% |
| **Prophet** | **0.2561** | **0.2517** | **+1.69%** |

###  Best Model: **Prophet** (RMSE: 0.2517 kW)

### Anomaly Detection Results

| Method | Anomalies Detected |
|--------|-------------------|
| Z-Score | 13 |
| ARIMA Residuals | 13 |
| Isolation Forest | 29 |
| **Consensus (2+ methods)** | **8** |

---

## 📁 Project Structure

```
├── household_power_consumption.txt    # Raw dataset
├── Household_Power_Consumption_Analysis.ipynb  # Main analysis notebook
├── model_results.csv                  # Model comparison results
├── README.md                          # Project documentation
```

---

##  Requirements

```
pandas>=1.5.0
numpy>=1.23.0
matplotlib>=3.6.0
statsmodels>=0.13.0
prophet>=1.1.0
scikit-learn>=1.1.0
```

### Installation

```bash
pip install pandas numpy matplotlib statsmodels prophet scikit-learn
```

---

##  How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/household-power-forecasting.git
   cd household-power-forecasting
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Download the dataset**
   - Download from [UCI Repository](https://archive.ics.uci.edu/ml/datasets/individual+household+electric+power+consumption)
   - Place `household_power_consumption.txt` in the project folder

4. **Run the notebook**
   ```bash
   jupyter notebook Household_Power_Consumption_Analysis.ipynb
   ```

---

##  Key Findings

1. **Clear Seasonality**: Power consumption shows strong weekly and yearly patterns
   - Higher usage in winter (heating)
   - Lower usage in summer
   - Weekday vs weekend differences

2. **Prophet Outperforms Traditional Models**: Achieved lowest RMSE (0.2517 kW) by effectively capturing multiple seasonal patterns

3. **Anomaly Detection**: Identified 8 days with unusual power consumption using consensus of 3 methods

4. **Data Cleaning Impact**: Removing anomalies improved SARIMA (+3.28%) and Prophet (+1.69%) forecasts

5. **Energy Data is Predictable**: Unlike stock prices, power consumption follows consistent patterns suitable for forecasting

---

##  References

- [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/individual+household+electric+power+consumption)
- [Statsmodels Documentation](https://www.statsmodels.org/)
- [Prophet Documentation](https://facebook.github.io/prophet/)
- [Scikit-learn Isolation Forest](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.IsolationForest.html)

---

## 👥 Team Members

| Name | Role |
|------|------|
| Member Fabien Ebot | Data Preprocessing & EDA ,Forecasting Models|
| Member Abdul wahaab | Anomaly Detection , Documentation & Presentation |

---

##  License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

##  Acknowledgments

- UCI Machine Learning Repository for providing the dataset
- Course instructor for guidance
- Statsmodels and Prophet teams for excellent documentation

---

*Last Updated: January 2025*
