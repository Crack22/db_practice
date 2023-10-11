10.10.23
## Task 1 Please create 2 Database Views (with similar attributes like the original table) based on simple filtering of gender of persons. Set the corresponding names for the database views: v_persons_female and v_persons_male
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

## Task 2 Please use 2 Database Views from Exercise #00 and write SQL to get female and male person names in one list. Please set the order by person name. The sample of data is presented below.
```
SELECT v1.name FROM view_1 v1 
UNION ALL
SELECT v2.name FROM view_2 v2
ORDER BY name
```
![image](https://github.com/necessary22/db_practice/assets/93242683/f432a4ea-93b2-4d79-8a20-6fff5551f412)
