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
 Screen Short

### Data cleaning & Analysis using Power BI

First I did filter in the column market_name from the table Market for avoiding new york and paris as market name values because these two market names show blanks in other related columns in that table. Also these two market names appeared only one time. 
                        Screen short
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



                        
   
     



















 
