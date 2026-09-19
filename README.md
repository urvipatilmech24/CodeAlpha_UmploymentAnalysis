# 📊 Unemployment Analytics & Prediction

An interactive data analytics and machine learning application for analyzing unemployment trends in India and predicting unemployment rates based on employment and labour participation indicators.

The project combines **data analysis, COVID-19 impact analysis, seasonal pattern detection, regional comparisons, and machine learning-based prediction** through a FastAPI backend.

## 🚀 Features

### 📈 Unemployment Overview

* Total number of records
* Average unemployment rate
* Maximum unemployment rate
* Average labour participation rate
* Available regions and areas
* COVID-era unemployment statistics

### 🦠 COVID-19 Impact Analysis

The application divides the data into three periods:

* **Pre-COVID:** Before March 2020
* **Peak COVID Shockwave:** March–December 2020
* **Post-Lockdown / Recovery:** After 2020

It provides:

* Average unemployment rate for each period
* Average employment
* Labour participation comparison
* Regional changes in unemployment during the COVID period

### 📅 Seasonal Pattern Analysis

The application analyzes unemployment and labour participation rates across different months to identify seasonal patterns.

### 🗺️ Regional & Urban-Rural Analysis

Users can analyze:

* Unemployment trends by state/region
* Urban vs rural unemployment
* Regional average unemployment rates
* Time-series trends

### 🤖 Machine Learning Prediction

A **Random Forest Regression** model is used to predict the unemployment rate using:

* Estimated employed population
* Labour participation rate

The prediction API also provides an associated risk category and policy-action output based on the predicted unemployment rate.

---

## 🛠️ Technologies Used

| Technology              | Purpose                         |
| ----------------------- | ------------------------------- |
| Python                  | Core programming language       |
| FastAPI                 | Backend REST API                |
| Pandas                  | Data processing and analysis    |
| NumPy                   | Numerical operations            |
| Scikit-learn            | Machine learning                |
| Random Forest Regressor | Unemployment prediction         |
| Joblib                  | Saving/loading trained ML model |
| Uvicorn                 | Running the FastAPI server      |
| CSV                     | Dataset storage                 |

---

## 📂 Project Structure

```text
Umemployment Analytics/
│
├── Backend/
│   │
│   ├── data/
│   │   ├── Unemployment_in_India.csv
│   │   └── Unemployment_Rate_upto_11_2020.csv
│   │
│   ├── models/
│   │   ├── model_trainer.py
│   │   └── unemployment_model.pkl
│   │
│   ├── main.py
│   ├── requirements.txt
│   └── .env
│
└── README.md
```

> `venv/` should be excluded from the GitHub repository because it contains the local Python virtual environment and installed packages.

---

## 🧹 Data Processing

The application performs several preprocessing operations before analysis:

1. Loads the unemployment dataset.
2. Removes unnecessary whitespace from column names.
3. Removes missing records.
4. Renames important columns for easier processing.
5. Converts dates into a standard datetime format.
6. Extracts year and month information.
7. Creates a numerical month feature.
8. Categorizes records into COVID-19 eras.
9. Prepares the data for analysis and machine learning.

### Important Dataset Features

The model and analysis use information including:

* Region
* Date
* Estimated Unemployment Rate
* Estimated Employed
* Estimated Labour Participation Rate
* Area (Urban/Rural)

---

## 🤖 Machine Learning Model

The project uses a **Random Forest Regressor** from Scikit-learn.

### Input Features

```text
Estimated Employed
Labour Participation Rate
```

### Target

```text
Unemployment Rate
```

The trained model is saved as:

```text
Backend/models/unemployment_model.pkl
```

The model can be retrained using:

