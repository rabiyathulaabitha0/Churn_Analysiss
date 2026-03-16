# 📊 Customer Churn Analysis Dashboard
### End-to-End Data Analytics Project | SQL Server · Power BI · Python · Machine Learning

---

## 📌 Brief One Line Summary
An end-to-end churn analysis identifying **26.99% churn rate** across **6,418 customers** using SQL Server, Power BI and Random Forest Machine Learning.

---

## 🔍 Overview
In today's competitive business environment, retaining customers is crucial for long-term success. This project performs an end-to-end churn analysis for a telecom firm using SQL Server for data processing, Power BI for visualization, and Machine Learning to predict future churners — enabling businesses to take proactive steps to improve customer retention.

---

## ❓ Problem Statement
Customer churn is a critical business problem. Companies lose significant revenue when customers leave. The goal of this project is to:
- Identify **why customers are churning**
- Understand **which customers are at risk**
- **Predict future churners** before they leave
- Enable the business to take **proactive retention actions**

---

## 📂 Dataset
| Detail | Info |
|--------|------|
| **Source** | Telecom Customer Data |
| **Total Records** | 6,418 customers |
| **Total Columns** | 32 features |
| **Target Variable** | Customer_Status (Churned / Stayed / Joined) |
| **File Format** | CSV → SQL Server → Excel |

**Key Features:**
- Demographics — Age, Gender, Married, State
- Account Info — Contract, Payment Method, Tenure
- Services — Internet, Online Security, Streaming
- Charges — Monthly Charge, Total Revenue

---

## 🛠️ Tools and Technologies
| Tool | Purpose |
|------|---------|
| **SQL Server (SSMS)** | ETL, Data Cleaning, Views |
| **Power BI** | Dashboard, DAX Measures, Visualization |
| **Python** | Machine Learning Model |
| **Jupyter Notebook** | ML Development |
| **Pandas / NumPy** | Data Processing |
| **Scikit-learn** | Random Forest Model |
| **Matplotlib / Seaborn** | Feature Importance Plot |

---

## ⚙️ Methods

### Step 1 — ETL in SQL Server
```sql
-- Created staging table
SELECT * INTO stg_Churn FROM Customer_Data;

-- Cleaned nulls and loaded to production
SELECT ISNULL(Value_Deal, 'None') AS Value_Deal, ...
INTO prod_Churn FROM stg_Churn;

-- Created views for Power BI
CREATE VIEW vw_ChurnData AS
SELECT * FROM prod_Churn WHERE Customer_Status IN ('Churned','Stayed');

CREATE VIEW vw_JoinData AS
SELECT * FROM prod_Churn WHERE Customer_Status = 'Joined';
```

### Step 2 — Power BI Transformation
- Created **Churn Status** column (1 = Churned, 0 = Stayed)
- Created **Monthly Charge Range** groups
- Created **Age Group** mapping table
- Created **Tenure Group** mapping table
- Unpivoted services columns → `prod_Services` table

### Step 3 — DAX Measures
```dax
Total Customers = COUNT(prod_Churn[Customer_ID])
Total Churn = SUM(prod_Churn[Churn Status])
Churn Rate = [Total Churn] / [Total Customers]
New Joiners = CALCULATE(COUNT(prod_Churn[Customer_ID]), 
              prod_Churn[Customer_Status] = "Joined")
```

### Step 4 — Machine Learning (Random Forest)
```python
from sklearn.ensemble import RandomForestClassifier

# Train model
rf_model = RandomForestClassifier(n_estimators=100, random_state=42)
rf_model.fit(X_train, y_train)

# Predict future churners
new_predictions = rf_model.predict(new_data)
```

---

## 💡 Key Insights
| Insight | Value |
|---------|-------|
| Overall Churn Rate | **26.99%** |
| Top Churn Reason | **Competitor — 761 customers** |
| Highest Churn Contract | **Month-to-Month — 46.53%** |
| Highest Churn State | **Jammu & Kashmir — 57.19%** |
| No Online Security Churn | **84.64%** |
| Age 50+ Churn Rate | **43%** |
| Predicted Future Churners | **384 customers** |

---

## 📊 Dashboard / Model / Output

### Power BI Dashboard Pages:
| Page | Description |
|------|-------------|
| **Overview** | Project summary and navigation |
| **Churn Analysis** | Historical churn patterns |
| **Summary** | Key metrics and KPIs |
| **Churn Prediction** | ML predicted churners |

### ML Model Output:
- **Algorithm:** Random Forest Classifier
- **Training Size:** 4,805 rows (80%)
- **Test Size:** 1,202 rows (20%)
- **Predicted Churners:** 384 customers
- **Output File:** `Predictions.csv`

---

## 🚀 How to Run this Project

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn joblib openpyxl
```

### Step 1 — SQL Setup
1. Install **SQL Server** and **SSMS**
2. Create database `db_Churn`
3. Import `Customer_Data.csv` using Import Wizard
4. Run the SQL scripts in order

### Step 2 — Power BI
1. Open **Power BI Desktop**
2. Connect to SQL Server → `RABIYA\SQLEXPRESS`
3. Import `vw_ChurnData` and `vw_JoinData`
4. Open `churn_Analysis.pbix`


### Step 3 — ML Model
```bash
# Open Jupyter Notebook
jupyter notebook

# Run the notebook cells in order:
# 1. Import Libraries
# 2. Load Data
# 3. Preprocessing
# 4. Train Model
# 5. Evaluate
# 6. Predict New Data
```

### Step 4 — View Predictions
- Output saved to `Predictions.csv`
- Import CSV back to Power BI
- View on **Churn Prediction** page

---


## 📈 Results & Conclusion

| Metric | Result |
|--------|--------|
| Total Customers Analysed | 6,418 |
| Total Churned | 1,732 |
| Churn Rate | 26.99% |
| New Joiners | 411 |
| Predicted Future Churners | 384 |


**Conclusion:**
- Month-to-month contract customers are most likely to churn
- Competitor influence is the #1 reason for churn
- Customers without Online Security churn at 84.64%
- The ML model successfully predicted 384 future churners
- Businesses can use these insights to run targeted retention campaigns

---

## 🔮 Future Work
- [ ] Deploy ML model as a **REST API** using Flask
- [ ] Add **real-time data** pipeline using Azure
- [ ] Implement **deep learning** model for better accuracy
- [ ] Build **automated email alerts** for at-risk customers
- [ ] Add **customer segmentation** using clustering



## 📁 Project Structure
```
churn-analysis/
│
├── SQL/
│   └── churn_analysis_queries.sql
│
├── PowerBI/
│   └── churn_Analysis.pbix
│
├── ML/
│   ├── Churn_Prediction.ipynb
│   └── Predictions.csv
│
├── Data/
│   ├── Customer_Data.csv
│   └── Prediction_Data.xlsx
│
└── README.md
```
## Dashboard Preview



## 👩‍💻 Author
**Rabiya Thul Aabitha**
- 📧 rabiyathulaabitha04@gmail.com
- 🐙 github.com/rabiyathulaabitha0

---
