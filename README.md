# SQL_Retail_sales
This project showcases SQL skills used by data analysts to explore, clean, and analyze retail sales data. It involves setting up a sales database, performing exploratory analysis, and answering business questions with SQL queries—ideal for beginners building a strong SQL foundation.

Objectives
Set up a retail sales database: Create and populate a retail sales database with the provided sales data.
Data Cleaning: Identify and remove any records with missing or null values.
Exploratory Data Analysis (EDA): Perform basic exploratory data analysis to understand the dataset.
Business Analysis: Use SQL to answer specific business questions and derive insights from the sales data.


Project Structure
1. Database Setup
Database Creation: The project starts by creating a database named p1_retail_db.
Table Creation: A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.


  -- Write a SQL query to retrieve all columns for sales made on '2022-11-05:
SELECT *
FROM project_p1.retails_sales
WHERE sale_date = '2022-11-05';

-- Write a SQL query to retrieve all transactions where the category is 'Clothing' 
-- and the quantity sold is more than 4 in the month of Nov-2022:
SELECT * from project_p1.retails_sales
WHERE category = 'Clothing'
    AND quantiy >= 4
    AND month(sale_date) ='11'
    AND year(sale_date) ='2022';
    
 -- Write a SQL query to calculate the total sales (total_sale) for each category.:  
 SELECT 
    category,
    SUM(total_sale) as net_sale
FROM project_p1.retails_sales
GROUP BY category;

-- Write a SQL query to find the average age of customers who purchased 
-- items from the 'Beauty' category.:
SELECT AVG(age) as avg_age
FROM project_p1.retail_sales
WHERE category = 'Beauty';

-- Write a SQL query to find all transactions where the total_sale is greater than 1000.:
select *  from project_p1.retails_sales
where total_sale > 1000;

-- Write a SQL query to find the total number of transactions (transaction_id) made by 
-- each gender in each category.:
SELECT category,gender,COUNT(ï»¿transactions_id) as total_trans
FROM project_p1.retails_sales
GROUP BY category,gender;


-- **Write a SQL query to find the top 5 customers based on the highest total sales **:
select customer_id,sum(total_sale) as total_sales from project_p1.retails_sales
group by customer_id
order by total_sales desc
limit 5;

-- Write a SQL query to find the number of unique customers who purchased items 
-- from each category.:
select category,count(distinct customer_id) as no_of_customers from project_p1.retails_sales
group by category;


-- Write a SQL query to calculate the average sale for each month. 
-- Find out best selling month in each year:
select * from(
select 
YEAR(sale_date) AS year,
MONTH(sale_date) AS month,
AVG(total_sale) AS Avg_sale,
RANK() OVER(PARTITION BY YEAR(sale_date) ORDER BY AVG(total_sale) DESC) AS rk
from project_p1.retails_sales
GROUP BY year,month
) as m1
where m1.rk = 1;
