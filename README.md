# Sales-Data-Analysis

## Project Overview
This project is to analyse the sales data, extract necessary information about products and customers based on a combination of features. It will explore sales trends over time identify best selling products, top customers, calculate total revenue, find revenue distribution among different zones and create visualisations to present findings effectively. This project showcases my ability to manipulate and derive insights from large data sets enabling me to make data driven recommendations for optimizing sales strategies.

## Data Set
The data set contains 5 tables. Tables are Customers, Date, Markets, Products and Transactions.


## Tools
 
 MySQL 
 Power BI 

 ## steps
  ### Data Analysis using SQL
 1) I use dump sql file as data set. so I imort this dump sql file into MySQL. It will create entire data base along with the records in the system. Sales is the database name and it has 5 tables. Names of the tables are Customers, Date, Markets, Products and Transactions.

  show the records from customers table
   ```sql
   select * from sales.customers;
   ```
 check the total number of customers.
  ```sql
  select count(*) from sales.customers;
  ```
show transactions for the market name Chennai
```sql
 select * from sales.tranactions where market_code = 'Mark001';
```

  
     



















 
