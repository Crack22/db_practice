18.10.23
## Task 1 Найти клиентов, сделавших более двух заказов в течение последних трех месяцев.
```
SELECT c.first_name, c.last_name FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
ORDER BY c.customer_id, o.order_date
COUNT (c.cutomer_id) >= 2

```
