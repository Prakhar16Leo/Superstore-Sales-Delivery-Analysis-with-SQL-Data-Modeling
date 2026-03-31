# Superstore Sales Delivery Analysis (SQL)

This project focuses on analyzing retail sales and delivery performance using SQL. We aimed to identify operational inefficiencies, evaluate delivery performance, understand sales patterns across different business dimensions, and turn a raw dataset into a relational database to demonstrate real-world data systems.

## Business Problem needs to be understood:

-Which factors affect delivery performance
-where operational delays occur
-Which products and regions drive revenue
-How data can be structured for scalable analysis

#### This project aims to answer these questions using data analysis and database modeling.

---

## Dataset Overview

#### The dataset contains retail transaction data, including:

* order details (order date, ship date, ship mode)
* customer information (segment, region, location)
* product hierarchy (category, sub-category, product)
* sales values

## Tools Used
1. SQL (MySQL)
2. Data Cleaning
3. Data Analysis
4. Relational Data Modeling
5. Data Preparation

---
 
## Data Cleaning 
#### Cleaning Data by Checking Null, Blank, and Duplicate:

1. Converted date fields using STR_TO_DATE
2. Removed blank and invalid records
3. Checking for duplicates for the unique ID and Other Columns
4. standardized text fields using TRIM

#### Validating Dataset :

1. converted sales into a numeric format
2. Converting text in datatime and decimal values
3. validated shipping logic (ship_date ≥ order_date)

#### A clean dataset was created (superstore_clean) for analysis.

---

## SQL Analysis Performed

### 1. Delivery Performance Analysis

* Evaluated delivery time across shipping modes
* Measured average, minimum, and maximum delivery days
* Analyzed delivery variability using standard deviation

### 2. Delay Analysis
* identified delayed orders (> 6 days)
* calculated the delay percentage by state and city
* segmented cities into High / Medium / Low delay categories
  
### 3. Sales & Segment Analysis
* analyzed total sales by customer segment
* compared delivery performance across segments
* calculated average order value
  
### 4. Product & Category Analysis
* evaluated sales by category and sub-category
* identified instability in the furniture category
* detected “Tables” as the key contributor to delivery variation

  ---
  
## JOIN and Data Modeling

The data was structured into relational tables using primary and foreign keys:

- customers → customer_id
- orders → order_id, customer_id
- products → product_id
- sales → order_id, product_id

JOIN operations were performed using:

- INNER JOIN to combine matching records across tables
- relationships between order_id, customer_id, and product_id

Example:

```sql
SELECT c.segment, SUM(s.sales)
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN sales s ON o.order_id = s.order_id
GROUP BY c.segment;
```

---

## Why Analysis Was Performed in Two Ways

The same analysis was performed on:

1. Flat dataset (superstore_clean)
2. Relational dataset (using JOINs)

Purpose:
- to validate data consistency
- to ensure JOIN logic produces correct results
- to simulate real-world database querying

Result:
Both approaches produced consistent results, confirming that the relational model was correctly designed.

---

## Key Findings

1. Standard shipping mode shows a higher delivery time due to the volume load
2. Delivery delays are concentrated in specific cities, not uniformly distributed
3. High-delay cities can be identified using percentage-based analysis
4. Consumer segment generates the highest sales but shows higher variability
5. The furniture category has an inconsistent delivery performance
6. “Tables” sub-category is a major contributor to delivery instability

## Business Recommendations

* Optimize logistics for high-delay cities
* Improve handling of furniture shipments
* Monitor delivery performance during high-volume shipping modes
* Prioritize stable delivery strategies for high-revenue segments

## Project Value

### Key Insight with SQL 

#### 1. Which customer segment generates the highest sales?
   
 ```
SELECT segment, 
 ROUND(SUM(sales), 2) AS total_sales
 FROM superstore_clean`
 GROUP BY segment. 
 ORDER BY total_sales DESC;
