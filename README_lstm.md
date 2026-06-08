# ⏳ Multivariate Time Series Forecasting with RNN / GRU / LSTM

This project investigates **deep learning approaches for multivariate time series forecasting** using meteorological data (radiation, rainfall, humidity, temperature, wind).  
We compare stacked RNN, GRU, and LSTM models on the task of **predicting the next hour of weather variables given the past 24 hours**.

---

## 🚀 Setup & Usage

### Requirements
```bash
pip install -r requirements.txt
```

### Data
The notebook was originally developed on Kaggle using the **ARPA Lombardia** meteorological dataset.  
See [`data/README.md`](data/README.md) for download instructions and how to adapt the paths for local execution.

### Running the Notebook
1. Download the dataset and place the CSVs in a `data/raw/` folder (or update `directory_path` in the notebook).
2. Open `LSTM-GRU-RNN-for-Weatherprediction.ipynb` in Jupyter or VS Code.
3. Run all cells sequentially from top to bottom.

---

## 📖 Abstract
Forecasting time series data is a critical problem in meteorology, energy systems, and finance.  
In this work, we explore recurrent neural architectures (RNN, GRU, LSTM) for **one-step-ahead prediction** of multivariate meteorological variables.  
A fixed-length **sliding window approach (24h → 1h)** is employed to generate supervised learning samples.  
The models are evaluated on MAE, RMSE, R², MAPE, and sMAPE, with the aim of assessing their robustness and generalization to unseen weather patterns.

---

## ⚙️ Methodology

### Data Preprocessing
- Collected radiation, rainfall, humidity, temperature, and wind datasets  
- Cleaned: duplicate removal, date filtering, unnecessary columns dropped  
- Feature engineering: wind direction → vector components  
- Normalization: **Min-Max scaling** applied to continuous features  
- Dataset split: 70% train, 15% validation, 15% test (chronological, no shuffle)

### Sliding Window Framing
- **Sequence length = 24** (past 24 hourly observations)  
- Input: `X[t-24 : t-1]`  
- Output: `y[t]` (multivariate next step)  
- Generated overlapping samples for supervised learning

### Model Architectures
- **RNN**: SimpleRNN (50 units × 2 layers) + Dropout + Dense  
- **GRU**: GRU (50 units × 2 layers) + Dropout + Dense  
- **LSTM**: LSTM (50 units × 2 layers) + Dropout + Dense  
- First recurrent layer returns sequences, second collapses to single vector (many-to-one)  
- Final Dense layer outputs predictions for all variables simultaneously  

### Training
- Loss: Mean Squared Error (MSE)  
- Optimizer: Adam (lr=0.001)  
- EarlyStopping on validation loss (patience 3–5)  
- Epochs: up to 20–50 per model (early stopping applied)  
- Batch sizes: 32–128 depending on experiment  

---

## 📊 Results

| Model   | Validation Performance | Notes |
|---------|------------------------|-------|
| RNN     | Baseline, weaker generalization | Suffers from vanishing gradients |
| GRU     | Stable, better than RNN | Faster convergence, fewer parameters |
| LSTM    | Strongest overall performance | Handles long-range dependencies best |

- Performance metrics reported: MAE, RMSE, R², MAPE, sMAPE (per feature)  
- **LSTM outperformed GRU and RNN** on most metrics  
- Residual plots showed remaining errors concentrated in high-variance regimes (rainfall, wind)  

---

## ⚠️ Limitations
- Current setup restricted to **1-step-ahead forecasting** only  
- Fixed sliding window may not fully capture long-term seasonality  
- Limited feature engineering (no external covariates like calendar effects)  

---

## 🔮 Future Work
- **Multi-step forecasting** (direct, recursive, seq2seq with attention)  
- Hybrid architectures (CNN-LSTM, TCN, Transformers)  
- Probabilistic forecasting with quantile loss or conformal prediction  
- Feature expansion: cyclical time features, lag/rolling stats, exogenous meteorological data  
- Walk-forward cross-validation for more robust evaluation  

---

## 📚 References
1. Hochreiter & Schmidhuber (1997) – *Long Short-Term Memory*  
2. Cho et al. (2014) – *Learning Phrase Representations using GRU*  
3. Bengio et al. (1994) – *Learning Long-Term Dependencies with Gradient Descent*  
4. Lim & Zohren (2021) – *Time Series Forecasting with Deep Learning: A Survey*  

---

## 👥 Authors
- **Yesim Nur Tortop**  
- Final Project – *Multivariate Time Series Forecasting*
