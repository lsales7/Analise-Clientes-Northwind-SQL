USE ImportExport

-- Identifique os clientes com maior volume de compras.

SELECT TOP 20
	C.CompanyName,
	COUNT(DISTINCT OD.ProductID) as Distinct_Products
FROM Customers C
INNER JOIN Orders O ON O.CustomerID = C.CustomerID
INNER JOIN [Order Details] OD ON OD.OrderID = O.OrderID
GROUP BY C.CompanyName
ORDER BY Distinct_Products DESC

-- Descubra os países com mais clientes ativos.

SELECT
	C.Country,
	COUNT(Distinct C.CustomerID) AS Active_Customers
FROM Customers C
INNER JOIN Orders O ON O.CustomerID = C.CustomerID
INNER JOIN [Order Details] OD ON OD.OrderID = O.OrderID
GROUP BY C.Country
ORDER BY 2 DESC

-- Quem são os clientes mais valiosos?

SELECT
	C.CompanyName as Customer,
	COUNT(OD.OrderID) AS Total_Orders,
	SUM(OD.Quantity * OD.UnitPrice) AS Total_Revenue
FROM Customers C
INNER JOIN Orders O ON O.CustomerID = C.CustomerID
INNER JOIN [Order Details] OD ON OD.OrderID = O.OrderID
GROUP BY C.CompanyName
ORDER BY Total_Revenue DESC, Total_Orders DESC
