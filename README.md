# Sales First - Self-Service Business Intelligence

Step by step Self-Service BI implementation using Microsoft Power BI

## Simulate ETL

> IT department has implemented an ETL solution for loading data into the data warehouse. ETL solution is scheduled to execute every day during off-peak hours.

For the demonstration lets add some sales valuesf for ***December 2018***.
![sales by order date](images/sales_order_date.png)

Lets add same sales values from ***December 2016***. Execute the following.

```sql
SELECT *
INTO dbo.sales_temp
FROM dbo.FactInternetSales
WHERE YEAR(OrderDate) = 2016 and MONTH(OrderDate) = 12

UPDATE dbo.sales_temp
SET orderdate = DATEADD(YY, +2, orderdate)

INSERT INTO dbo.FactInternetSales
SELECT * FROM dbo.sales_temp
```

Now execute the following to check the insertion.

```sql
SELECT TOP (10) *
FROM [SalesFirstDW].[dbo].[FactInternetSales]
ORDER BY OrderDate DESC
```

Results
![sales by order date](images/check_insertion.png)
