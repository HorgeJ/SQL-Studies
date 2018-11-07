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

### Subquery Example
```SQL
SELECT 
  all_orders.EmployeeID, 
  Employees.LastName,
  all_orders.order_count AS total_order_count, 
  late_orders.order_count AS late_order_count
  FROM (
    SELECT EmployeeID, COUNT(*) AS order_count
    FROM Orders
    GROUP BY EmployeeID
  ) all_orders
  JOIN (
    SELECT EmployeeID, COUNT(*) AS order_count
    FROM Orders
    WHERE RequiredDate <= ShippedDate
    GROUP BY EmployeeID 
  ) late_orders
  ON all_orders.EmployeeID = late_orders.employeeID
  JOIN Employees
  ON all_orders.EmployeeId = Employees.Id

```

### Subquery Example Rewritten with Common Table Expressions
```SQL
WITH all_orders AS (
    SELECT EmployeeID, COUNT(*) AS order_count
    FROM Orders
    GROUP BY EmployeeID
),
  late_orders AS (
    SELECT EmployeeID, COUNT(*) AS order_count
    FROM Orders
    WHERE RequiredDate <= ShippedDate
    GROUP BY EmployeeID 
)
SELECT 
  Employees.ID, LastName, 
  all_orders.order_count AS total_order_count,
  late_orders.order_count AS late_order_count
FROM Employees
JOIN all_orders ON Employees.ID = all_orders.EmployeeID 
JOIN late_orders ON Employees.ID = late_orders.EmployeeID
```

## CTEs Refrencing a CTE
```SQL
WITH 
  all_sales AS (
    SELECT Orders.Id AS OrderId, Orders.EmployeeId,
     SUM(OrderDetails.UnitPrice * OrderDetails.Quantity) AS invoice_total
     FROM Orders 
     JOIN OrderDetails ON Orders.id = OrderDetails.OrderId
     GROUP BY Orders.ID
  ), 
  revenue_by_employee AS (
     SELECT EmployeeId, SUM(invoice_total) AS total_revenue
     FROM all_sales
     GROUP BY EmployeeID
  ), 
  sales_by_employee AS (
     SELECT EmployeeId, COUNT(*) AS sales_count
     FROM all_sales
     GROUP BY EmployeeId
  )
SELECT 
  Employees.Id,
  Employees.LastName, 
  revenue_by_employee.total_revenue,
  sales_by_employee.sales_count,
  revenue_by_employee.total_revenue/sales_by_employee.sales_count AS    
                                               avg_revenue_per_sale
FROM revenue_by_employee
JOIN sales_by_employee ON revenue_by_employee.EmployeeId = sales_by_employee.EmployeeId
JOIN Employees ON revenue_by_employee.EmployeeId = Employees.Id
ORDER BY total_revenue DESC
```
