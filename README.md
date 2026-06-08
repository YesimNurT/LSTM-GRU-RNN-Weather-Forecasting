# Multivariate Weather Forecasting — RNN vs. GRU vs. LSTM

> A comparative study of recurrent architectures for next-hour weather forecasting from 24-hour multivariate windows.

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?logo=tensorflow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?logo=keras&logoColor=white)
![Time Series](https://img.shields.io/badge/domain-Time%20Series-2C5777)

<!-- Add a result figure here, e.g. predicted vs. actual curves:
<p align="center"><img src="assets/result.png" width="650"/></p>
-->

## Overview
Predicts the next hour of weather from the previous 24 hours of meteorological variables
(radiation, rainfall, humidity, temperature, wind), comparing recurrent architectures with a shared
preprocessing and evaluation pipeline.

## Approach
- **Framing:** min-max scaling, chronological 70/15/15 split, sliding window (24 h → 1 h multivariate output).
- **Models:** SimpleRNN, GRU, LSTM (50 units × 2 layers, dropout), plus a Bidirectional LSTM with L2 regularization.
- **Tuning:** Keras Tuner (RandomSearch).
- **Metrics:** MAE, RMSE, R², MAPE, sMAPE.

## Results
LSTM > GRU > RNN across most metrics; residual error concentrates in high-variance variables
(rainfall, wind).

## Dataset
ARPA Lombardia hourly weather data (2016-01-01 → 2024-04-01). See `data/README.md` for download
instructions; raw CSVs are not committed.

## Tech stack
TensorFlow/Keras · Keras Tuner · scikit-learn · statsmodels · pandas · NumPy

## Repository structure
```
LSTM-GRU-RNN-for-Weatherprediction.ipynb   # main notebook
requirements.txt
data/README.md                             # dataset instructions
README_lstm.md                             # detailed notes
LICENSE
```

## How to run
```bash
pip install -r requirements.txt
# place raw CSVs under data/raw/ as described in data/README.md
# open the notebook and run all cells
```

## Author
Yeşim Nur Tortop · [GitHub](https://github.com/YesimNurT)
