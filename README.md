# Weather & Bicycle Usage – Data Analytics Project

## Project Overview
This project investigates **how weather influences bicycle usage in Zurich**, integrating multiple Data Analytics techniques presented in the ZHAW module.

## Research Question
**Does weather have a significant impact on bicycle usage patterns in Zurich?**

## Methodology
This project follows a complete data analytics workflow:

1. **Data Collection** – Weather API + Synthetic bike counter data
2. **Data Preparation** – Cleaning, merging, and feature engineering
3. **Exploratory Data Analysis** – Visualizations and statistical insights
4. **Regression Modeling** – Predicting bicycle usage from weather
5. **Statistical Analysis** – Correlation tests with p-values
6. **Clustering Analysis** – K-means segmentation (bonus feature)

## Project Structure
```
notebooks/
├── 01_data_collection.ipynb      # Fetch weather data from Open-Meteo API
├── 02_preprocessing.ipynb        # Clean, merge, and prepare data
├── 03_eda.ipynb                  # Exploratory analysis + K-means clustering
├── 04_model.ipynb                # Regression model + evaluation + interpretation
└── 05_database.ipynb             # PostgreSQL integration (bonus feature)

data/
├── weather_zurich.csv            # Hourly weather data (2023)
├── bikes_raw.csv                 # Hourly bicycle counts (2023)
└── merged_weather_bikes.csv      # Combined dataset for analysis

docker-compose.yml                # PostgreSQL database configuration
```

## Key Features

### Minimum Requirements (8 Points)
- ✅ Data collection via Web API (Open-Meteo)
- ✅ Data preparation (cleaning, merging, feature engineering)
- ✅ Data storage (CSV-based, extensible to SQLite/PostgreSQL)
- ✅ Exploratory Data Analysis with multiple visualizations
- ✅ Regression modeling (Linear Regression)
- ✅ Model evaluation (R², RMSE, MAE)
- ✅ Correct interpretation of results
- ✅ Structured Jupyter notebooks

### Bonus Features (Up to 5 Points)
- ✅ **K-means Clustering**: Unsupervised learning for pattern discovery (3 clusters)
- ✅ **Correlation Analysis**: Pearson & Spearman with p-values
- ✅ **Silhouette Score**: Cluster quality evaluation
- ✅ **Elbow Method**: Optimal cluster selection
- ✅ **PostgreSQL Integration**: Professional database setup with Docker
- ✅ **ZHAW Style**: Exact formatting, matplotlib visualizations, proper structure

## Technology Stack
- **Python 3.x** with pandas, numpy, scikit-learn, matplotlib
- **Jupyter Notebooks** for interactive analysis
- **Open-Meteo API** for weather data
- **PostgreSQL 15** with Docker for data persistence
- **psycopg2** for database connectivity
- **Synthetic data** for bicycle counters (representative patterns)

## Results Highlights

### Model Performance
- **Test R² Score**: 0.687 (model explains 68.7% of variance)
- **Test RMSE**: 7,030 bicycles per day
- **Test MAE**: 6,039 bicycles per day
- **Features used**: Temperature, Humidity, Wind Speed, Precipitation, Weekday, Month

### Key Insights
1. **Temperature** is the strongest positive predictor (coef=+836, r=0.607, p<0.001)
2. **Wind Speed** is the strongest negative predictor (coef=-789, r=-0.208, p<0.001)
3. **Precipitation** significantly reduces bicycle usage (coef=-573, r=-0.296, p<0.001)
4. **Humidity** shows moderate negative correlation (coef=-404, r=-0.524, p<0.001)
5. **Weekday patterns** show strong weekend preference for recreational cycling
6. **K-means analysis** identifies 3 distinct usage clusters (cold/low, warm/high, transition)

### Statistical Test Results
- **Chi-squared test**: Weather quality vs bike usage shows significant association (χ²=47.8, p<0.001)
- **ANOVA**: Significant differences in bike usage across weekdays (p<0.001)
- **Pearson correlations** (all highly significant, p<0.001):
  - Temperature: r=+0.607 (strong positive)
  - Humidity: r=-0.524 (moderate negative)
  - Precipitation: r=-0.296 (moderate negative)
  - Wind Speed: r=-0.208 (weak negative)
- **K-means silhouette score**: 0.337 (fair cluster quality with k=3)

## How to Run

### Option 1: Without Database
1. **Install dependencies**:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn scipy requests
   ```

2. **Run notebooks in order**:
   - `01_data_collection.ipynb` – Generates data files
   - `02_preprocessing.ipynb` – Cleans and merges data
   - `03_eda.ipynb` – Analyzes and visualizes data
   - `04_model.ipynb` – Trains model and evaluates

3. **Data will be saved to `data/` folder**

### Option 2: With PostgreSQL Database (Bonus)
1. **Start PostgreSQL container**:
   ```bash
   docker compose up -d
   ```

2. **Install additional dependencies**:
   ```bash
   pip install psycopg2-binary
   ```

3. **Run all notebooks including**:
   - `05_database.ipynb` – PostgreSQL integration and SQL queries

4. **Database credentials**:
   - Host: localhost
   - Database: postgres
   - User: pgadmin
   - Password: geheim
   - Port: 5432

## Limitations & Future Enhancements

### Current Limitations
- Data covers one year only (2025) - longer time series would improve seasonal analysis
- Daily aggregation may hide intraday patterns (rush hour effects)
- Does not account for holidays, events, or infrastructure changes
- Linear model may not capture non-linear weather interactions

### Future Enhancements
- Add hourly data for intraday pattern modeling (rush hours, night vs day)
- Incorporate holiday and event indicators (festivals, concerts, strikes)
- Implement non-linear models (Random Forest, XGBoost) for potential R² improvement
- Time series forecasting with ARIMA/Prophet for operational planning
- Geographic visualization with interactive maps
- Real-time weather integration for dynamic predictions

---

**Author**: ZHAW Data Analytics Project  
**Date**: December 2025  
**Status**: Complete
