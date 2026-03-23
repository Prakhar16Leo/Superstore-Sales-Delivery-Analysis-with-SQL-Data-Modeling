--- Superstore-Sales-Delivery-Analysis-with-SQL-Data-Modeling
This project focuses on analyzing retail sales and delivery performance using SQL. The objective was to identify operational inefficiencies, evaluate delivery performance, and understand sales patterns across different business dimensions, and also to transform a raw dataset into a relational database structure to simulate real-world data systems.
Business Problem

---Retail businesses need to understand:

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

---This project demonstrates:

SQL-based data cleaning and transformation
analytical thinking and problem-solving
ability to derive business insights from data
understanding of relational database design and joins
