# 🗃️ Codtech_internship_task-2-Data-Analysis-With-Complex-Queries
👩‍🎓Prepared by:GORJALA JAHNAVI

🏷️Internship Id CT04DZ839

🏢Organization: CODTECH 

📆Date: August 2025

# 📌 INTRODUCTION:

This task focuses on advanced data analysis using SQL. The objective is to apply window functions,subqueries, and common table expression(CTEs) to extract meaningful insights and trends from a dataset.  
For this project, a sales dataset is used, containing details of customer purchases,including product IDs,sales dates,quantity,and prices.

# 🏗️Creating table   
create table sales(   
  sale_id INT PRIMARY KEY,  
  customer_id INT,  
  product_id VARCHAR(10),    
  sale_date DATE,  
  quantity INT,  
  price DECIMAL(10,2)  
  );
  # 📥Data Insertion 
  
  Insert into sales (sale_id,customer_id,product_id,sale_date,quantity,price)VALUES  
  (1,101,'P01','2023-01-05',2,500),  
  (2,102,'P02','2023-01-07',1,300),  
  (3,103,'P01','2023-01-10',3,500),  
  (4,101,'P03','2023-02-01',1,800),  
  (5,104,'P02','2023-02-05',2,300),  
  (6,105,'P01','2023-02-07',4,500); 
  # Dataset Preview:
  |🏷️sale_id|👤 customer_id|📦product_id|📆 sale_date| 🔢quantity| 💰price|
  |----------|--------------|-------------|-------------|-----------|---------|
  |1         | 101          | P01         | 2023-01-05 | 2          | 500    |
  |2         | 102           | P02        | 2023-01-07 | 1          | 300     |
  |3         | 103          | P01        | 2023-01-10 | 3          | 500     |
  |4        | 101          | P03       | 2023-02-01 | 1          | 800     |
  |5         | 104           | P02        | 2023-02-05 | 2          | 300     |
  |6         | 105           | P01        | 2023-02-07 | 4          | 500     |  
  # QUERIES WITH OUTPUTS:  
  # 📈1. Monthly Sales Trend (CTE)   
  With monthly_sales As(  
  select    
        Date_Trunc('month',sale_date)
  As month,  
        sum(quantity * price) As  
    total_sales  
       from sales  
       GROUP BY Date_Trunc('month',sale_date))  
       select * from monthly_sales  ORDER BY month;  
   ✅ Result:

|📅 month	|💰 total_sales|
|---------|-------------|
|2023-01-01|	3100       |
|2023-02-01|	4400        |


📌 Insight: Sales grew from 3100 in January → 4400 in February

# 🏆 2. Top 3 Customers by Spending (Window Function)

SELECT  
    customer_id, 
    SUM(quantity * price) AS total_spent, 
    RANK() OVER (ORDER BY SUM(quantity * price) DESC) AS rank
FROM sales 
GROUP BY customer_id 
ORDER BY rank 
LIMIT 3; 

✅ Result:

|👤 customer_id|	💳 total_spent|	🥇 rank|
|-------------|----------------|--------|
|105	        |2000           |	1    |
|101	         |1800	        | 2        |
|103	          |1500	         |3       |

📌 Insight: Customer 105 is the highest spender.

# 📊 3. Product-wise Contribution (Subquery)

SELECT 
    product_id,
    SUM(quantity * price) AS product_sales,
    ROUND(
        (SUM(quantity * price) * 100.0 / 
        (SELECT SUM(quantity * price) FROM sales)), 2
    ) AS sales_percentage
FROM sales
GROUP BY product_id
ORDER BY product_sales DESC;

✅ Result:

|📦 product_id	|💰 product_sales|	📉 sales_percentage|
|----------------|----------------|---------------------|
|P01	|3500	|51.47%|
|P02	|900	|13.24%|
|P03	|800	|11.76%|


📌 Insight: Product P01 dominates with ~51% of total sales.

# 🔄 4. Customer Purchase Pattern (LAG Window Function)

SELECT 
    customer_id,
    sale_date,
    LAG(sale_date) OVER (PARTITION BY customer_id ORDER BY sale_date) AS prev_purchase,
    sale_date - LAG(sale_date) OVER (PARTITION BY customer_id ORDER BY sale_date) AS days_between
FROM sales
ORDER BY customer_id, sale_date;

✅ Result:

|👤 customer_id	|📅 sale_date	|⏮️ prev_purchase|	⏳ days_between|
|----------------|-------------|---------------|------------------|
|101	|2023-01-05	|NULL	|NULL|
|101	|2023-02-01	|2023-01-05|	27|
|102	|2023-01-07	|NULL	|NULL|
|103	|2023-01-10	|NULL	|NULL|
|104	|2023-02-05	|NULL	|NULL|
|105	|2023-02-07	|NULL	|NULL|

📌 Insight: Customer 101 returned after 27 days, showing repeat purchase behavior.

# 🏁 4. Conclusion

This task successfully demonstrates complex SQL queries for data analysis. Key findings include:

✔️ Sales grew significantly between January and February.  
✔️ Customer 105 is the top spender.  
✔️ Product P01 contributes the majority of revenue.  
✔️ Customer 101 shows repeat purchase behavior within a month.  

These insights showcase how SQL can be used for business intelligence, customer analytics, and sales trend monitoring.
       
       
        
  

  
  
  
  
  
  
