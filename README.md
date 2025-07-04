# 📊 E-commerce Customer Segmentation (Python)
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
  
<details>
  <summary><strong>Sheet 1: Ecommerce Retail</strong></summary>

| Column Name | Data Type        | Description                                                                 |
|-------------|------------------|-----------------------------------------------------------------------------|
| `InvoiceNo`   | object         | Unique invoice number for each transaction (6-digit). If it starts with 'C', it indicates a cancellation. |
| `StockCode`   | object         | Unique product (item) code (5-digit).                                      |
| `Description` | object         | Product (item) name.                                                       |
| `Quantity`    | int64          | The number of units purchased per transaction.                             |
| `InvoiceDate` | datetime64[ns] | Date and time when the transaction occurred.                               |
| `UnitPrice`   | float64        | Price per unit of the product in sterling.                                 |
| `CustomerID`  | float64        | Unique 5-digit identifier for each customer.                               |
| `Country`     | object         | Name of the country where the customer resides.                            |

</details>

<details>
  <summary><strong>Sheet 2: Segmentation</strong></summary>

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
| **Lost Customers**     | 111, 112, 121, 131, 141, 151                                                                                 |

</details>   

---

## 📊 Exploratory Data Analysis (EDA)

### 1️⃣ Initial Exploration
[In 1]:  

```python

# Check the general information of df
ecommerce.info()
```
[Out 1]:  

