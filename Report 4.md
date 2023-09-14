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
