# Air Quality Forecasting Project

## Introduction

This project focuses on forecasting PM2.5 air pollutant concentrations using a **Long Short-Term Memory (LSTM)** neural network. The primary goal is to reduce the **Root Mean Square Error (RMSE)** on the leaderboard to **below 4000**, significantly improving from the initial RMSE of **5180.4377**.

The dataset comprises **hourly PM2.5 readings** along with associated **weather features** such as temperature and wind speed, spanning multiple years. The core task is to accurately predict future PM2.5 values on the test set.

We employed a **Bidirectional LSTM with an attention mechanism**, robust preprocessing strategies, and temporal feature engineering to uncover complex patterns in the data.

---

## Challenges & Solutions

| **Challenge**             | **Description**                                                                             | **Solution**                                                                                              |
| ------------------------- | ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| High Initial RMSE         | Baseline model had an RMSE of 5180.4377, indicating poor performance.                       | Introduced a Bidirectional LSTM with attention, robust scaling, and temporal feature engineering.         |
| Missing `chrono` Library  | Initial code used `chrono` for datetime parsing, which wasn’t available in the environment. | Replaced `chrono.parseDate` with `pd.to_datetime` for compatibility.                                      |
| Missing Values in Data    | Missing entries disrupted temporal continuity, degrading LSTM performance.                  | Applied `forward-fill (ffill)` to maintain time-series structure.                                         |
| Capturing PM2.5 Spikes    | Data included sharp PM2.5 spikes (e.g., values up to 390) that were hard to model.          | Used **attention layers** to focus on critical time steps and **RobustScaler** to handle outliers.        |
| Sequence Length Selection | A fixed sequence length (48 hours) might not capture all relevant patterns.                 | Tested 24-hour sequences to balance performance and efficiency; future plans include testing 48/72 hours. |

---

## Knowledge Gained

| **Area**                  | **What I Learned**                                                                                                                                         |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Time-Series Preprocessing | Preserving temporal continuity using forward-fill and deriving cyclic features (hour, day, month, weekday).                                                |
| Robust Scaling            | RobustScaler outperforms MinMaxScaler on outlier-prone data by using medians and IQR for scaling.                                                          |
| Bidirectional LSTM        | Enhances performance by analyzing input sequences in both forward and backward directions.                                                                 |
| Attention Mechanism       | Custom attention layers help the model focus on the most relevant time steps, especially during PM2.5 spikes.                                              |
| Submission Formatting     | Gained experience formatting predictions for leaderboard: `%Y-%m-%d %H:%M:%S` datetime and integer PM2.5 values.                                           |

---


##  Future Work

* Explore **longer sequence lengths (48 or 72 hours)**.
* Tune **hyperparameters** further using grid/random search.
* Add **external features** like AQI categories or regional data.
* Try **transformer-based models** or hybrid CNN-LSTM architectures.
