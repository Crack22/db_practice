## Task 1 Write a SQL statement which returns menu’s identifier
```
SELECT id, pizza_name FROM menu
UNION
SELECT id, name FROM person 
ORDER BY id, pizza_name
```
![image](https://github.com/necessary22/db_practice/assets/93242683/5e644eff-038d-4e1d-9f65-858ec27bf54a)

## Task 2  Removing the id column. Then change ordering
```
SELECT pizza_name,'menu' AS source FROM menu
UNION ALL
SELECT name, 'person' AS source FROM person ORDER BY source,pizza_name

```
![image](https://github.com/necessary22/db_practice/assets/93242683/7b37a397-82e9-457c-865f-5d556374e7f8)

## Task 3

## asd
Please write a SQL statement which returns common rows for attributes 
order_date, person_id from person_order table from one side and visit_date, 
person_id from person_visits table from the other side (please see a sample 
below). In other words, let’s find identifiers of persons, who visited and 
ordered some pizza on the same day. Actually, please add ordering by 
action_date in ascending mode and then by person_id in descending mode.
4. Please write a SQL statement which returns a difference (minus) of person_id 
column values with saving duplicates between person_order table and 
person_visits table for order_date and visit_date are for 7th of January of 2022
