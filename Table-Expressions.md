## Table Expressions Using WITH

The CTE was introduced into standard SQL in order to simplify various classes of SQL Queries for which a derived table just wasn't suitable. For some reason, it can be difficult to grasp the techniques of using it. Well, that's before Rob Sheldon explained it all so clearly for us.

Introduced in SQL Server 2005, the common table expression (CTE) is a temporary named result set that you can reference within a SELECT, INSERT, UPDATE, or DELETE statement. You can also use a CTE in a CREATE VIEW statement, as part of the view’s SELECT query. In addition, as of SQL Server 2008, you can add a CTE to the new MERGE statement.

SQL query that you name and use in a longer quiery

You define CTEs by adding a WITH clause directly before your SELECT, INSERT, UPDATE, DELETE, or MERGE statement. The WITH clause can include one or more CTEs, as shown in the following syntax:
```
WITH cte_name AS (
  -- select query goes here
  )
  
  ---use CTEs like a table
  SELECT * FROM cte_name
```

Ex:
```SQL
WITH product_details AS (
  SELECT ProductName, CategoryName, UnitPrice, UnitsInStock
  FROM Products
  JOIN Categories ON PRODUCTS.CategoryId = Categories.Id
  WHERE Products.Discontinued = 0
  )
  
SELECT CategoryName, COUNT(*) AS unique_product_count, SUM(UnitsInStock) AS stock_count
FROM product_details
GROUP BY CategoryName
ORDER BY unique_product_count;
```

##
