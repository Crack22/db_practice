## Task 1 Please write a SQL statement which returns a list of pizzerias names with corresponding rating value which have not been visited by persons.
```
SELECT DISTINCT pizzeria.name, rating FROM pizzeria
CROSS JOIN menu
WHERE pizzeria.id NOT IN (SELECT pizzeria_id FROM person_visits)
```
![image](https://github.com/necessary22/db_practice/assets/93242683/2fecc88d-04e7-4642-97ff-5ca9edca1647)

## Task 2 Please write a SQL statement which returns the missing days from 1st to 10th of January 2022 (including all days) for visits of persons with identifiers 1 or 2 (it means days missed by both). Please order by visiting days in ascending mode. The sample of data with column name is presented below.

```
SELECT  missing_date::date FROM generate_series ('2022-01-01','2022-01-10', INTERVAL '1 DAY') AS missing_date 
FULL JOIN (
SELECT * FROM person_visits WHERE person_id = 1 OR person_id = 2 AND visit_date BETWEEN '2022-01-01' AND '2022-01-10')  as tab
ON missing_date = visit_date WHERE tab.person_id IS NULL
ORDER BY missing_date
```
![image](https://github.com/necessary22/db_practice/assets/93242683/0043fa07-b008-4cf2-a3e6-52ce3d6fa313)
