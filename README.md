Superstore-Sales-Delivery-Analysis-with-SQL-Data-Modeling
This project focuses on analyzing retail sales and delivery performance using SQL. The objective was to identify operational inefficiencies, evaluate delivery performance, understand sales patterns across different business dimensions, and transform a raw dataset into a relational database structure to simulate real-world data systems.
Business Problem

Retail businesses need to understand:

Which factors affect delivery performance
where operational delays occur
Which products and regions drive revenue
How data can be structured for scalable analysis

This project aims to answer these questions using data analysis and database modeling.

---Dataset Overview

The dataset contains retail transaction data, including:

order details (order date, ship date, ship mode)
customer information (segment, region, location)
product hierarchy (category, sub-category, product)
sales values
🛠 Tools Used
SQL (MySQL)
Data Cleaning
Data Analysis
Relational Data Modeling
Data Preparation

The raw dataset contained inconsistencies and required cleaning.

---Key steps:

converted date fields using STR_TO_DATE
removed blank and invalid records
standardized text fields using TRIM
converted sales into a numeric format
validated shipping logic (ship_date ≥ order_date)

A clean dataset was created (superstore_clean) for analysis.

---SQL Analysis Performed
1. Delivery Performance Analysis
evaluated delivery time across shipping modes
measured average, minimum, and maximum delivery days
analyzed delivery variability using standard deviation
2. Delay Analysis
identified delayed orders (> 6 days)
calculated the delay percentage by state and city
segmented cities into High / Medium / Low delay categories
3. Sales & Segment Analysis
analyzed total sales by customer segment
compared delivery performance across segments
calculated average order value
4. Product & Category Analysis
evaluated sales by category and sub-category
identified instability in the furniture category
detected “Tables” as the key contributor to delivery variation
--- Data Modeling (JOIN Project)

The dataset was transformed into a relational structure:

customers (customer details)
orders (order and shipping information)
products (product hierarchy)
sales (transaction-level data)

Relationships were created using:

primary keys
foreign keys
multi-table joins

Analysis was revalidated using JOIN queries.

---Key Findings
Standard shipping mode shows a higher delivery time due to the volume load
Delivery delays are concentrated in specific cities, not uniformly distributed
High-delay cities can be identified using percentage-based analysis
Consumer segment generates the highest sales but shows higher variability
The furniture category has an inconsistent delivery performance
“Tables” sub-category is a major contributor to delivery instability

Business Recommendations
Optimize logistics for high-delay cities
improve handling of furniture shipments
Monitor delivery performance during high-volume shipping modes
Prioritize stable delivery strategies for high-revenue segments

Project Value

Key Insight with SQL 

1. Which customer segment generates the highest sales?
SELECT
    segment,
    ROUND(SUM(sales), 2) AS total_sales
FROM superstore_clean
GROUP BY segment
ORDER BY total_sales DESC;

Answer
Consumer segment generated the highest revenue (~1.14M)

Insight
A large portion of sales comes from individual customers, indicating strong B2C demand.

2. Which shipping mode takes the longest time?
SELECT
    ship_mode,
    ROUND(AVG(DATEDIFF(ship_date, order_date)), 2) AS avg_delivery_days
FROM superstore_clean
GROUP BY ship_mode
ORDER BY avg_delivery_days DESC;

Answer
Standard Class has the highest average delivery time (~4 days)

Insight
Standard shipping handles higher volume, which impacts delivery speed.

3. Which states have the highest delivery delays?
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

Answer
Certain states show significantly higher delay percentages (>10%)

Insight
Delivery inefficiencies are geographically concentrated and require targeted improvement.

4. Which sub-category generates the highest sales?
SELECT
    sub_category,
    ROUND(SUM(sales), 2) AS total_sales
FROM superstore_clean
GROUP BY sub_category
ORDER BY total_sales DESC;

Answer
Top-performing sub-categories contribute a large share of total revenue

Insight
Revenue is driven by a few key product segments rather than being evenly distributed.

5. Which product category shows delivery instability?
SELECT
    sub_category,
    ROUND(STDDEV(DATEDIFF(ship_date, order_date)), 2) AS delivery_variation
FROM superstore_clean
WHERE category = 'Furniture'
GROUP BY sub_category
ORDER BY delivery_variation DESC;

Answer
The furniture category shows high delivery variation, especially in specific sub-categories

Insight
Inconsistent delivery performance suggests operational issues in handling certain products.

6. Who are the top customers by sales?
SELECT
    customer_name,
    ROUND(SUM(sales), 2) AS total_sales
FROM superstore_clean
GROUP BY customer_name
ORDER BY total_sales DESC
LIMIT 10;

Answer
A small number of customers contribute significantly to total revenue

Insight
High-value customers can be targeted for retention strategies.


---This project demonstrates:

SQL-based data cleaning and transformation
analytical thinking and problem-solving
ability to derive business insights from data
understanding of relational database design and joins
