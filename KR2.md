18.10.23
## Task 1 Найти клиентов, сделавших более двух заказов в течение последних трех месяцев.
```
SELECT c.first_name,c.customer_id FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id,o.order_date
HAVING COUNT (c.customer_id) > 2 AND o.order_date BETWEEN '2023-07-18' and '2023-10-18'


```
![image](https://github.com/necessary22/db_practice/assets/93242683/fb18cc17-1c46-4437-a649-e8586920ef87)

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

## Task 4
```
SELECT c.first_name, c.last_name, c.email FROM customers c
JOIN orders o ON o.customer_id = c.customer_id
JOIN products p ON p.product_id = o.product_id
WHERE p.price > 1000 AND p.category != 'Electronics';
```
![image](https://github.com/necessary22/db_practice/assets/93242683/f5ef05b4-de6f-488a-a6db-430cf1d4d623)

## Task 6
```
WITH customer_max_min AS (
	SELECT o.customer_id, MAX(o.order_date) AS max_date, MIN(o.order_date) AS min_date FROM orders o
	GROUP BY o.customer_id
), 
range_max_min AS(
	SELECT cusmm.customer_id, (cusmm.max_date - cusmm.min_date) AS range FROM customer_max_min cusmm
),

max_p  AS (
	SELECT cus.first_name, cus.last_name,cus.customer_id, MAX(o.order_date), MIN(o.order_date), MAX(rgmm.range) AS all_mm FROM orders o
	JOIN range_max_min rgmm ON rgmm.customer_id = o.customer_id
	JOIN customers cus ON cus.customer_id = o.customer_id
	GROUP BY cus.first_name, cus.last_name, cus.customer_id
)

SELECT first_name, last_name, customer_id FROM max_p WHERE all_mm = (SELECT MAX(all_mm) FROM max_p);

```
![image](https://github.com/necessary22/db_practice/assets/93242683/3109b5e4-9138-4174-b8c5-7111f10064cf)

## Task 8 
```
SELECT category, p.price, (p.price * 0.9) AS dis_price FROM products p
WHERE category = 'Clothing'
```
![image](https://github.com/necessary22/db_practice/assets/93242683/4e7c19b9-99ce-48fb-8968-404135dc2fd8)

## Task 9  Найти категорию товаров с самой высокой средней ценой, и категорию с самой низкой средней ценой.

```
SELECT category, AVG(price) AS avg_price FROM products
GROUP BY category
ORDER BY avg_price;

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
