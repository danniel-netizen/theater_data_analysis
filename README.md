# Movie Theater Footfall & Food Purchase Analysis

## Project Overview

This project analyzes **movie theater customer footfall and food & beverage purchasing behavior** using **SQL and Python**.

The project follows a two-stage data analysis approach:

1. **SQL** is used to load and store the raw movie theater transaction data in a relational database and perform data extraction, transformation, and aggregation.
2. **Python** is used to perform exploratory data analysis (EDA), identify trends, create visualizations, and generate business insights.

The primary objective is to understand **monthly movie theater footfall** and determine **what food and beverage items customers purchase during their movie visits**.

---

## Problem Statement

A movie theater generates customer transactions throughout the year. Each transaction may contain information about the movie visit, customer, date, ticket, food or beverage purchased, quantity, and revenue.

The objective of this project is to analyze the transaction data to answer the following business questions:

* What is the **monthly customer footfall**?
* Which months have the **highest and lowest footfall**?
* What are the **most popular food and beverage items** purchased by customers?
* How many units of each food item are sold each month?
* Which food items generate the highest revenue?
* Does higher movie footfall result in higher food and beverage sales?
* Which months generate the highest food and beverage revenue?
* What are the major patterns and trends in customer food-purchasing behavior?

---

## Project Objectives

### 1. Data Loading

Load the raw movie theater transaction data into a relational database.

### 2. Data Storage

Design appropriate database tables and store the transaction data in SQL.

### 3. SQL Analysis

Use SQL to:

* Extract required data.
* Clean and transform data.
* Handle missing or invalid values.
* Calculate monthly customer footfall.
* Calculate monthly food-item sales.
* Calculate food and beverage revenue.
* Identify the most frequently purchased items.
* Prepare aggregated datasets for Python analysis.

### 4. Python Analysis

Use Python to perform:

* Exploratory Data Analysis (EDA)
* Monthly footfall analysis
* Food and beverage purchase analysis
* Monthly sales analysis
* Revenue analysis
* Footfall vs. food-sales analysis
* Trend analysis
* Data visualization

### 5. Business Insights

Generate meaningful insights that can help a movie theater improve:

* Food inventory planning
* Food and beverage promotions
* Staffing
* Inventory management
* Customer engagement
* Concession revenue

---

# Technology Stack

## Database

* SQL
* PostgreSQL / MySQL / SQL Server

## Programming Language

* Python

## Python Libraries

* Pandas
* NumPy
* Matplotlib
* Seaborn

## Development Environment

* Jupyter Notebook / JupyterLab
* VS Code / PyCharm

---

# Project Workflow

```text
Raw Transaction Data
        |
        v
   Data Validation
        |
        v
   SQL Database
        |
        v
 SQL Cleaning & Transformation
        |
        v
 SQL Aggregation
        |
        v
 Python / Pandas
        |
        v
 Exploratory Data Analysis
        |
        v
 Visualization
        |
        v
 Business Insights
```

---

# Data Flow

## Step 1 – Raw Data

The project starts with raw movie theater transaction data.

Potential fields may include:

* Transaction ID
* Customer ID
* Movie ID
* Movie Name
* Transaction Date
* Ticket Quantity
* Food Item
* Food Category
* Food Quantity
* Food Price
* Food Revenue

The exact columns depend on the source dataset.

---

## Step 2 – Load Data into SQL

The raw data will first be loaded into the SQL database.

Example:

```sql
CREATE TABLE movie_transactions (
    transaction_id INT,
    customer_id INT,
    movie_id INT,
    movie_name VARCHAR(255),
    transaction_date DATE,
    ticket_quantity INT,
    food_item VARCHAR(255),
    food_category VARCHAR(100),
    food_quantity INT,
    food_price DECIMAL(10,2),
    food_revenue DECIMAL(10,2)
);
```

---

# SQL Analysis

SQL will be used as the primary data preparation and querying layer.

### Monthly Footfall

Calculate the number of customers visiting the theater each month.

Example analysis:

```sql
SELECT
    EXTRACT(YEAR FROM transaction_date) AS year,
    EXTRACT(MONTH FROM transaction_date) AS month,
    COUNT(DISTINCT customer_id) AS monthly_footfall
FROM movie_transactions
GROUP BY
    EXTRACT(YEAR FROM transaction_date),
    EXTRACT(MONTH FROM transaction_date)
ORDER BY year, month;
```

### Monthly Food Sales

Determine how many food items were sold each month.

```sql
SELECT
    EXTRACT(YEAR FROM transaction_date) AS year,
    EXTRACT(MONTH FROM transaction_date) AS month,
    food_item,
    SUM(food_quantity) AS quantity_sold
FROM movie_transactions
GROUP BY
    EXTRACT(YEAR FROM transaction_date),
    EXTRACT(MONTH FROM transaction_date),
    food_item
ORDER BY year, month, quantity_sold DESC;
```

