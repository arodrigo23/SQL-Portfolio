## Customer Sales Analysis in SQLite
In this project, I connect SQLite to a database of customer sales data containing the following tables: 
- Customers
- JanSales
- FebSales
- MarSales
- MaySales

The following SQL statements answer questions about the sales data:

```sql
--How many orders were placed in January?
SELECT COUNT(*) AS numOfOrders
FROM BIT_DB.JanSales;

--How many of those orders were for an iPhone?
SELECT COUNT(*) AS iPhoneOrders
FROM BIT_DB.JanSales
WHERE Product LIKE '%iPhone%';

--Select the customer account numbers for all the orders that were placed in February
SELECT acctnum
FROM BIT_DB.customers Customers
INNER JOIN BIT_DB.FebSales FebSales
ON Customers.order_id = FebSales.orderID;

--Which product was the cheapest one sold in January, and what was the price?
SELECT Product, price
FROM BIT_DB.JanSales
ORDER BY price
LIMIT 1;

--What is the total revenue for each product sold in January? 
SELECT Product, SUM(price)*COUNT(Product) AS totalRevenue
FROM BIT_DB.JanSales
GROUP BY Product;

-- Which products were sold in Fenruary at 548 Lincoln St, Seattle, WA 98101, how many of each were sold, and what was the total revenue?
SELECT Product, SUM(Quantity) as totalQuantity, SUM(Quantity)*price as totalRevenue
FROM BIT_DB.FebSales
WHERE location LIKE '%548 Lincoln%Seattle%WA%'
GROUP BY Product;

--How many customers ordered more than 2 products at a time in February, and what was the average amount spent for those customers?
SELECT COUNT(DISTINCT Customers.acctnum), AVG(Quantity*price)
FROM BIT_DB.customers Customers
JOIN BIT_DB.FebSales FebSales
ON Customers.order_id = FebSales.orderID
WHERE FebSales.Quantity > 2;

--List all the products sold in Los Angeles in February, and include how many of each were sold
SELECT Product, SUM(Quantity) AS Quantity
FROM BIT_DB.FebSales
WHERE location LIKE '%Los Angeles%'
GROUP BY Product;

--Which locations in New York received at least 3 orders in January, and how many orders did they each receive?
SELECT location, COUNT(orderID) as orders
FROM BIT_DB.JanSales
WHERE location LIKE '%New York%'
GROUP BY location
HAVING COUNT(orderID) > 2;

--How many of each type of headphone were sold in February?
SELECT Product, SUM(Quantity) as totalSold
FROM BIT_DB.FebSales
WHERE Product LIKE '%headphone%'
GROUP BY Product;

--What was the average amount spent per account in February?
SELECT SUM(S.Quantity * S.price) / COUNT(C.acctnum) AS avgSpentPerAcct
FROM BIT_DB.FebSales S
JOIN BIT_DB.customers C
ON S.orderID = C.order_id;

--What was the average quantity of products purchased per account in February?
SELECT SUM(S.Quantity) / COUNT(C.acctnum)
FROM BIT_DB.FebSales S
JOIN BIT_DB.customers C
ON S.orderID = C.order_id;

--Which product brought in the most revenue in January and how much revenue did it bring in total?
SELECT Product, SUM(Quantity * price)
FROM BIT_DB.JanSales
GROUP BY Product
ORDER BY 2 DESC
LIMIT 1;
```
