# 🚗🔌 EV Charging Infrastructure Modeling & Ward-Level Profitability Analysis  

---

## 📌 Overview

Using ward-level demographic and socioeconomic data for Delhi, the notebook builds a complete 3-model pipeline plus clustering to:

- Predict EV-related demand  
- Estimate charging station success probability  
- Classify wards into suitability categories  
- Cluster wards into profitability groups  
- Produce a final ranked ward table  

The workflow is **fully reproducible**, interpretable, and follows the structure of the published research.

---

## 📁 Repository Structure

├── README.md  
├── notebook.ipynb # Main notebook containing the full workflow   


---

## 🔧 Project Goals

- Create ML models estimating charging station demand  
- Predict success viability using regression  
- Classify wards using a Random Forest  
- Segment wards into profitability clusters  
- Offer a final actionable ranking for EV charging deployment  

---

## 📊 Dataset Description

The core dataset includes:

| Feature | Meaning |
|--------|---------|
| `Ward` | Delhi administrative region |
| `Population` | Resident population |
| `Income` | Socioeconomic indicator |
| `Vehicles` | Count of registered vehicles |

Derived features created in the workflow:

- `station_score` (0–100 success probability)
- `station_category` (Worst, Moderate, Good, Best)
- `cluster` (K-means assigned)
- `profit_band` (0–25%, 25–50%, 50–75%)

---

# 🧠 Methodology

---

## 🧩 Model 1 — Polynomial Regression (Demand Estimation)

Inputs  
- Population  
- Income  

Target  
- Vehicles (proxy for EV demand)

Procedure:
1. Generate polynomial models for degrees 1–10  
2. Plot **MSE vs Degree**  
3. Choose optimal degree  
4. Evaluate test performance (MAE, MSE, RMSE, R²)

---

## 🧩 Model 2 — Composite Success Score Regression

A weighted success metric is created:

station_score =
0.35 * population_norm +
0.45 * vehicles_norm +
0.20 * income_norm

yaml
Copy code

Again:
- Fit polynomial regression  
- Plot MSE vs degree  
- Predict final success score  

---

## 🧩 Model 3 — Random Forest Classification

`station_score` is binned into:

| Score Range | Category |
|-------------|----------|
| 0–25        | Worst    |
| 25–50       | Moderate |
| 50–75       | Good     |
| 75–100      | Best     |

Random Forest is trained using:

- Population  
- Income  
- Vehicles  

Outputs:
- Balanced accuracy  
- Classification report  
- Confusion matrix visualization  

---

## 🧩 K-Means Clustering & Profitability Segmentation

Steps:

1. Standardize numerical features  
2. Compute WCSS for K = 1–10  
3. Use Elbow Method to choose optimal K  
4. Fit final K (K=5)  
5. Assign profitability based on cluster mean score quartiles  

Visual outputs include:

- Population vs Vehicles cluster plot  
- Population vs Income cluster plot  
- Income vs Vehicles cluster plot  

---

# 🏁 Final Result: Ranked Ward Suitability Table

The notebook concludes with a **complete table per ward**, containing:

| Column | Description |
|--------|-------------|
| `Ward` | Ward name |
| `station_score` | 0–100 probability of success |
| `station_category` | Best/Good/Moderate/Worst |
| `cluster` | Profitability group |
| `profit_band` | 0–25%, 25–50%, 50–75% |

This is the recommended deployment-priority output.

---

# 📈 Visualizations Produced

The notebook automatically generates:

- ✔️ Correlation Heatmap  
- ✔️ Population–Vehicles scatterplot  
- ✔️ Income–Vehicles scatterplot  
- ✔️ MSE vs Degree (Model 1 & 2)  
- ✔️ Confusion Matrix Heatmap  
- ✔️ Elbow Method Plot  
- ✔️ Cluster Visualizations  
- ✔️ Final Ranking Bar Chart  


---

# ▶️ How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/ev-station-pred.git
cd ev-station-pred
```

### 2. Launch the notebook
```bash
jupyter notebook EVChargingProject.ipynb
```
---

# 🧪 Technologies Used

Python 3.x

pandas

numpy

matplotlib

seaborn

scikit-learn

Jupyter Notebook

---

# 🧭 Real-World Applications

EV charging station placement planning

Profitability estimation for infrastructure investors

Urban transportation policy development

Market penetration analysis for EV adoption

Location selection for private charging startups

Can be extended by adding:

Real EV registrations

Traffic & parking availability data

Time-series forecasting

---


