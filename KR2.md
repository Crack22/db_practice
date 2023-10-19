18.10.23
## Task 1 Найти клиентов, сделавших более двух заказов в течение последних трех месяцев.
```
SELECT c.first_name,c.customer_id FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id,o.order_date
HAVING COUNT (c.customer_id) > 2 AND o.order_date BETWEEN '2023-07-18' and '2023-10-18'


```
![image](https://github.com/necessary22/db_practice/assets/93242683/fb18cc17-1c46-4437-a649-e8586920ef87)


## Task 2 Найти средний размер заказа для каждой категории товаров, исключая категории, в которых есть товары с ценой менее $50.
```

```

## Task 3  Получить список клиентов, у которых суммарная стоимость всех заказов выше средней стоимости заказа в системе.
```
WITH sumas AS (SELECT p.product_id,SUM(p.price) AS suma FROM products p
					 GROUP BY p.product_id, p.price
),
avg_suma AS (SELECT AVG(p.price) AS sms  FROM products p
)

SELECT c.first_name, c.customer_id from customers c 
JOIN orders o ON c.customer_id = o.customer_id
JOIN sumas s ON s.product_id = o.product_id
WHERE s.suma > (SELECT avgs.sms FROM avg_suma avgs)
GROUP BY c.first_name, c.customer_id
ORDER BY c.customer_id
```
![image](https://github.com/necessary22/db_practice/assets/93242683/122c99aa-8d3a-4c0e-84c9-94e91791a8cc)


## Task 9  Найти категорию товаров с самой высокой средней ценой, и категорию с самой низкой средней ценой.

```
SELECT category, AVG(price) AS avg_price FROM products
GROUP BY category
ORDER BY avg_price ASC;

```
![image](https://github.com/necessary22/db_practice/assets/93242683/05f1a389-9e18-4c86-8240-9aa3ee012bad)


# Database
```
-- Создание таблиц
CREATE TABLE Customers (
    customer_id serial PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    address TEXT
);

CREATE TABLE Products (
    product_id serial PRIMARY KEY,
    product_name VARCHAR(100),
    price DECIMAL(10, 2),
    category VARCHAR(50)
);

CREATE TABLE Orders (
    order_id serial PRIMARY KEY,
    customer_id INT,
    product_id INT,
    quantity INT,
    order_date DATE
);

-- Заполнение таблиц данными
-- Добавление 50 клиентов
INSERT INTO Customers (first_name, last_name, email, address)
SELECT 
    'First Name ' || generate_series(1, 50),
    'Last Name ' || generate_series(1, 50),
    'email' || generate_series(1, 50) || '@example.com',
    'Address ' || generate_series(1, 50)
FROM generate_series(1, 50);

-- Добавление 250 товаров
INSERT INTO Products (product_name, price, category)
SELECT 
    'Product ' || generate_series(1, 250),
    CAST(random() * 1000 AS DECIMAL(10, 2)),
    CASE
        WHEN random() < 0.3 THEN 'Electronics'
        WHEN random() < 0.6 THEN 'Clothing'
        ELSE 'Other'
    END
FROM generate_series(1, 250);

-- Добавление 8000 заказов
INSERT INTO Orders (customer_id, product_id, quantity, order_date)
SELECT 
    floor(random() * 50) + 1,
    floor(random() * 250) + 1,
    floor(random() * 5) + 1,
    current_date - (random() * 365 || ' days')::interval
FROM generate_series(1, 8000);

```
