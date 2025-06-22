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
3. [📊 Exploratory Data Analysis (EDA)](#-exploratory-data-analysis-eda)  
4. [🧮 Apply RFM Model](#-apply-rfm-model)  
5. [📊 Visualization & Analysis](#-visualization--analysis)  



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

| Column Name | Data Type        | Description                                                                 |
|-------------|------------------|-----------------------------------------------------------------------------|
| InvoiceNo   | object            | Unique invoice number for each transaction (6-digit). If it starts with 'C', it indicates a cancellation. |
| StockCode   | object            | Unique product (item) code (5-digit).                                      |
| Description | object            | Product (item) name.                                                       |
| Quantity    | int64             | The number of units purchased per transaction.                             |
| InvoiceDate | datetime64[ns]    | Date and time when the transaction occurred.                               |
| UnitPrice   | float64           | Price per unit of the product in sterling.                                 |
| CustomerID  | float64           | Unique 5-digit identifier for each customer.                               |
| Country     | object            | Name of the country where the customer resides.   


Sheet 2: Segmentation  

| Segment               | RFM Scores                                                                                                   |
|------------------------|--------------------------------------------------------------------------------------------------------------|
| **Champions**          | 555, 554, 544, 545, 454, 455, 445                                                                            |
| **Loyal**              | 543, 444, 435, 355, 354, 345, 344, 335                                                                       |
| **Potential Loyalist** | 553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323 |
| **New Customers**      | 512, 511, 422, 421, 412, 411, 311                                                                            |
| **Promising**          | 525, 524, 523, 522, 521, 515, 514, 513, 425, 424, 413, 414, 415, 315, 314, 313                               |
| **Need Attention**     | 535, 534, 443, 434, 343, 334, 325, 324                                                                       |
| **About To Sleep**     | 331, 321, 312, 221, 213, 231, 241, 251                                                                       |
| **At Risk**            | 255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124  |
| **Cannot Lose Them**   | 155, 154, 144, 214, 215, 115, 114, 113                                                                       |
| **Hibernating**        | 332, 322, 233, 232, 223, 222, 132, 123, 122, 212, 211                                                        |
| **Lost Customers**     | 111, 112, 121, 131, 141, 151    


---

## 📊 Exploratory Data Analysis (EDA)

### 1️⃣ Initial Exploration

To understand the data structure and assess its quality, the following initial steps were taken:

- **Dataset Overview:**
  - The dataset contains **541,909 rows** and **8 columns**.
  - Used `.info()` to check data types and null values.
  - Used `.head()` to view sample transactions.

- **Descriptive Statistics:**
  - `.describe()` revealed unusually large negative values in `Quantity` and `UnitPrice`.
  - Example: `Quantity` min = -80,995; `UnitPrice` min = -11,062 — which are not logically valid.

- **Data Type Review:**
  - No mismatched data types were detected.
  - However, some columns like `InvoiceNo`, `StockCode`, and `CustomerID` were later cast to `string` for better processing.

- **Missing & Duplicate Values:**
  - `CustomerID`: ~0.27% missing → Critical for segmentation → **to be removed**.
  - `Description`: ~25% missing → Retained (not used in RFM).
  - Duplicate rows: 5,268 duplicates found → **to be removed**.




## 🧮 Apply RFM Model  

👉🏻 Based on the insights and findings above, we would recommend the [stakeholder team] to consider the following:  

📌 Key Takeaways:  
✔️ Recommendation 1  
✔️ Recommendation 2  
✔️ Recommendation 3  

---

## 📊 Visualization & Analysis  

👉🏻 Based on the insights and findings above, we would recommend the [stakeholder team] to consider the following:  

📌 Key Takeaways:  
✔️ Recommendation 1  
✔️ Recommendation 2  
✔️ Recommendation 3
