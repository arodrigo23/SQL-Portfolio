### Customer and Order Analytics
Here I explore sales data from a database to extract meaningful insights. The database contains information about customer orders and product sales in different months. 

Initial investigation of the data showed that while most order ID numbers are 6-digit integers, some records contain nulls or a generic 'Order ID' string. To exclude these invalid records from the queries below, a filtering condition was added to only include records with valid orderID's: WHERE LENGTH(orderID) = 6. This successfully excludes null values and the 8-character 'Order ID' strings.

```
-- Which locations in New York received at least 3 orders in January, and how many orders did they each receive?
SELECT DISTINCT location, COUNT(orderID) AS num_of_orders
FROM BIT_DB.JanSales
WHERE LENGTH(orderID) = 6 AND location like '%NY%'
GROUP BY location
HAVING COUNT(orderID) >= 3;

-- How many of each type of headphone were sold in February?
SELECT DISTINCT Product, SUM(Quantity)
FROM BIT_DB.FebSales
WHERE LENGTH(orderID) = 6 AND Product LIKE '%headphone%' OR '%head phone%'
GROUP BY Product;

-- What was the average amount spent per account in February?
SELECT SUM(S.Quantity * S.Price) / COUNT(C.acctnum) AS avg_amnt_spent
FROM BIT_DB.FebSales S
JOIN BIT_DB.customers C
ON S.orderID = C.order_ID
WHERE LENGTH(S.orderID) = 6; 

-- What was the average quantity of products purchased per account in February?
SELECT SUM(S.Quantity) / COUNT(C.acctnum)
FROM BIT_DB.FebSales S
JOIN BIT_DB.customers C
ON S.orderID = C.order_ID
WHERE LENGTH(S.orderID) = 6; 

-- Which product brought in the most revenue in January and how much revenue did it bring in total?
SELECT Product, SUM(Quantity * Price)
FROM BIT_DB.JanSales
WHERE LENGTH(orderID) = 6
GROUP BY Product
ORDER BY 2 DESC
LIMIT 1; 

-- List all the products sold in Los Angeles in February, and include how many of each were sold
SELECT Product, SUM(Quantity) AS total_qty_sold
FROM FebSales 
WHERE LENGTH(orderID) = 6 AND location LIKE '%los angeles%'
GROUP BY Product;

-- How many customers ordered more than 2 products at a time in February, and what was the average amount spent for those customers?
SELECT 
    COUNT(DISTINCT c.acctnum), 
    AVG(s.Quantity * s.Price)
FROM BIT_DB.FebSales s
JOIN BIT_DB.customers c
ON s.orderID = c.order_id
WHERE s.Quantity > 2
AND LENGTH(s.orderID) = 6;

-- Which products were sold in February at 548 Lincoln St, Seattle, WA 98101, how many of each were sold, and what was the total revenue?
SELECT Product, SUM(Quantity), SUM(Quantity) * Price AS total_revenue
FROM BIT_DB.FebSales
WHERE LENGTH(orderID) = 6 AND location LIKE '548 Lincoln St, Seattle, WA 98101'
GROUP BY Product;

-- How many orders were placed in January?
SELECT COUNT(orderID) 
FROM BIT_DB.JanSales
WHERE LENGTH(orderID) = 6;

-- How many of those orders were for an iPhone?
SELECT COUNT(orderID)
FROM BIT_DB.JanSales
WHERE Product LIKE '%iphone%';

--Select the customer account numbers for all the orders that were placed in February
SELECT DISTINCT acctnum
FROM BIT_DB.FebSales S
JOIN BIT_DB.customers C
ON C.order_ID = S.orderID
WHERE LENGTH(S.orderID) = 6;

-- Which product was the cheapest one sold in January, and what was the price?
SELECT Product, MIN(price) AS Price
FROM BIT_DB.JanSales
WHERE LENGTH(orderID) = 6;

-- What is the total revenue for each product sold in January? (Revenue can be calculated using the number of products sold and the price of the products)
SELECT 
    Product,
    SUM(Quantity) * price AS total_revenue
FROM BIT_DB.JanSales 
WHERE LENGTH(orderID) = 6
GROUP BY Product;
```
