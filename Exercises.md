```bash
CREATE TABLE products (
	product_id SERIAL PRIMARY KEY, # no need to provide value for this 
	name VARCHAR(100) NOT NULL,
	sku_code CHAR(8) UNIQUE NOT NULL CHECK (char_length(sku_code) = 8),
	price NUMERIC(8, 2) DEFAULT 0 CHECK (price >= 0),
	stock_quantity INT DEFAULT 0 CHECK (stock_quantity >= 0),
	is_available BOOLEAN DEFAULT TRUE,
	category text NOT NULL,
	added_on DATE DEFAULT current_date,
	last_update TIMESTAMP DEFAULT now()
);
```

```bash
INSERT INTO products (name, sku_code, price, stock_quantity, is_available, category)
values 
('Wireless Mouse', 'WM123456', 699.99, 50, TRUE, 'Electronics'),
('Bluetooth Speaker', 'BS234567', 1499.00, 30, TRUE, 'Electronics'),
('Laptop Stand', 'LS345678', 799.50, 20, TRUE, 'Accessories'),
('USB-C Hub', 'UC456789', 1299.99, 15, TRUE, 'Accessories'),
('Notebook', 'NB567890', 99.99, 100, TRUE, 'Stationery'),
('Pen Set', 'PS678901', 199.00, 200, TRUE, 'Stationery'),
('Coffee Mug', 'CM789012', 299.00, 75, TRUE, 'Home & Kitchen'),
('LED Desk Lamp', 'DL890123', 899.00, 40, TRUE, 'Home & Kitchen'),
('Yoga Mat', 'YM901234', 499.00, 25, TRUE, 'Fitness'),
('Water Bottle', 'WB012345', 349.00, 60, TRUE, 'Fitness');
```

```bash
SELECT * FROM products;
```

# Name & Price of all products

```bash
SELECT name, price FROM products;
```

# Show all procducts where categoey is Electronics

```bash
SELECT * FROM products WHERE category = 'Electronics';
```

# Group products by category, show each category once

```bash
SELECT category FROM products GROUP BY category;
```

# show categories that have more than 1 product.

```bash
SELECT category, count(*) FROM products GROUP BY category HAVING count(*) > 1;
```

# show all products sorted by price in asc order

```bash
SELECT * FROM products ORDER BY price;

SELECT * FROM products ORDER BY price DESC;
```

# show only first 3 products from table

```bash
SELECT * FROM products LIMIT 3;
```

# show product name as item_name and price as item_price

```bash
SELECT name as item_name, price as item_price FROM products;
```

# show all unique categories from products

```bash
SELECT DISTINCT category FROM products;
```