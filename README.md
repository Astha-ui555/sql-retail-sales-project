# sql-retail-sales-project
_**PROJECT OVERVIEW** :-_     
**Project Title:** Retail Sales Analysis     
**Database:** my_sql_project_P1    
**RDBMS:** PostgreSQL     

This project focuses on applying SQL to manage and analyze retail sales data effectively using PgSQL. It covers the complete process - from creating a structural sales database to exploring data patterns, identifying key insights, and solving business-related queries using SQL commands. The aim is to strengthen data analysis skills and gain hands-on experience with real-world datasets, making it an excellent starting point for beginners in data analytics.  

_**OBJECTIVES**:-_  
**1. Set up a retail sales database**: Create and populate a retail sales database with the provided sales data.  
**2. Data Cleaning**: Identify and remove any records with missing or null values.  
**3. Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.  
**4. Business Analysis**: Use SQL to answer specific business questions and derive insights from the sales data.  

  _**PROJECT STRUCTURE**_  

**1. Database Setup**     
**• Database Creation:** The project begins with the creation of a database named my_sql_project_P1 to store and manage retail sales records.  
**• Table Creation:** Within this database, a table named retail_sales is created to store sales information, including transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity, price per unit, cost of goods sold (COGS), and total sales amount.   

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





