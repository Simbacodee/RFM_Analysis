# 📊 RFM Customer Segmentation | Python
---
![ChatGPT Image 21_43_18 22 thg 6, 2025](https://github.com/user-attachments/assets/4f670ab7-d3bb-4822-abdb-66503e9ea59d)




Author: Duong Chi Tuan  
Date: June 2025  
Tools Used: Python   

---

## 📑 Table of Contents  

1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  
3. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)  
4. [📊 Exploratory Data Analysis (EDA)](#-exploratory-data-analysis-eda)  
5. [🧮 Apply RFM Model](#-apply-rfm-model)  
6. [📊 Visualization & Analysis](#-visualization--analysis)  



---

## 📌 Background & Overview  

### Objective:
### 📖 What is this project about? What Business Question will it solve?

- SuperStore is a global retail company with a rapidly growing customer base. As the holiday season approaches, the Marketing team is planning to run appreciation campaigns for existing customers and identify high-potential buyers who can be nurtured into loyal customers.

- In previous years, customer segmentation was handled manually using spreadsheets due to the smaller scale of data. However, with the increasing volume of transactions and customers, manual segmentation is no longer feasible.

- To address this, the Marketing department has requested support from the Data Analytics team to automate customer segmentation. Specifically, they proposed leveraging the RFM (Recency, Frequency, Monetary) model to classify customers into meaningful groups for targeted marketing.

- This project aims to build a robust and scalable RFM segmentation pipeline using Python, enabling the business to better understand customer behavior and execute personalized marketing strategies efficiently.

### 👤 Who is this project for?  

- Marketing Manager  
- Data Analyst  
---

## 📂 Dataset Description & Data Structure  

### 📌 Data Source  
- Source: Provided dataset for E-commerce retail analysis
- Size: 541,910 rows × 8 columns (Sheet 1: E-commerce retail), additional segmentation details in Sheet 2
- Format: .xlsx (Excel file with two sheets)
### 📊 Data Structure & Relationships  

#### 1️⃣ Tables Used:  
The dataset consists of two tables (sheets):  
- Sheet 1: Ecommerce Retail – Contains transactional data from a UK-based online retail store, covering all orders between December 1, 2010 and December 9, 2011. The company specializes in selling unique all-occasion gifts. The majority of its customers are wholesalers, making this dataset well-suited for customer segmentation and purchasing behavior analysis.
- Sheet 2: Segmentation – Contains the RFM score combinations used to classify customers into different segments. Each record maps a specific RFM score (e.g., 555, 344, 211) to a customer label such as “Loyal Customer”, “At Risk”, or “New Customer”.  
#### 2️⃣ Table Schema & Data Snapshot  

Sheet 1: Ecommerce Retail  

| Column Name | Data Type | Description |  
|-------------|----------|-------------|  
| InvoiceNo   | INT      | Unique identifier for each product |  
| StockCode        | TEXT     | Product name |  
| Category    | TEXT     | Product category |  
| Price       | FLOAT    | Price per unit |  


Table 2: Sales Transactions  

👉🏻 Insert a screenshot of table schema.


---

## ⚒️ Main Process

1️⃣ Data Cleaning & Preprocessing  
2️⃣ Exploratory Data Analysis (EDA)  
3️⃣ SQL/ Python Analysis 

- First, explain codes' purpose - what they do

- Then how your query/ code & Insert screenshots of your result

- Finally, explain your observations/ findings from the results  ts findings
  
 _Describe trends, key metrics, and patterns._  

---

## 🔎 Final Conclusion & Recommendations  

👉🏻 Based on the insights and findings above, we would recommend the [stakeholder team] to consider the following:  

📌 Key Takeaways:  
✔️ Recommendation 1  
✔️ Recommendation 2  
✔️ Recommendation 3
