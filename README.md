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
  # 1.Monthly Sales Trend (CTE)   
  With monthly_sales As(  
  select    
        Date_Trunc('month',sale_date)
  As month,  
        sum(quantity * price) As  
    total_sales  
       from sales  
       GROUP BY Date_Trunc('month',sale_date))  
       select * from monthly_sales  ORDER BY month;
       
       
        
  

  
  
  
  
  
  
