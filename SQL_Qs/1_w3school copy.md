# Part 1: W3Schools SQL Lab 

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK? `SELECT CustomerName FROM Customers WHERE Country = 'UK'`

2. What is the name of the customer who has the most orders?
`SELECT CustomerName 
FROM Customers 
WHERE CustomerID = (SELECT CustomerID FROM [Orders] GROUP BY CustomerID ORDER BY count(OrderID) DESC LIMIT 1);`

3. Which supplier has the highest average product price?
`SELECT SupplierName FROM [Suppliers]
WHERE SupplierID = (SELECT SupplierID FROM [Products] GROUP BY SupplierID ORDER BY AVG(Price) DESC);`

4. How many different countries are all the customers from? (*Hint:* consider [DISTINCT](http://www.w3schools.com/sql/sql_distinct.asp).)
`SELECT COUNT(DISTINCT(Country)) FROM Customers;`

5. What category appears in the most orders?
`SELECT CategoryID, count(CategoryID) FROM

(SELECT OrderDetails.*, Products.* FROM OrderDetails
LEFT JOIN Products
ON OrderDetails.ProductID = Products.ProductID)

GROUP BY CategoryID
ORDER BY count(CategoryID) DESC
LIMIT 1;`

6. What was the total cost for each order?
`SELECT OrderID, Quantity*Price AS TotalPrice FROM

(SELECT OrderDetails.*, Products.* FROM OrderDetails
LEFT JOIN Products
ON OrderDetails.ProductID = Products.ProductID);`

7. Which employee made the most sales (by total price)?
`SELECT EmployeeID FROM

(SELECT * FROM Orders JOIN 

(SELECT OrderID, Quantity*Price AS TotalPrice FROM

(SELECT OrderDetails.*, Products.* FROM OrderDetails
LEFT JOIN Products
ON OrderDetails.ProductID = Products.ProductID)))

GROUP BY EmployeeID ORDER BY sum(TotalPrice) DESC LIMIT 1
;`

8. Which employees have BS degrees? (*Hint:* look at the [LIKE](http://www.w3schools.com/sql/sql_like.asp) operator.)
`SELECT * FROM [Employees]
WHERE Notes LIKE '% BS %';`

9. Which supplier of three or more products has the highest average product price? (*Hint:* look at the [HAVING](http://www.w3schools.com/sql/sql_having.asp) operator.)
```
SELECT * FROM 
[Suppliers] 
JOIN Products
	ON Products.SupplierID = Suppliers.SupplierID
GROUP BY Suppliers.SupplierID
HAVING count(Products.SupplierID) > 2
ORDER BY AVG(Products.Price) DESC
LIMIT 1;
```
