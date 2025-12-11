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
- **Test R² Score**: ~0.85 (model explains 85% of variance)
- **RMSE**: ~15.3 bicycles
- **MAE**: ~10.2 bicycles

### Key Insights
1. **Hour of day** is the strongest predictor (rush hours vs. off-peak)
2. **Temperature** shows positive correlation with usage
3. **Precipitation** significantly reduces bicycle usage
4. **Weekday/Weekend** patterns are distinct
5. **K-means analysis** identifies 3 distinct usage clusters

### Correlation Findings (p-values)
- Temperature vs Bikes: r=+0.34, p<0.001 ✓ Significant
- Precipitation vs Bikes: r=-0.28, p<0.001 ✓ Significant
- Humidity vs Bikes: r=-0.12, p<0.001 ✓ Significant
- Wind Speed vs Bikes: r=-0.08, p<0.001 ✓ Significant

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
   - Database: weatherbike
   - User: student
   - Password: student123

## Future Enhancements
- Geographic data visualization (maps)
- ANOVA for group comparisons
- Advanced models (Random Forest, Neural Networks)
- Time series forecasting
- Real-time data integration

---

**Author**: ZHAW Data Analytics Project  
**Date**: December 2025  
**Status**: Complete
