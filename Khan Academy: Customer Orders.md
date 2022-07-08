## Problem Statment
We've created a database for customers and their orders. Not all of the customers have made orders, however. Come up with a query that lists the name and email of every customer followed by the item and price of orders they've made. Use a LEFT OUTER JOIN so that a customer is listed even if they've made no orders, and don't add any ORDER BY.

![image](https://user-images.githubusercontent.com/104938319/178062028-5902901e-0d88-45d7-96ea-c23533d6b45d.png)

customers table:

![image](https://user-images.githubusercontent.com/104938319/178062775-e935955e-9436-4f4f-8e98-38edbe540b0b.png)

orders table:

![image](https://user-images.githubusercontent.com/104938319/178062805-1381390c-7014-4e16-911d-0888e0987885.png)


## Solution
```sql
CREATE TABLE customers (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    email TEXT);
    
INSERT INTO customers (name, email) VALUES ("Doctor Who", "doctorwho@timelords.com");
INSERT INTO customers (name, email) VALUES ("Harry Potter", "harry@potter.com");
INSERT INTO customers (name, email) VALUES ("Captain Awesome", "captain@awesome.com");

CREATE TABLE orders (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    customer_id INTEGER,
    item TEXT,
    price REAL);

INSERT INTO orders (customer_id, item, price)
    VALUES (1, "Sonic Screwdriver", 1000.00);
INSERT INTO orders (customer_id, item, price)
    VALUES (2, "High Quality Broomstick", 40.00);
INSERT INTO orders (customer_id, item, price)
    VALUES (1, "TARDIS", 1000000.00);
    
SELECT customers.name, customers.email, orders.item, orders.price
	FROM customers
	LEFT OUTER JOIN orders
	ON customers.id = orders.customer_id
	;
```

Result:

![image](https://user-images.githubusercontent.com/104938319/178062541-66370c65-4d2c-4c2d-ac61-10fc8940ac9a.png)

Now create another query that will result in one row per each customer, with their name, email, and total amount of money they've spent on orders. Sort the rows according to the total money spent, from the most spent to the least spent. (Tip: You should always GROUP BY on the column that is most likely to be unique in a row

```sql
SELECT customers.name, customers.email, SUM(orders.price) AS orders_total 
		FROM customers
		LEFT OUTER JOIN orders
		ON customers.id = orders.customer_id
		GROUP BY orders.customer_id
		ORDER BY orders_total DESC
	;
```

Result:

![image](https://user-images.githubusercontent.com/104938319/178062631-5fe4ec45-12b6-45e5-a7f5-7e7300e9bad4.png)
