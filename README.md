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
check the sales amount has any wrong value
```sql
 Select *  from sales.transactions where sales_amount<=0;
```
Screen short
here we can see that sales amount column has some negative values and zero. So I have to clean that using power BI.

let's find the currency column for sales amount in same currency or not.
```sql
 select distinct currency from sales.transactions;
```
Screen Short

Here we can see that  two types INR , US.

Let's look the transactions done in US Dollar
```sql
 select * from sales.transactions where currency='USD';
```
Only two transactions. So I decide to convert this USD to INR .

show the total revenue in chennai in the year 2020
```sql
 select sum(sales.transactions.sales_amount) from sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code='Mark001' ;
```


### Data Modeling using Power BI  
 
 ![Data Modelling](https://github.com/user-attachments/assets/2d158cea-dc2a-4da1-8c13-230e5aaff795)


### Data cleaning & Analysis using Power BI

First I did filter in the column market_name from the table Market for avoiding new york and paris as market name values because these two market names show blanks in other related columns in that table. Also these two market names appeared only one time. 

![Screenshot (3)](https://github.com/user-attachments/assets/81d62388-f8ed-4ac2-bef2-a475281841e1)

                        
when I did data analysis using sql we saw that sales amount column has some negative values and zeroe.So in power BI I use filter in sales amount column for avoiding zero or negative values.
```
= Table.SelectRows(sales_transactions, each ([sales_amount] <> -1 and [sales_amount] <> 0))
```


Another issue is in the sales amount column in transaction table has two types. I ssaw this issue when I did sql analysis. I solved this issue using Dax function in Power BI. I decided to convert USD into INR. So all the sales amount become in the same currency as INR.
So I created a new column named Normalised_sales_amnt. Converting USD to  This normalised_sales _amount column contains all values in INR. For that I convert Sales amount in USD to INR using the folloeing formula inDAX function

```
=Table.AddColumn(#"Filtered Rows1", "normalised_sales_amount", each if [currency]="USD#(cr)" then [sales_amount]*83 else [sales_amount])
```
Now the normalised column has sales amount in same currency

Finally  Data cleaning successfully completed and it is ready for finding key insights

### Creating Dashboard using Power BI



![Dashboard](https://github.com/user-attachments/assets/dba981e9-2c83-4048-8b09-b240a0b6aed1)


First I calculate Total Revenue . for that I create a new measure named 'Total Revenue'.
```
 Total Revenue = SUM('sales transactions'[Normalised_sales_amnt])
```
 
![Total Revenue](https://github.com/user-attachments/assets/5249d5a7-cef7-4c36-b673-b7e18f9af1b9)

 Then calculate Total sales quantity 
 ```
 Sales_Qty = SUM('sales transactions'[sales_qty])
```

![Sales_qty](https://github.com/user-attachments/assets/1021316f-4189-4e6d-ba3e-0ecb432b28e6)


I 


![Total  Profit](https://github.com/user-attachments/assets/ccf1ed62-179a-4cf0-bdfd-c8c36a92e151)

 
 Bar chart for showing Top 5 customers.

 ![Top 5 customers](https://github.com/user-attachments/assets/bbd34640-afb5-4dbc-81cf-ecc9cf2be894)

 
 Then finding most selling products based on sales quantity.

 
![Most selling Products](https://github.com/user-attachments/assets/24d0d545-c19a-4189-b298-d06aa6a0018f)

 
 Then use a Pie chart for identifying each zone contribute how much percentage in the total revenue.

![Revenue by zone](https://github.com/user-attachments/assets/32bfb849-28a8-4d66-a302-261b46f781a8)


Create a line graph shows Profit in each year

![Profit by year](https://github.com/user-attachments/assets/de2d58e9-6a80-4dc7-a42f-b1624e608b4b)









![Table](https://github.com/user-attachments/assets/0287fb48-b1e1-4b37-a39f-bdbe8f235608) 





Finally, I created buttons for choosing year

![Dashboard](https://github.com/user-attachments/assets/ba170fbc-ac30-4fdd-868d-b398c7876daf)











 