### Top Food Items

Identify the most frequently purchased food and beverage items.

```sql
SELECT
    food_item,
    SUM(food_quantity) AS total_quantity
FROM movie_transactions
GROUP BY food_item
ORDER BY total_quantity DESC;
```

### Monthly Food Revenue

```sql
SELECT
    EXTRACT(YEAR FROM transaction_date) AS year,
    EXTRACT(MONTH FROM transaction_date) AS month,
    SUM(food_revenue) AS total_food_revenue
FROM movie_transactions
GROUP BY
    EXTRACT(YEAR FROM transaction_date),
    EXTRACT(MONTH FROM transaction_date)
ORDER BY year, month;
```

---

# Python Analysis

The SQL-generated datasets will be imported into Python using Pandas.

Example:

```python
import pandas as pd

df = pd.read_sql(query, connection)
```

Python will then be used for exploratory analysis and visualization.

---

# Key Python Analysis

## 1. Monthly Footfall Analysis

Analyze customer footfall month by month.

### Questions

* Which month has the highest footfall?
* Which month has the lowest footfall?
* Are there seasonal patterns?
* How does footfall change throughout the year?

---

## 2. Food Purchase Analysis

Analyze customer food and beverage purchasing behavior.

### Questions

* What is the most popular food item?
* What is the least purchased item?
* Which food category is most popular?
* How many items are sold each month?

---

## 3. Monthly Food Sales

Analyze food sales across different months.

Example visualization:

```text
Month
 |
 |        █
 |    █   █
 |    █   █       █
 | █  █   █   █   █
 +--------------------
```

A line or bar chart can be created using Matplotlib or Seaborn.

---

## 4. Footfall vs Food Sales

Compare monthly movie theater footfall with food sales.

For example:

```text
Month | Footfall | Food Items Sold
------|----------|----------------
Jan   | 12,500   | 18,200
Feb   | 10,800   | 15,400
Mar   | 14,200   | 21,100
```

This analysis can help determine whether higher customer attendance is associated with higher food sales.

---

# Expected Visualizations

The Python analysis should include:

### Monthly Footfall

A bar chart showing:

**Month vs. Number of Customers**

### Monthly Food Sales

A line or bar chart showing:

**Month vs. Food Items Sold**

### Top Food Items

A bar chart showing:

**Food Item vs. Quantity Sold**

### Food Revenue

A monthly chart showing:

**Month vs. Food Revenue**

### Footfall vs Food Sales

A comparison chart showing:

**Monthly Footfall vs. Food Items Sold**

---

# Key Business Questions

The completed project should answer:

1. What is the monthly movie theater footfall?
2. Which month has the highest footfall?
3. Which month has the lowest footfall?
4. What food item is purchased most frequently?
5. What food item is purchased least frequently?
6. Which food category generates the most sales?
7. How do food sales change from month to month?
8. Which month generates the highest food revenue?
9. Is there a relationship between customer footfall and food sales?
10. What recommendations can be derived from the analysis?

---

# Project Structure

```text
movie-theater-analysis/
│
├── data/
│   ├── raw/
│   │   └── movie_transactions.csv
│   │
│   └── processed/
│
├── sql/
│   ├── 01_create_tables.sql
│   ├── 02_load_data.sql
│   ├── 03_data_cleaning.sql
│   ├── 04_monthly_footfall.sql
│   ├── 05_food_analysis.sql
│   └── 06_revenue_analysis.sql
│
├── python/
│   ├── data_loading.py
│   ├── data_analysis.py
│   └── visualization.py
│
├── notebooks/
│   └── movie_theater_analysis.ipynb
│
├── README.md
└── requirements.txt
```

---

# Expected Outcome

At the end of the project, the analysis should provide a clear understanding of:

* Monthly movie theater footfall
* Customer attendance trends
* Popular food and beverage items
* Monthly food-item sales
* Food and beverage revenue
* Relationship between footfall and food sales
* Seasonal purchasing patterns

The final Python notebook should contain the analysis, visualizations, and business insights derived from the SQL-prepared data.

---

# Skills Demonstrated

This project demonstrates practical skills in:

* SQL
* Relational database design
* Data loading
* Data cleaning
* SQL aggregation
* Joins and subqueries
* Window functions
* Python
* Pandas
* NumPy
* Exploratory Data Analysis
* Matplotlib
* Seaborn
* Data visualization
* Business analysis
* Data-driven decision making

---

# Conclusion

This project combines **SQL and Python** to analyze movie theater customer behavior.

SQL is used to store, clean, transform, and aggregate the transaction data, while Python is used for deeper exploratory analysis and visualization.

The final analysis provides insights into **monthly customer footfall, food and beverage purchasing patterns, sales trends, and the relationship between theater attendance and concession sales**.
