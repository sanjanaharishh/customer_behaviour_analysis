# 📊 Customer Behavior Analytics Project

## 🔎 Overview

This project analyses customer shopping behaviour to identify revenue drivers, customer segments, and the impact of discounts and subscriptions on purchasing patterns.

The project demonstrates an end-to-end data workflow using:

* Python for data cleaning and feature engineering
* PostgreSQL for analytical querying
* Power BI for dashboard development

The objective was to generate actionable business insights from transactional data.


## 📁 Dataset

The dataset contains 3,900 customer transaction records with 18 features, including:

* Customer demographics (Age, Gender)
* Product details (Item Purchased, Category)
* Purchase Amount (USD)
* Review Rating
* Subscription Status
* Shipping Type
* Discount Applied
* Previous Purchases


## 🛠 Tools & Technologies

* Python (pandas, numpy, SQLAlchemy, psycopg2)
* PostgreSQL
* Power BI
* Jupyter Notebook


## ⚙️ Project Workflow

### 1️⃣ Data Cleaning & Feature Engineering (Python)

* Checked data types and missing values
* Imputed missing review ratings using median by category
* Standardised column names (snake_case format)
* Created new feature: `age_group`
* Converted purchase frequency into numeric format
* Removed redundant columns
* Loaded cleaned data into PostgreSQL

### Example Python Transformation

```python
df['review_rating'] = df.groupby('category')['review_rating'].transform(
    lambda x: x.fillna(x.median())
)
```

### 2️⃣ SQL Analysis (PostgreSQL)

Performed analytical queries to answer business questions:

* Revenue comparison by gender
* Subscriber vs Non-subscriber revenue analysis
* Discount usage rate by product
* Top 5 highest-rated products
* Shipping type performance comparison
* Customer segmentation (New, Returning, Loyal)
* Top 3 products per category using window functions
* Revenue contribution by age group

### Example SQL Query: Customer Segmentation

```sql
WITH customer_type AS (
    SELECT customer_id,
           CASE
               WHEN previous_purchases = 1 THEN 'New'
               WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
               ELSE 'Loyal'
           END AS customer_segment
    FROM customer
)
SELECT customer_segment, COUNT(*) AS total_customers
FROM customer_type
GROUP BY customer_segment;
```

Advanced SQL techniques used:

* Aggregations (SUM, AVG, COUNT)
* CASE statements
* CTEs (Common Table Expressions)
* Window functions (ROW_NUMBER)
* Subqueries


## 📊 Power BI Dashboard

The interactive dashboard presents:

### Key KPIs

* Total Customers: 4,000
* Average Purchase Amount: 59.76 USD
* Average Review Rating: 3.75

### Visual Analysis

* Revenue by Category
* Sales by Age Group
* Subscription Distribution
* Shipping Type Analysis
* Category Performance

The dashboard allows filtering by:

* Gender
* Subscription Status
* Category
* Shipping Type


## 📈 Key Insights

* Clothing category generates the highest revenue.
* Subscribed customers contribute higher total revenue.
* Express shipping customers show higher average spending.
* Loyal customers account for a significant portion of sales.
* Discounted products increase transaction frequency.


## 💡 Business Recommendations

* Introduce loyalty rewards for repeat customers.
* Optimise discount strategies to protect margins.
* Promote premium shipping for high-value customers.
* Target high-performing age groups with personalised campaigns.


## 🎯 Skills Demonstrated

* Data Cleaning & Transformation
* Feature Engineering
* SQL Analytics
* Window Functions & CTEs
* Customer Segmentation
* Business Insight Development
* Dashboard Design
* End-to-End Data Workflow
