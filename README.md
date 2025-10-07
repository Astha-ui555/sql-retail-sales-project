# sql-retail-sales-project
## **PROJECT OVERVIEW** :-     
**Project Title:** Retail Sales Analysis     
**Database:** `my_sql_project1`    
**RDBMS:** PostgreSQL     

This project focuses on applying SQL to manage and analyze retail sales data effectively using PgSQL. It covers the complete process - from creating a structural sales database to exploring data patterns, identifying key insights, and solving business-related queries using SQL commands. The aim is to strengthen data analysis skills and gain hands-on experience with real-world datasets, making it an excellent starting point for beginners in data analytics.  

## **OBJECTIVES**:-  
 **1. Set up a retail sales database**: Create and populate a retail sales database with the provided sales data.  
 **2. Data Cleaning**: Identify and remove any records with missing or null values.  
 **3. Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.  
 **4. Business Analysis**: Use SQL to answer specific business questions and derive insights from the sales data.  

  ## **PROJECT STRUCTURE**  

### **1. Database Setup**  
 
 - **Database Creation:** The project begins with the creation of a database named `my_sql_project1` to store and manage retail sales records.  
 - **Table Creation:** Within this database, a table named `retail_sales` is created to store sales information, including transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity, price per unit, cost of goods sold (COGS), and total sales amount.   
```
 CREATE DATABASE my_sql_project1;

 CREATE TABLE retail_sales
      (  transactions_id INT PRIMARY KEY,
		 sale_date	DATE,
		 sale_time	TIME,
		 customer_id  INT,	
		 gender	VARCHAR(15),
		 agE  INT,
		 category VARCHAR(15),	
		 quantiy INT,
		 price_per_unit	FLOAT,
		 cogs FLOAT,
		 total_sale FLOAT
      );
```
### Data Exploration & Cleaning

- **Record Count**: Determine the total number of records in the dataset.
- **Customer Count**: Find out how many unique customers are in the dataset.
- **Category Count**: Identify all unique product categories in the dataset.
- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.

```
SELECT*FROM retail_sales 
WHERE 
    transactions_id IS NULL OR sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR gender IS NULL OR age IS NULL OR category IS NULL OR
 quantiy IS NULL OR price_per_unit IS NULL OR cogs IS NULL OR total_sale IS NULL ;

-- Data Cleaning
DELETE FROM retail_sales
WHERE 
    transactions_id IS NULL OR sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR gender IS NULL OR age IS NULL OR category IS NULL OR
quantiy IS NULL OR  price_per_unit IS NULL OR cogs IS NULL OR total_sale IS NULL ;
```
### Data Analysis & Findings 

The following SQL queries were developed to answer specific business questions:

**Q1. Write a SQL query to retrieve all columns for sales made on '2022-11-05:**  
```
 SELECT * 
  FROM retail_sales
  WHERE sale_date = '2022-11-05';
```

   **Q2.Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022.**  
```   
  SELECT *
FROM retail_sales
WHERE category = 'Clothing'
AND
TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
AND
quantiy >= 4
```

**Q3.Write a SQL query to calculate the total sales (total_sale) for each category.**  

```
  SELECT 
     category,
	 SUM(total_sale) as net_sale,
	 COUNT(*) as total_order
	 FROM retail_sales
     GROUP BY 1
```
  
**Q4.Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**  

```
SELECT 
    ROUND(AVG(age), 2) as avg_age   
FROM retail_sales
WHERE category = 'Beauty';
```

**Q5.Write a SQL query to find all transactions where the total_sale is greater than 1000.** 

```
SELECT * FROM retail_sales
WHERE total_sale > 1000
```

**Q6. Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**   

```
SELECT 
     category,
	 gender,
	 COUNT(*) as total_trans
FROM retail_sales
GROUP BY 
      category,
	  gender
ORDER BY 1
```

**Q7.Write a SQL query to calculate the average sale for each month. Find out best selling month in each year.**  

```
SELECT 
       year,
       month,
    avg_sale
FROM 
(    
SELECT 
    EXTRACT(YEAR FROM sale_date) as year,
    EXTRACT(MONTH FROM sale_date) as month,
    AVG(total_sale) as avg_sale,
    RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) as rank
FROM retail_sales
GROUP BY 1, 2
) as t1
WHERE rank = 1
```

**Q8.Write a SQL query to find the top 5 customers based on the highest total sales.**  

```
SELECT 
    customer_id,
    SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5
```

**Q9.Write a SQL query to find the number of unique customers who purchased items from each category.**  

```
SELECT 
    category,    
    COUNT(DISTINCT customer_id) as cnt_unique_cs
FROM retail_sales
GROUP BY category
```

**Q10.Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17)**

```
WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift
```

### **Findings**

 - The dataset includes many retail transactions across categories like Clothing, Electronics, and Beauty.
 - Multiple unique customers indicate a strong and loyal customer base.
 - Clothing and Electronics are the top-selling categories, while Beauty is more popular among younger and female customers.
 - Several transactions exceed ₹1000, showing premium or bulk purchases.
 - The best-selling months are November–December (festive season).
 - Afternoon records the highest number of sales, followed by evening and morning.
 - Top 5 customers contribute a large share of total sales.


### **Report & Analysis**

- Created and cleaned the retail_sales database to remove null or incorrect records.
- Explored data using SQL queries to check total sales, unique customers, and product categories.
- Applied SQL functions like SUM, AVG, COUNT, DISTINCT, GROUP BY, and CTEs for analysis.
- Identified sales trends based on month, category, customer age, and time of day.
- Found top-performing categories, loyal customers, and peak sales periods.
- Used SQL ranking and filtering to highlight best-selling months and customer groups.


### **🏁 Conclusion**

- This project gives a clear understanding of SQL through retail sales analysis.
- It includes database creation, data cleaning, and business-focused SQL queries.
- The queries reveal key insights on sales trends, customer behavior, and product performance.
-  Overall, it shows how SQL helps in making data-driven business decisions.





