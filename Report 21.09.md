## Task 1 Please write a SQL statement which returns all possible combinations between person and pizzeria tables and please set ordering by person identifier
```
SELECT * FROM person
CROSS JOIN pizzeria
ORDER BY person,pizzeria
```
![image](https://github.com/necessary22/db_practice/assets/93242683/4744d68d-8ad5-4059-962f-4a4969e48809)

## Task 2  Return person names instead of person identifiers and change ordering by action_date in ascending mode and then by person_name in descending mode
```
SELECT name FROM person 
CROSS JOIN person_visits 
ORDER BY person_visits,name DESC
```
![image](https://github.com/necessary22/db_practice/assets/93242683/c3599ef6-06f8-4df4-bb6c-8992e53c3543)

## Task 3 Please write a SQL statement which returns the date of order from the person_order table and corresponding person name which made an order from the person table. Add a sort by both columns in ascending mode.

```
SELECT DISTINCT order_date, (name,age) AS person_inf 
FROM person_order
CROSS JOIN person 
ORDER BY order_date, person_inf ASC;
```
![image](https://github.com/necessary22/db_practice/assets/93242683/58d90a21-b37f-4b06-ace2-d70ff8ee421f)

## Task 4 Please rewrite a SQL statement from exercise #07 by using NATURAL JOIN construction.

```
SELECT DISTINCT order_date, (name,age) AS person_inf 
FROM person_order
NATURAL JOIN person 
ORDER BY order_date, person_inf ASC;
```
![image](https://github.com/necessary22/db_practice/assets/93242683/66e6c6e6-cbf5-4304-9b98-b0fdd1e124c7)

## Task 5 Please write 2 SQL statements which return a list of pizzerias names which have not been visited by persons by using IN for 1st one and EXISTS for the 2nd one.

```
SELECT pizzeria.name FROM pizzeria
WHERE pizzeria.id NOT IN (SELECT pizzeria_id FROM person_visits)
```
![image](https://github.com/necessary22/db_practice/assets/93242683/180458b2-f6ce-41d7-81d1-ec45edb774e8)

## Task 6 Please write a SQL statement which returns a list of the person names which made an order for pizza in the corresponding pizzeria. The sample result (with named columns) is provided below and yes ... please make ordering by 3 columns (person_name, pizza_name, pizzeria_name) in ascending mode.

```
SELECT person.name,menu.pizza_name, pizzeria.name FROM person_order JOIN person ON person_order.person_id = person_id
LEFT JOIN menu ON menu.id = person_order.menu_id
LEFT JOIN pizzeria ON pizzeria.id = menu.pizzeria_id
```
![image](https://github.com/necessary22/db_practice/assets/93242683/f0c3a4a6-3b33-4211-988a-310a13a05cf4)