![image](https://github.com/user-attachments/assets/cd73860d-94ca-409a-a685-936dc82d176c)  

[In 2]:  

```python

# Check data summary
ecommerce.describe()
```
[Out 2]:  

![image](https://github.com/user-attachments/assets/213d6feb-c51c-4e71-aca3-b080cac02121)  

[In 3]:  

```python

# Print the first five rows of the dataset
ecommerce.head()
```
[Out 3]:  

![image](https://github.com/user-attachments/assets/9cafe599-3e0f-4af5-bc2e-27023c91e530)
 
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
  - `CustomerID`: ~0.27% missing → Critical for segmentation.
  - `Description`: ~25% missing → Retained (not used in RFM).
  - Duplicate rows: 5,268 duplicates found.

- **Outliers Identified:**
  - `Quantity`: Values range from **-80,995** to **80,995**, with a median of just **3**. This wide spread and the presence of negative values indicate outliers, often linked to cancelled transactions.
  - `UnitPrice`: Ranges from **-11,062** to **38,970**, while 75% of prices are below **4.13**. These extremes suggest likely data entry errors or invalid records.

### 2️⃣ Data Cleaning

The following steps were performed to clean the dataset and prepare it for segmentation:  

Step 1: Remove duplicate rows  

Step 2: Drop rows with missing values  

Step 3: Filter rows where Quantity > 0 and UnitPrice > 0  

Step 4: Keep rows with valid StockCode (5-digit numeric format)  

Step 5: Detect outliers in Quantity and UnitPrice  

![image](https://github.com/user-attachments/assets/1fd7f406-6c46-4d02-abcf-c7e91fa758ce)  

![image](https://github.com/user-attachments/assets/292c3f42-47f5-41a5-8052-117567d62721)

Step 6: Handle outliers using appropriate techniques

## 🧮 Apply RFM Model  

### 📌 What is RFM?

Helps identify the most valuable customers for marketers by analyzing customer behavior.

- **Recency:** When was the customer’s last purchase?

→ Indicates the level of engagement and potential interest. Customers who purchased recently are more likely to respond positively to marketing campaigns and promotions.

- **Frequency:** How often does the customer make a purchase?

→ Measures loyalty and long-term engagement. Frequent buyers tend to have higher retention and can be targeted with loyalty programs or exclusive offers.

- **Monetary:** How much does the customer spend?

→ Reflects the value and revenue contribution of the customer. High spenders contribute significantly to total revenue and may deserve special perks or recognition.

The objective is to segment customers based on their activity and value to facilitate targeted marketing and retention strategies.  

### 🧮 Main Process  

#### Step 1: Calculating the three RFM behavioral metrics  

- **Recency:** Number of days since the customer's most recent purchase up to the analysis date.

- **Frequency:** Total number of orders the customer has placed up to the analysis date.

- **Monetary:** Total revenue the customer has spent up to the analysis date.

![image](https://github.com/user-attachments/assets/a2f64a44-d3ff-4df2-b79f-faf1d29da37b)  

#### Step 2: Scoring customers based on RFM values  

After calculating the Recency, Frequency, and Monetary values, each customer is assigned an R, F, and M score using quintiles — dividing all customers into five equally sized groups for each metric.

**Why use quintiles instead of quartiles or deciles?**  

✅ Balanced granularity: Quintiles provide enough segmentation without overcomplicating the model.

✅ Easy to interpret: A consistent score range from 1 to 5 makes the results intuitive and easy to communicate.

✅ Standardized scoring: All three metrics are mapped to the same scale, making them easy to combine into a unified RFM score.

**How scores are assigned:**  

**Recency (R):** Customers who purchased more recently are considered more engaged.  

→ Customers with the lowest recency values (i.e., most recent purchases) receive R = 5, and those with the highest values receive R = 1.

**Frequency (F):** Customers who purchase more often are more loyal.  

→ The most frequent buyers receive F = 5, and the least frequent receive F = 1.

**Monetary (M):** Customers who spend more contribute more value.  

→ The highest spenders receive M = 5, and the lowest spenders receive M = 1.

![image](https://github.com/user-attachments/assets/258cd7ea-867b-4e9a-ae1a-6e50b99f26a9)  

#### Step 3: Creating the combined RFM score  

After assigning individual scores for **Recency**, **Frequency**, and **Monetary**, the three scores are concatenated into a three-digit string. Each customer is assigned a unique RFM score (e.g., 543, 215, 355) that represents their purchasing behavior.  

![image](https://github.com/user-attachments/assets/9fdc5f59-ee58-40b5-a14a-70d323d1a6e3)  

#### Step 4: Assigning customer segments  

After generating the RFM score (e.g., 543, 215...), each score is matched to a specific customer group based on a predefined segmentation table.

This makes it easy to identify which group each customer belongs to, allowing the business to apply appropriate strategies such as offering promotions, providing personalized care, or encouraging repeat purchases.  

![image](https://github.com/user-attachments/assets/70911ad7-4ad0-42cb-8ad7-22856f49eb0f)

---

## 📊 Visualization & Analysis  

![image](https://github.com/user-attachments/assets/f19a0546-39f3-42b2-ae6a-65f7fd2a6a91)

**🧠 Insights**

- 🔵 **Hibernating Customers** (20.29%) are the **largest group**  
  → Long-inactive, low-value customers.

- 🟢 **Champions** (19.41%)  
  → Highly engaged, recent, and top-spending customers.

- 🟡 **Potential Loyalists + Loyal Customers** (~20.6%)  
  → High potential for long-term retention if nurtured well.

- 🔴 **Lost + At Risk** (~19.3%)  
  → Previously active but now disengaged — high risk of churn.

- 🟠 **New Customers** (7.66%)  
  → Low proportion, indicating limited recent acquisition.

**✅ Recommended**

- 🎯 *Retain Champions & Loyal Customers*  
  → Create VIP benefits, offer exclusive early-access promotions.

- 🔄 *Re-engage Hibernating & At-Risk*  
  → Run "We Miss You" campaigns with time-sensitive offers.

- 🌱 *Nurture New & Potential Loyalists*  
  → Use onboarding flows, referral incentives, and personalized emails.

- 🧩 *Investigate Lost Customers*  
  → Collect feedback on churn, run win-back strategies.

- 🚀 *Improve Acquisition Funnel*  
  → Invest in SEO/ads, optimize first-time purchase experience.

