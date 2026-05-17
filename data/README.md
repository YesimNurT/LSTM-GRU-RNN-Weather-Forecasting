# Dataset

## Source

This project uses the **ARPA Lombardia** open environmental monitoring dataset, available via the Kaggle dataset:

> **ARPA Lombardia – Weather and Air Quality Data**  
> [https://www.kaggle.com/datasets/](https://www.kaggle.com/datasets/)  
> *(Search for "ARPA Lombardia" on Kaggle and use the dataset referenced in the notebook.)*

The data covers **2016-01-01 → 2024-04-01** at **hourly resolution** and includes:

| File | Variable |
|------|----------|
| `wind_speed_filtered.csv` | Wind speed (m/s) |
| `wind_direction_filtered.csv` | Wind direction (degrees) |
| `global_radiation_filtered.csv` | Global solar radiation (W/m²) |
| `rain_filtered.csv` | Precipitation (mm) |
| `humidity_filtered.csv` | Relative humidity (%) |
| `temperature_filtered.csv` | Air temperature (°C) |

Sentinel value `-999.0` is used to denote missing readings and is imputed in the preprocessing stage.

## Running Locally

1. Download the CSVs from Kaggle and place them in `data/raw/`.
2. In the notebook, change `directory_path` from `/kaggle/working/` to `data/raw/` (or an absolute path of your choice).
3. Update the output path in `process_csv` from `/kaggle/working/` to `data/processed/`.
4. The notebook will create intermediate processed files automatically.

## Note on Data Licensing

The ARPA Lombardia dataset is published under the **Italian Open Data License (IODL 2.0)**.  
Please respect the license terms when redistributing or publishing derived work.
