## Problem Statment
We've created a database for customers and their orders. Not all of the customers have made orders, however. Come up with a query that lists the name and email of every customer followed by the item and price of orders they've made. Use a LEFT OUTER JOIN so that a customer is listed even if they've made no orders, and don't add any ORDER BY

Database Schema
customers | 3 rows
----------|--------
id (PK)   | INTEGER
name      | TEXT
email     | TEXT
