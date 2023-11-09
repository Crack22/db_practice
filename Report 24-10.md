24.10.23
## Task 1 Let’s make a simple aggregation, please write a SQL statement that returns person identifiers and corresponding number of visits in any pizzerias and sorting by count of visits in descending mode and sorting in person_id in ascending mode. Please take a look at the sample of data below.
```sql 
SELECT p.id, (SELECT COUNT(pv.id) FROM person_visits pv 
			  WHERE pv.person_id = p.id) AS "count_of_visits" FROM person p
ORDER BY count_of_visits DESC, p.id ASC
```
![image](https://github.com/necessary22/db_practice/assets/93242683/124f820f-503f-495e-a0ed-20af4cfecfad)

## Task 2 Please change a SQL statement from Exercise 00 and return a person name (not identifier). Additional clause is we need to see only top-4 persons with maximal visits in any pizzerias and sorted by a person name. Please take a look at the example of output data below.

```sql
WITH tmp AS (
	SELECT p.name, (SELECT COUNT(pv.id) FROM person_visits pv WHERE pv.person_id = p.id) AS "count_of_visits" FROM person p
	ORDER BY count_of_visits DESC LIMIT 4
)

SELECT name FROM tmp ORDER BY name
```
![image](https://github.com/necessary22/db_practice/assets/93242683/d3802075-3818-4428-9644-3d54572d8e4c)

## Task 3 
