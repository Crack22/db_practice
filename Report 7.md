10.10.23
## Task 0 Please create 2 Database Views (with similar attributes like the original table) based on simple filtering of gender of persons. Set the corresponding names for the database views: v_persons_female and v_persons_male
```
CREATE VIEW view_1 AS
SELECT name,gender FROM person 
WHERE gender = 'male'
```
```
CREATE VIEW view_2 AS
SELECT name,gender FROM person 
WHERE gender = 'female'
```
![image](https://github.com/necessary22/db_practice/assets/93242683/f9fd464a-f81c-4be9-9eee-5f1f11518773)
![image](https://github.com/necessary22/db_practice/assets/93242683/bb963e82-6ff7-46f5-bd1e-3858198b5870)

## Task 1 Please use 2 Database Views from Exercise #00 and write SQL to get female and male person names in one list. Please set the order by person name. The sample of data is presented below.
```
SELECT v1.name FROM view_1 v1 
UNION ALL
SELECT v2.name FROM view_2 v2
ORDER BY name
```
![image](https://github.com/necessary22/db_practice/assets/93242683/f432a4ea-93b2-4d79-8a20-6fff5551f412)

## Task 2 Please create a Database View (with name v_generated_dates) which should be “store” generated dates from 1st to 31th of January 2022 in DATE type. Don’t forget about order for the generated_date column.
```
CREATE VIEW v_generated_dates AS 
SELECT dates::date FROM generate_series ('2022-01-01','2022-01-31', INTERVAL '1 DAY') AS dates
```
![image](https://github.com/necessary22/db_practice/assets/93242683/e75dfb24-7ec1-4fb8-94bc-e98b0cbf98a4)

## Task 3 Please write a SQL statement which returns missing days for persons’ visits in January of 2022. Use v_generated_dates view for that task and sort the result by missing_date column. The sample of data is presented below.
```
SELECT * FROM v_generated_dates 
WHERE date NOT IN (SELECT visit_date FROM person_visits)
ORDER BY date
```
![image](https://github.com/necessary22/db_practice/assets/93242683/19f8f68a-2e5c-4cc3-8973-7200561954f4)

## Task 4  Please write a SQL statement which satisfies a formula (R - S)∪(S - R) 
```
CREATE VIEW v_symmetric_union AS (
	(SELECT person_id FROM view_r EXCEPT ALL SELECT person_id FROM view_s)
	UNION ALL
	(SELECT person_id FROM view_s EXCEPT ALL SELECT person_id FROM view_r)
);
SELECT * FROM v_symmetric_union
```
![image](https://github.com/necessary22/db_practice/assets/93242683/e64099a3-e1af-48f4-a74b-38379d6c9f32)

## Task 5 Please create a Database View v_price_with_discount that returns a person's orders with person names, pizza names, real price and calculated column discount_price (with applied 10% discount and satisfies formula price - price*0.1).
```
CREATE VIEW v_price_with_discount AS (
	SELECT pizza_name, p.name, m.price,(m.price * 0.9) AS discount_price FROM person_order po
	JOIN person p ON p.id = po.person_id
	JOIN menu m ON m.id = po.menu_id
)
```
![image](https://github.com/necessary22/db_practice/assets/93242683/c46e0215-e396-4c31-a131-7f33f59a0afa)

## Task 6 Please create a Materialized View mv_dmitriy_visits_and_eats (with data included) based on SQL statement that finds the name of pizzeria Dmitriy visited on January 8, 2022 and could eat pizzas for less than 800 rubles 

```
CREATE MATERIALIZED VIEW mv_dmitriy_visits_and_eats AS (
	SELECT p.name FROM pizzeria p
	JOIN person_visits pv ON p.id = pv.pizzeria_id
	JOIN person pr ON pv.person_id = pr.id
	JOIN menu m ON m.pizzeria_id = pv.pizzeria_id 
	WHERE pr.name = 'Dmitriy' AND pv.visit_date = '2022-01-08' AND price <= '800'  
)
```
![image](https://github.com/necessary22/db_practice/assets/93242683/a2e999f9-d330-458a-8b2b-90d7a6e359f6)

