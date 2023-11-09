## Task 0
```sql
SELECT person_id, COUNT(person_id) FROM person_visits
GROUP BY person_id
ORDER BY count DESC, person_id ASC
```
![image](https://github.com/necessary22/db_practice/assets/93242683/1bf89425-1d47-4bb2-b8a7-fb841f93cfb9)

## Task 1
```sql  
SELECT p.name, COUNT(person_id) FROM person_visits
JOIN person p ON p.id = person_visits.person_id
GROUP BY name
ORDER BY count DESC, name ASC
```
![image](https://github.com/necessary22/db_practice/assets/93242683/9baf9e48-8679-4cf7-83ab-6c5cc06743b3)

## Task 2
```sql
SELECT pi.name, COUNT(menu_id), 'order' AS action_type FROM person_order po
JOIN menu m ON m.id = po.menu_id
JOIN pizzeria pi ON pi.id = m.pizzeria_id
GROUP BY pi.name
ORDER BY count DESC
LIMIT 3
```
![image](https://github.com/necessary22/db_practice/assets/93242683/9250e507-630a-454b-a91b-a89006031513)

## Task 3
```sql
(SELECT pi.name, COUNT(pizzeria_id), 'order' AS action_type FROM person_visits pv
JOIN pizzeria pi ON pi.id = pv.pizzeria_id
GROUP BY pi.name
ORDER BY count DESC
LIMIT 3)
  union
(SELECT pi.name, COUNT(menu_id), 'order' AS action_type FROM person_order po
JOIN menu m ON m.id = po.menu_id
JOIN pizzeria pi ON pi.id = m.pizzeria_id
GROUP BY pi.name
ORDER BY count DESC
LIMIT 3)
ORDER BY action_type
```
![image](https://github.com/necessary22/db_practice/assets/93242683/537a07b2-9144-433b-a274-09f96090e818)

## Task 4 
```sql
SELECT p.name, COUNT(pv.id) AS count_of_visits FROM person p
JOIN person_visits pv ON pv.person_id = p.id
GROUP BY 1
HAVING COUNT(pv.id) > 3
```
![image](https://github.com/necessary22/db_practice/assets/93242683/7fd846a5-24f6-438c-bf1d-ee725339122d)

## Task 5
```sql
SELECT DISTINCT p.name FROM person p
LEFT JOIN person_order pd ON pd.person_id = p.id
ORDER BY 1
```
![image](https://github.com/necessary22/db_practice/assets/93242683/6d0fda03-8af3-43eb-a969-1541ee858a0d)

## Task 6 
```sql

SELECT COUNT(po.order_date) AS Count_of_orders FROM person_order po
   JOIN menu m ON m.id = po.id;

SELECT round(AVG(m.price), 2) as average_price,
   round(MAX(m.price), 2) as max_price,
   round(MIN(m.price), 2) as min_price
   FROM menu m
GROUP BY m.pizzeria_id;
```
![image](https://github.com/necessary22/db_practice/assets/93242683/e578ee40-605c-4f36-bd81-58d95f80cc1a)

## Task 7 
```sql
SELECT round(AVG(pz.rating ), 4) AS global_rating FROM pizzeria pz
```
![image](https://github.com/necessary22/db_practice/assets/93242683/ec26e2e6-3b43-46bb-af1f-76618db50a27)

## Task 8
```sql
SELECT address, pi.name, COUNT(po.order_date) FROM person p
JOIN pizzeria pi ON pi.id = p.id
JOIN person_order po ON po.person_id = p.id 
GROUP BY p.address, pi.name
ORDER BY p.address;
```
![image](https://github.com/necessary22/db_practice/assets/93242683/e9f62ebe-1431-4b22-96cb-159f1f7265fa)

## Task 9
```sql
WITH formula_average AS 
	(SELECT p.address, (MAX(p.age) - (MIN(p.age) / MAX(p.age))) AS formula, ROUND(AVG(p.age),2)
	AS average FROM person p
	GROUP BY 1
	)
SELECT fa.address, fa.formula, fa.average, (fa.formula>fa.average) AS comparison FROM formula_average fa
```
![image](https://github.com/necessary22/db_practice/assets/93242683/3ca4c793-2952-4db6-82a4-3af5e449f60e)
