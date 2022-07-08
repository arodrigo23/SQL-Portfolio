##Problem Statement
Create your own store! Your store should sell one type of things, like clothing or bikes, whatever you want your store to specialize in. You should have a table for all the items in your store, and at least 5 columns for the kind of data you think you'd need to store. You should sell at least 15 items, and use select statements to order your items by price and show at least one statistic about the items

##Solution
```sql
CREATE TABLE store_items (
    id INTEGER PRIMARY KEY,
    item TEXT,
    stock_quantity INTEGER,
    category TEXT,
    price INTEGER);
    
INSERT INTO store_items VALUES
    (1, "T-shirt", 326, "clothing", 10),
    (2, "Crewneck sweatshirt", 500, "clothing", 25),
    (3, "hair brush", 25, "beauty", 5),
    (4, "laptop", 60, "electronics", 1000),
    (5, "water glass", 100, "kitchen", 3),
    (6, "cat toy", 45, "pet", 4),
    (7, "picture frame", 80, "decor", 10),
    (8, "yoga mat", 160, "fitness", 15),
    (9, "slippers", 200, "clothing", 9),
    (10, "power cable", 600, "electronics", 13),
    (11, "flower pot", 150, "garden", 5),
    (12, "toilet paper", 260, "bath", 6),
    (13, "clock", 89, "decor", 18),
    (14, "throw pillow", 265, "decor", 14),
    (15, "fan", 160, "electronics", 20);

/* display all items in order of price */
SELECT * FROM store_items ORDER BY price;
/* display most expensive item in each category */
SELECT item, category, MAX(price) FROM store_items GROUP BY category;
```
