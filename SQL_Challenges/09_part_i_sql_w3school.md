# Challenge Set 9
## Part I: W3Schools SQL Lab 

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK?

SELECT CustomerName FROM Customers
WHERE Country = 'UK';

CustomerName
Around the Horn
B's Beverages
Consolidated Holdings
Eastern Connection
Island Trading
North/South
Seven Seas Imports

2. What is the name of the customer who has the most orders?

SELECT Customers.CustomerName, Orders.CustomerID, COUNT(Orders.CustomerID) FROM Orders
INNER JOIN Customers on Orders.CustomerID=Customers.CustomerID
GROUP BY Orders.CustomerID
ORDER BY COUNT(Orders.CustomerID) DESC;

CustomerName	CustomerID	COUNT(*)
Ernst Handel	20	        10

3. Which supplier has the highest average product price?

SELECT Suppliers.SupplierName, Products.SupplierID, AVG(Products.Price) FROM [Products]
INNER JOIN Suppliers on Products.SupplierID=Suppliers.SupplierID
GROUP BY SupplierName
ORDER BY AVG(Products.Price) DESC;

SupplierName	            SupplierID	  AVG(Products.Price)
Aux joyeux ecclésiastiques	18	          140.75

4. How many different countries are all the customers from? (*Hint:* consider [DISTINCT](http://www.w3schools.com/sql/sql_distinct.asp).)

SELECT COUNT (DISTINCT Country) FROM Customers;

21

5. What category appears in the most orders?

SELECT *,COUNT(CategoryName) FROM [OrderDetails]
INNER JOIN Categories on Categories.CategoryID=Products.CategoryID
INNER JOIN Products on OrderDetails.ProductID=Products.ProductID
GROUP BY CategoryName
ORDER BY COUNT(CategoryName) DESC;

Dairy Products

6. What was the total cost for each order?

SELECT OrderID, SUM(Quantity*Price) as Total_Price FROM [OrderDetails]
INNER JOIN Categories on Categories.CategoryID=Products.CategoryID
INNER JOIN Products on OrderDetails.ProductID=Products.ProductID
GROUP BY OrderID;

OrderID	Total_Price
10248	566
10249	2329.25
10250	2267.25
10251	839.5
10252	4662.5
10253	1806
10254	781.5
10255	3115.75
10256	648
10257	1400.5
10258	2529.75
10259	126
10260	2183.9
10261	560
10262	782.2
etc.


7. Which employee made the most sales (by total price)?

SELECT Orders.EmployeeID, SUM(Quantity*Price) FROM [OrderDetails]
INNER JOIN Products on OrderDetails.ProductID=Products.ProductID
INNER JOIN Orders on Orders.OrderID=OrderDetails.OrderID
INNER JOIN Employees on Orders.EmployeeID=Orders.EmployeeID
GROUP BY Orders.EmployeeID

EmployeeID = 4 (Margaret Peacock)

8. Which employees have BS degrees? (*Hint:* look at the [LIKE](http://www.w3schools.com/sql/sql_like.asp) operator.)

SELECT LastName, FirstName FROM [Employees]
WHERE Notes
LIKE '%BS%'

LastName	FirstName
Leverling	Janet
Buchanan	Steven

9. Which supplier of three or more products has the highest average product price? (*Hint:* look at the [HAVING](http://www.w3schools.com/sql/sql_having.asp) operator.)

SELECT SupplierName, AVG(Price), COUNT(ProductID) FROM [Products]
INNER JOIN Suppliers on Suppliers.SupplierID=Products.SupplierID
GROUP BY Products.SupplierID
HAVING COUNT(ProductID)>=3
ORDER BY AVG(Price) Desc;

Tokyo Traders





