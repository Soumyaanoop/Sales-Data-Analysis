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

First I calculate Total Revenue . for that I create a new measure named 'Total Revenue'.
```
 Total Revenue = SUM('sales transactions'[Normalised_sales_amnt])
```
 ![Total_Revenue](https://github.com/user-attachments/assets/d77897da-357a-4487-a72a-5b477ecb7062) 

 Then calculate Total sales quantity 
 ```
 Sales_Qty = SUM('sales transactions'[sales_qty])
```
![Sales_qty (2)](https://github.com/user-attachments/assets/43d0eb7b-0122-4fcc-a0e1-a6c933cdfa0a) 


I use Slicer for choosing time period. It helps to find sales data like revenue, profit, sales qty etc between particular time period.


 ![Time_period](https://github.com/user-attachments/assets/72c89328-018a-41fc-abe1-41572be5cd94) 

 Bar chart for showing Top 5 customers.

 ![Top_customers](https://github.com/user-attachments/assets/ba680f75-a264-4d09-8a93-a579d7f9d30a) 

 Then finding most selling products based on sales quantity.

 ![Sales_qty](https://github.com/user-attachments/assets/894e3ffc-8cc7-4cea-9e0a-ba3614dd42c2) 

 Then use a Pie chart for identifying each zone contribute how much percentage in the total revenue.

![Revenue by Zone](https://github.com/user-attachments/assets/b818603d-99a0-45fc-9b37-9e79132beef7) 

Create a line graph shows revenue in each year.

![Revenue by year](https://github.com/user-attachments/assets/7668eae7-81af-4e40-8b36-1e2c45cf5cdc)




















 
