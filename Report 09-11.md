## Task 0
```sql
CREATE TABLE person_discounts
	(id INT PRIMARY KEY NOT NULL,
	 person_id INT, 
	 pizzeria_id INT,
	 constraint fk_person_discounts_person_id foreign key (person_id) references person(id),
	 constraint fk_person_discounts_pizzeria_id foreign key (pizzeria_id) references pizzeria(id)
	);
```
![image](https://github.com/necessary22/db_practice/assets/93242683/508c6839-f66f-4302-a4e6-0370a5956395)

## Task 1
```sql
INSERT INTO person_discounts (person_id, pizzeria_id, discount)
SELECT person_id, pizzeria_id,
    case
   	WHEN amount_of_orders = 1 THEN 10.5
   	WHEN amount_of_orders = 2 THEN 22
   	ELSE 30
    END AS discount
FROM
	(SELECT person_id, pizzeria_id, COUNT(*) AS amount_of_orders
	 FROM person_discounts
     GROUP BY person_id, pizzeria_id
    )AS order_counts;
```
