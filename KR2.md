18.10.23
## Task 1 Найти клиентов, сделавших более двух заказов в течение последних трех месяцев.
```
SELECT c.first_name, c.last_name FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
ORDER BY c.customer_id, o.order_date
COUNT (c.cutomer_id) >= 2

```
![image](https://github.com/necessary22/db_practice/assets/93242683/c49e8c26-bd48-462b-a36e-4290dafc00ae)

## Task 2 Найти средний размер заказа для каждой категории товаров, исключая категории, в которых есть товары с ценой менее $50.
```

```

## Task 3  Получить список клиентов, у которых суммарная стоимость всех заказов выше средней стоимости заказа в системе.
```

```

## Task 4 Найти клиентов, которые сделали заказы на сумму более $1000 и при этом не делали заказы в категории "Электроника"
```

```

## Task 5 Создать VIEW, который показывает среднюю стоимость заказа для каждого клиента, а также отклонение этой стоимости от средней стоимости заказа в системе.
```

```

## Task 6 Найти клиента, у которого самый долгий период между двумя последними заказами
```

```

## Task 7 Получить список клиентов, у которых суммарная стоимость всех заказов увеличилась в последние два месяца.
```

```

## Task 8 Обновить столбец price в таблице Products таким образом, чтобы он отражал новую цену товара с учетом скидки 10% на все товары в категории "Одежда".
```

```

## Task 9  Найти категорию товаров с самой высокой средней ценой, и категорию с самой низкой средней ценой.
```

```

# Task 10 Удалить все заказы, в которых количество товаров превышает среднее количество товаров в заказах.
```

```

## Database
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