```
#### Answer
Consumer segment generated the highest revenue (~1.14M)

#### Insight
A large portion of sales comes from individual customers, indicating strong B2C demand.

#### 2. Which shipping mode takes the longest time?
```
SELECT
ship_mode,
ROUND(AVG(DATEDIFF(ship_date, order_date)), 2) AS avg_delivery_days
FROM superstore_clean
GROUP BY ship_mode
ORDER BY avg_delivery_days DESC;
```

#### Answer
Standard Class has the highest average delivery time (~4 days)

#### Insight
Standard shipping handles higher volume, which impacts delivery speed.

#### 3. Which states have the highest delivery delays?
```
SELECT
    state,
    COUNT(*) AS total_orders,
    SUM(CASE WHEN DATEDIFF(ship_date, order_date) > 6 THEN 1 ELSE 0 END) AS delayed_orders,
    ROUND(
        SUM(CASE WHEN DATEDIFF(ship_date, order_date) > 6 THEN 1 ELSE 0 END) * 100.0 / COUNT(*),
        2
    ) AS delay_percentage
FROM superstore_clean
GROUP BY state
ORDER BY delay_percentage DESC;
```

#### Answer
Certain states show significantly higher delay percentages (>10%)

#### Insight
Delivery inefficiencies are geographically concentrated and require targeted improvement.

#### 4. Which sub-category generates the highest sales?

```
SELECT
sub_category,
ROUND(SUM(sales), 2) AS total_sales
FROM superstore_clean
GROUP BY sub_category
ORDER BY total_sales DESC;
```
#### Answer
Top-performing sub-categories contribute a large share of total revenue

#### Insight
Revenue is driven by a few key product segments rather than being evenly distributed.

#### 5. Which product category shows delivery instability?
```
SELECT
sub_category,
ROUND(STDDEV(DATEDIFF(ship_date, order_date)), 2) AS delivery_variation
FROM superstore_clean
WHERE category = 'Furniture'
GROUP BY sub_category
ORDER BY delivery_variation DESC;
```

#### Answer
The furniture category shows high delivery variation, especially in specific sub-categories

#### Insight
Inconsistent delivery performance suggests operational issues in handling certain products.

#### 6. Who are the top customers by sales?
```
SELECT
customer_name,
ROUND(SUM(sales), 2) AS total_sales
FROM superstore_clean
GROUP BY customer_name
ORDER BY total_sales DESC
LIMIT 10;
```

#### Answer
A small number of customers contribute significantly to total revenue

#### Insight
High-value customers can be targeted for retention strategies.

---

### This project demonstrates:

SQL-based data cleaning and transformation
analytical thinking and problem-solving
ability to derive business insights from data
understanding of relational database design and joins

### Project Value

#### This project demonstrates:

* Strong SQL fundamentals
* Understanding of relational database design
* Ability to solve real-world business problems using data
* Analytical thinking and structured problem-solving

---
## Key insights with Image

#### Shiping Analysis showing different modes  
<img width="687" height="134" alt="image" src="https://github.com/user-attachments/assets/97a27476-eb41-451a-8a0a-2c32741760f7" />

#### Shiping mode showing the highest Delay 
<img width="381" height="129" alt="image" src="https://github.com/user-attachments/assets/c7967e9c-94e9-45e1-b4ec-07cb0751c218" />

#### Sub-categories analysis 
<img width="702" height="132" alt="image" src="https://github.com/user-attachments/assets/a8043b93-f383-4033-9db4-1acd73011e96" />

#### Total sale by region 
<img width="191" height="132" alt="image" src="https://github.com/user-attachments/assets/5550f304-cce0-435f-81d8-9d6820a2a957" />

#### Top Sales by State
<img width="243" height="182" alt="image" src="https://github.com/user-attachments/assets/125959d3-b224-42b5-a19b-3600d67ca143" />

#### Top sales by Product 
<img width="431" height="172" alt="image" src="https://github.com/user-attachments/assets/d886dae6-f7d8-40f7-9d74-a66440557d83" />
