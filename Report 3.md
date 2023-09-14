## Task 1. Insert 10 recording to all tables your’s database.

```
INSERT INTO menu (id, pizzeria_id, pizza_name, price)
VALUES (19, 1, 'Margherita', 900),
(20, 1, 'Margherita', 800),
(21, 3, 'Quattro Stagioni', 700),
(22, 4, 'Carbonara', 1000),
(23, 6, 'Crudo', 950),
(24, 2, 'Napoletana', 850),
(25, 4, 'Pugliese', 650),
(26, 1, 'Montanara', 750),
(27, 3, 'Emiliana', 800),
(28, 5, 'Romana', 1100);
```
![image](https://github.com/Crack22/db_practice/assets/93242683/355b3d07-5c49-4eb3-b0d0-95e310665ead)

```
INSERT INTO person (id, name, age, gender, address)
VALUES (10, 'Katya', 17, 'female', 'Moscow'),
(11, 'Katya', 17, 'female', 'Moscow'),
(12, 'Artem', 18, 'male', 'Kazan'),
(13, 'Matvey', 16, 'male', 'Moscow'),
(14, 'Bogdan', 19, 'male', 'Moscow'),
(15, 'Vova', 18, 'male', 'kazan'),
(16, 'Vika', 20, 'female', 'Samara'),
(17, 'Sonya', 17, 'female', 'Moscow'),
(18, 'Petr', 16, 'male', 'Samara'),
(19, 'Ruslan', 18, 'male', 'Kazan');
```
![image](https://github.com/Crack22/db_practice/assets/93242683/794374b8-b976-4ea2-a15b-f0c4feed6da5)

```
INSERT INTO person_order (id, person_id, menu_id, order_date)
VALUES (21, 1, 4, '2022-03-01'),
(22, 1, 4, '2022-04-02'),
(23, 2, 14, '2022-05-03'),
(24, 3, 15, '2022-06-04'),
(25, 4, 6, '2022-07-05'),
(26, 5, 2, '2022-08-06'),
(27, 6, 16, '2022-09-07'),
(28, 7, 8, '2022-10-08'),
(29, 8, 5, '2022-11-09'),
(30, 9, 2, '2022-12-10');
```
![image](https://github.com/Crack22/db_practice/assets/93242683/7b22ecf7-fb6c-4b5f-96f1-cafa2ff2d625)

```
INSERT INTO person_visits (id, person_id, pizzeria_id, visit_date)
VALUES (20, 1, 4, '2022-04-02'),
(21, 1, 6, '2021-05-03'),
(22, 2, 1, '2022-06-04'),
(23, 3, 5, '2021-07-05'),
(24, 4, 2, '2023-08-06'),
(25, 5, 4, '2021-09-07'),
(26, 6, 3, '2019-10-08'),
(27, 1, 5, '2022-11-09'),
(28, 2, 2, '2021-12-10'),
(29, 3, 1, '2023-12-10');
```
![image](https://github.com/Crack22/db_practice/assets/93242683/ee1825fe-412a-481e-a5c3-0c5511a9639a)

```
INSERT INTO pizzeria (id, name, rating)
VALUES (7, 'Firehouse Pizza', '3.9'),
(8, 'Firehouse Pizza', '4.9'),
(9, 'Firehouse Pizza', '4.2'),
(10, 'Firehouse Pizza', '4.4'),
(11, 'Firehouse Pizza', '4.6'),
(12, 'Firehouse Pizza', '4.1'),
(13, 'Firehouse Pizza', '4.5'),
(14, 'Firehouse Pizza', '3.7'),
(15, 'Firehouse Pizza', '4.8'),
(16, 'Firehouse Pizza', '4.4');
```
![image](https://github.com/Crack22/db_practice/assets/93242683/40fc90e9-910b-4b72-8597-15b065f00e8f)

## Task 2 Make a select statement which returns all person's names and person's ages from the city
```
SELECT (name, age)
FROM person WHERE address = 'Samara'
```
![image](https://github.com/Crack22/db_practice/assets/93242683/b292ab4f-9fea-485f-a5bc-a5af0de1f429)

## Task 3 Make a select statement which returns names , ages for all women from the city

```
SELECT ("name", "age", "address")
FROM "person" WHERE "gender" = 'female' and "address" = 'Kazan'
```
![image](https://github.com/necessary22/db_practice/assets/93242683/940eb501-4e95-4aa5-a7dc-56845f765de2)

## Task 4 Make 2 syntax different select statements which return a list of pizzerias with rating between 3.5 and 5 points

```
SELECT "name", "rating" FROM "pizzeria" WHERE "rating" BETWEEN 3.5 AND 5 OR "rating" > 3.5 
```
![image](https://github.com/necessary22/db_practice/assets/93242683/274f21ef-ca44-4d77-a3b8-edff8b4dd1ff)

## Task 5 Make a select statement which returns the person's identifiers

```
SELECT DISTINCT person_id FROM person_visits
WHERE visit_date BETWEEN '2022-01-02' AND '2022-01-09'
```
![image](https://github.com/necessary22/db_practice/assets/93242683/76f97650-f86d-4736-bbc7-acd41fba982c)

## Task 6 Make a select statement which returns person's names

```
SELECT name FROM person WHERE id IN 
(SELECT id FROM person_visits WHERE visit_date = '2022-01-02' OR visit_date = '2022-01-03' OR visit_date = '2022-01-04')
```
![image](https://github.com/necessary22/db_practice/assets/93242683/b301e295-285d-488d-9a69-9cd9db6422b0)



## Task 7  Make a select to person table that returning (true or false) if person_name
```
SELECT EXISTS (SELECT * FROM "person" WHERE "name" = 'Anna') AS results
```
![image](https://github.com/necessary22/db_practice/assets/93242683/edc55bde-fb1a-4317-8cfd-9f199798ff81)