```bash
python models/model_trainer.py
```

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/urvipatilmech24/CodeAlpha_...git
```

Replace the repository URL above with your actual GitHub repository URL.

### 2. Navigate to the backend

```bash
cd "Umemployment Analytics/Backend"
```

### 3. Create a virtual environment

```bash
python -m venv venv
```

### 4. Activate the virtual environment

**Windows:**

```bash
venv\Scripts\activate
```

**macOS / Linux:**

```bash
source venv/bin/activate
```

### 5. Install dependencies

```bash
pip install -r requirements.txt
```

---

## ▶️ Running the API

From the `Backend` directory, run:

```bash
uvicorn main:app --reload
```

The API will normally be available at:

```text
http://127.0.0.1:8000
```

FastAPI automatically provides interactive API documentation at:

```text
http://127.0.0.1:8000/docs
```

---

## 🔌 API Endpoints

### Overview

```http
GET /api/overview
```

Returns overall unemployment statistics, available regions, areas, and COVID-era metrics.

### COVID Analysis

```http
GET /api/covid-analysis
```

Returns comparative analysis of unemployment before, during, and after the COVID period.

### Seasonal Patterns

```http
GET /api/seasonal-patterns
```

Returns monthly unemployment and labour participation patterns.

### Trends

```http
GET /api/trends
```

Optional filters:

```text
region
area
```

Example:

```text
/api/trends?region=Maharashtra&area=Urban
```

Returns:

* Time-series data
* Regional unemployment data
* Urban/rural comparison

### Unemployment Prediction

```http
POST /api/predict
```

Example request:

```json
{
  "employed": 10000000,
  "participation_rate": 40.0
}
```

Example response:

```json
{
  "predicted_unemployment_rate": 7.25,
  "risk_level": "Low / Stable",
  "recommended_policy_action": "..."
}
```

---

## 🔄 System Workflow

```text
                    ┌─────────────────────┐
                    │   Unemployment CSV  │
                    │       Dataset       │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Data Preprocessing   │
                    │ & Feature Engineering│
                    └──────────┬──────────┘
                               │
                 ┌─────────────┴─────────────┐
                 ▼                           ▼
        ┌─────────────────┐        ┌──────────────────┐
        │ Data Analytics  │        │ Machine Learning │
        └────────┬────────┘        └────────┬─────────┘
                 │                          │
        ┌────────┴─────────┐                ▼
        │                  │       ┌──────────────────┐
        ▼                  ▼       │ Random Forest    │
   Trend Analysis    COVID/Seasonal│ Regression Model │
        │              Analysis     └────────┬─────────┘
        │                                   │
        └────────────────┬──────────────────┘
                         ▼
                 ┌─────────────────┐
                 │   FastAPI API   │
                 └────────┬────────┘
                          ▼
                 ┌─────────────────┐
                 │ Analytics &     │
                 │ Predictions     │
                 └─────────────────┘
```

---

## 📊 Key Insights Supported

The application can be used to explore:

* Changes in unemployment over time
* Differences between regions
* Urban and rural unemployment patterns
* Labour participation trends
* Changes during the COVID-19 period
* Monthly/seasonal unemployment patterns
* Estimated unemployment based on employment and labour participation inputs

---

## 🔮 Future Enhancements

* Add an interactive frontend dashboard.
* Add more machine learning algorithms for comparison.
* Implement model evaluation metrics such as MAE, MSE and R².
* Add interactive charts and maps.
* Add more recent unemployment datasets.
* Add automated data updates.
* Deploy the FastAPI application to a cloud platform.
* Add authentication and role-based access.
* Improve prediction features using additional economic indicators.

---

## ⚠️ Security

Do not commit sensitive information such as API keys, passwords, tokens, or environment variables.

Add the following to `.gitignore`:

```gitignore
.env
venv/
__pycache__/
*.pyc
```

---

## 🎓 Project Purpose

This project was developed as a data analytics and machine learning application to demonstrate how historical unemployment data can be processed, analyzed, visualized, and used for predictive modeling.

It combines **Python data analysis, REST API development, feature engineering, and machine learning** into a single application.

## 👩‍💻 Author

**Urvi Patil**

Computer Engineering Student

