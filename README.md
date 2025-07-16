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

**Step 1:** Remove duplicate rows  

**Step 2:** Drop rows with missing values  

**Step 3:** Filter rows where Quantity > 0 and UnitPrice > 0  

**Step 4:** Keep rows with valid StockCode (5-digit numeric format)  

**Step 5:** Detect outliers in Quantity and UnitPrice  

![image](https://github.com/user-attachments/assets/1fd7f406-6c46-4d02-abcf-c7e91fa758ce)  

![image](https://github.com/user-attachments/assets/292c3f42-47f5-41a5-8052-117567d62721)

**Step 6:** Handle outliers using appropriate techniques

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

→ Customers with the **lowest recency values** (i.e., most recent purchases) receive **R = 5**, and those with the **highest values** receive **R = 1**.

**Frequency (F):** Customers who purchase more often are more loyal.  

→ The **most frequent buyers** receive **F = 5**, and the **least frequent** receive **F = 1**.

**Monetary (M):** Customers who spend more contribute more value.  

→ The **highest spenders** receive **M = 5**, and the **lowest spenders** receive **M = 1**.

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

### 1. Customer Segment Distribution

![image](https://github.com/user-attachments/assets/fd272775-091f-4871-b153-6237e07f8ea5)  

### 2. Recency by Segment  

![image](https://github.com/user-attachments/assets/bb5baae4-21be-4e7c-a5b8-44e5552ea045)  

### 3. Frequency by Segment

![image](https://github.com/user-attachments/assets/d2d8ef1f-834f-4013-96b2-486e3f25a6ce)

### 4. Monetary by Segment  

![image](https://github.com/user-attachments/assets/73d36f66-549e-417f-820f-7701f4f692aa)  

This table provides a detailed overview of each customer segment based on their average **Recency**, **Frequency**, and **Monetary** values, along with behavioral interpretation and recommended actions.

| Segment               | Recency (days) | Frequency (orders) | Monetary (£) | Behavior Interpretation                                                                 | Suggested Action                                                   |
|-----------------------|----------------|---------------------|--------------|------------------------------------------------------------------------------------------|--------------------------------------------------------------------|
| **Champions**         | 32.6           | 246.4               | 2,640,167    | Recently purchased, very frequent, very high spender → **top-tier customers**           | Offer VIP perks, exclusive deals, loyalty upgrades                 |
| **Loyal**             | 60.2           | 108.8               | 622,787      | Consistently engaged and spending → **loyal and reliable**                              | Maintain relationship, cross-sell, reward with incentives          |
| **Potential Loyalist**| 51.9           | 45.9                | 215,402      | Recently engaged, moderate activity → **potential long-term customer**                  | Nurture with emails, offer product bundles                         |
| **New Customers**     | 49.8           | 9.3                 | 49,708       | Recently made first purchase → **still exploring**                                      | Welcome emails, onboarding flow, personalized recommendations      |
| **Promising**         | 29.2           | 19.0                | 32,642       | Recently returned but still low activity                                                 | Small discounts, showcase trending items                          |
| **Need Attention**    | 52.2           | 52.3                | 215,526      | Previously active, now declining → **signs of disengagement**                           | Send reminder emails, recommend new or trending products           |
| **At Risk**           | 175.4          | 74.6                | 413,276      | Used to buy frequently and spend a lot → **risk of churn**                              | Win-back campaigns, feedback surveys                               |
| **Cannot Lose Them**  | 263.6          | 91.9                | 59,857       | VIP customers who haven’t purchased in a long time → **high retention priority**        | Send personal messages, exclusive win-back offers                  |
| **About To Sleep**    | 101.7          | 20.3                | 24,333       | Low engagement, infrequent purchases → **may become inactive soon**                     | Light re-engagement campaigns, send helpful reminders              |
| **Hibernating**       | 174.0          | 19.8                | 259,601      | Long inactive, low value → **low potential recovery**                                   | Run discount campaigns, consider excluding from future campaigns   |
| **Lost Customers**    | 293.5          | 8.2                 | 50,352       | Almost no recent activity → **very low value**                                          | Exclude from marketing efforts, clean from list                    |                          |

---
## 💡 Insight & Recommendation  

To simplify customer segmentation and enhance strategic planning efficiency, the original RFM segments have been consolidated into broader groups based on behavioral characteristics. Maintaining too many detailed segments can hinder decision-making, disperse resources, and reduce implementation effectiveness. Grouping customers with similar behaviors, engagement levels, and value contributions allows for clearer prioritization and more effective allocation of budgets, personnel, and marketing efforts. This approach not only streamlines the analytical framework but also ensures better alignment between customer value and investment strategy.

#### **1. Core Value Customers**  
**Includes:** Champions, Loyal, Potential Loyalist  
**Reason for grouping:** These customers purchase frequently, spend significantly, and are highly engaged or show strong long-term potential. They generate most of the revenue and should be prioritized for retention and value maximization.  

#### **2. Nurture & Growth**  
**Includes:** New Customers, Promising, Need Attention  
**Reason for grouping:** These customers are either new, recently re-engaged, or starting to decline. They hold potential for growth if nurtured properly through engagement and personalized offers.  

#### **3. At Risk & Retention**  
**Includes:** At Risk, Cannot Lose Them  
**Reason for grouping:** Previously high-value customers who haven't purchased for a while. They are at high risk of churn and require immediate win-back strategies to restore engagement.  

#### **4. Churned / Low Value**  
**Includes:** About To Sleep, Hibernating, Lost Customers  
**Reason for grouping:** These customers have low engagement, low spending, and long inactivity. They offer limited recovery potential and should be deprioritized or removed from active campaigns.  

### 🙋‍♂️ Customer Segmentation Strategy  

#### **1. Core Customers (Champions, Loyal, Potential Loyalist)**
**Traits:** Buy frequently, purchased recently, and spend a lot.  
**Strategy:**
- Maintain strong relationships with regular appreciation or loyalty offers.  
- Encourage product reviews or referrals.  
- Prioritize them when launching new products or campaigns.

#### **2. Nurture & Develop (New Customers, Promising, Need Attention)**
**Traits:** Recently purchased or showing early potential but not consistent yet.  
**Strategy:**
- Send welcome emails and product recommendations.  
- Offer a small discount to encourage a second purchase.  
- Send gentle reminders if inactive for a short time.

#### **3. At Risk of Churning (At Risk, Cannot Lose Them)**
**Traits:** Used to buy often or spend a lot but haven’t purchased in a while.  
**Strategy:**
- Send a “We miss you” message with a time-limited offer.  
- Ask for feedback to understand why they stopped purchasing.  
- Try to re-engage with a valuable incentive.

#### **4. Low or Lost Value (About to Sleep, Hibernating, Lost Customers)**
**Traits:** Inactive for a long time, low spenders.  
**Strategy:**
- Send a simple reactivation offer or final discount.  
- If no response over time, stop investing in this group.  
- Focus resources on higher-potential segments.


### 🏢 Business Recommendation  

For a global retail company like SuperStore, which serves a large and diverse customer base, identifying the most impactful metric within the RFM model is essential for effective marketing and sales strategies. Among the three metrics (Recency, Frequency, and Monetary), Recency should be the top priority.

Recency measures how recently a customer made a purchase. This is a strong indicator of engagement. Customers who bought recently are much more likely to respond to marketing campaigns, take advantage of promotions, and make repeat purchases. In contrast, even if a customer has purchased frequently or spent a lot in the past, a long period of inactivity may signal a loss of interest.

By focusing on Recency first, teams can identify active or “warm” customers and allocate resources to those with a higher chance of conversion.


