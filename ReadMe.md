# Flight Delay Prediction Project

## Overview

This project aims to develop a flight delay prediction feature for a travel app. The feature provides users with insights to help them select on-time flights and avoid frequently delayed flights. The project uses machine learning models to classify flights as either **on time** or **delayed** based on historical flight data.

---

## Dataset Description

The dataset used for this project is titled **`Flight Delay Dataset.csv`**, containing data from 2017 to 2018. It includes features such as flight dates, departure and arrival times, origin and destination details, and delay metrics.

### Key Columns:
- **Year**: Year of the flight.
- **Quarter**: Quarter of the year (1–4).
- **DayOfMonth**: Day of the month.
- **DayOfWeek**: Day of the week.
- **FL_DATE**: Flight date.
- **UNIQUE_CARRIER**: Marketing carrier code.
- **ORIGIN & DEST**: Origin and destination airport codes.
- **CRSDepTime**: Scheduled departure time (local time, hhmm).
- **DEP_TIME**: Actual departure time (local time, hhmm).
- **ARR_DELAY**: Arrival delay in minutes (negative values indicate early arrivals).
- **DISTANCE**: Distance between origin and destination (miles).
- **DISTANCE_GROUP**: Categorized distance intervals (250-mile bins).

---



## Objective

The goal is to:
1. Perform **exploratory data analysis (EDA)** to understand patterns in the data.
2. Build machine learning models to classify flights as **on time** or **delayed**.
3. Evaluate model performance using appropriate metrics and select the best model.
4. Identify contributing factors to flight delays.

---

## Solution Overview

### 1. **Data Exploration**
   - Missing values were handled by imputing or dropping rows/columns, depending on the feature's significance.
   - Time column (e.g., `FL_DATE`) were converted into DateTime frame.
   - Categorical features (e.g., `ORIGIN`, `DEST`, `UNIQUE_CARRIER`) were encoded using one-hot encoding.

### 2. **Feature Engineering**
   - **Target Variable Creation**: A new column, `Is_Delayed`, was created:
     - **1**: ARR_DELAY > 0
     - **0**: ARR_DELAY ≤ 0
   - Extracted new features (weekdays, name of month and whether a day is holiday or not), including:
     - **Weekday**: From `FL_DATE`.
     - **Month_Name**: From `FL_DATE`.
     - **holiday_status**: From `FL_DATE`.

### 3. **Models Used**
   - k-Nearest Neighbors (KNN)
   - Logistic Regression
   - Random Forest (Best-performing model)
   - Gradient Boosting  



### 4. **Evaluation Metrics**
   - The **Area Under the Curve (AUC)** of the Receiver Operating Characteristic (ROC) curve, **Precision**, **Recall**, **F1-Score** and **Cohen's Kappa** were used to evaluate model performance.


### 5. **Best Model: Random Forest**
   - Balanced AUC (0.601761), precision (0.413526), and recall (0.308078)
- Highest Cohen's Kappa (0.128998), indicating better agreement between predicted and actual labels
- Reasonable F1-score (0.353098)
 - Excellent at handling non-linear relationships and capturing interactions between features.

### 6. **Key Contributing Factors**
   Feature importance from the Gradient Boosting model revealed the top predictors of flight delays:
   - **Month_name** (Month of the year)
   - **DEP_TIME** (Actual Departure Time)
   - **UNIQUE_CARRIER** (Marketing carrier code.)
   - **DISTANCE** (Distance between origin and destination (miles))
   - **Weekday** (Day of the week)
   - **ORIGIN** (Origin Airport code)

---



## File Structure

### 1. **`FlightDelayPrediction.ipynb`**
   - Contains all code for:
     - Data exploration and cleaning
     - Feature engineering
     - Model building and evaluation
     - Feature importance analysis

### 2. **Dataset**
   - `Flight Delay Dataset.csv`: Contains flight data.

### 3. **README.md**
   - Provides an overview of the project.

---


## Results Summary

### Model Comparison
 

Here is a summary of the model performance:

| Model                 | AUC      | Precision | Recall   | F1-Score | Cohen's Kappa |
|-----------------------|----------|-----------|----------|----------|---------------|
| **KNN**               | 0.578732 | 0.384412  | 0.305009 | 0.340138 | 0.100248       |
| **Linear Regression** | 0.559881 | 0.349378  | 0.458112 | 0.396424 | 0.082854       |
| **Random Forest**      | 0.601761 | 0.413526  | 0.308078 | 0.353098 | 0.128998       |
| **Gradient Boosting**  | 0.633566 | 0.599788  | 0.084824 | 0.148629 | 0.079929       |

- **Gradient Boosting** excels in AUC and precision, **Linear Regression** leads in recall and F1-score, while **Random Forest** offers the most reliable performance with the highest Cohen's Kappa. **Random Forest** is the most suitable model due to its good AUC, F1-Score, and the highest Cohen's Kappa.

---

## Key Insights

### Feature Importance
From the **Random Forest** model, the following features contributed the most to flight delay predictions:
   1. **Month_name** (Month of the year)
   2. **DEP_TIME** (Actual Departure Time)
   3. **UNIQUE_CARRIER** (Marketing carrier code.)
   4. **DISTANCE** (Distance between origin and destination (miles))
   5. **Weekday** (Day of the week)
   6. **ORIGIN** (Origin Airport code)

### Practical Recommendations
- **Avoid flights with historically high delays**: Use `ARR_DELAY` and `DEP_TIME` trends for decision-making.
- **Select morning flights**: Flights scheduled earlier in the day tend to experience fewer delays.
- **Prefer shorter flights**: Longer distances are more likely to experience delays.

---


## Future Enhancements
- Incorporate external weather data for improved predictions.
- Explore deep learning models like LSTMs for time-series-based delay prediction.
- Add real-time flight data integration for dynamic predictions.



