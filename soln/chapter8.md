# Chapter 8

## Exercise 8-1

Construct a query that counts the number of rows in payment table

```sql
SELECT count(*) FROM payment;
```

Output

```bash
+----------+
| count(*) |
+----------+
|    16049 |
+----------+
```

## Exercise 8-2

Modify your query from Exercise 8-1 to count the number of payments made by each customer. Show the customer ID and the total amount paid by each customer.

```sql
SELECT customer_id, COUNT(*) number_of_payments, SUM(amount) total_amount_paid
FROM payment
GROUP BY customer_id;
```

Output

```bash
+-------------+--------------------+-------------------+
| customer_id | number_of_payments | total_amount_paid |
+-------------+--------------------+-------------------+
|           1 |                 32 |            118.68 |
|           2 |                 27 |            128.73 |
|           3 |                 26 |            135.74 |
|           4 |                 22 |             81.78 |
|           5 |                 38 |            144.62 |
...
|         593 |                 26 |            113.74 |
|         594 |                 27 |            130.73 |
|         595 |                 30 |            117.70 |
|         596 |                 28 |             96.72 |
|         597 |                 25 |             99.75 |
|         598 |                 22 |             83.78 |
|         599 |                 19 |             83.81 |
+-------------+--------------------+-------------------+
```

## Exercise 8-3

Modify your query from 8-2 to include only those customers who have made at least 40 payments.

```sql
SELECT customer_id, COUNT(*) number_of_payments, SUM(amount) total_amount_paid
FROM payment
GROUP BY customer_id
HAVING COUNT(*) >= 40;
```

Output

```bash
+-------------+--------------------+-------------------+
| customer_id | number_of_payments | total_amount_paid |
+-------------+--------------------+-------------------+
|          75 |                 41 |            155.59 |
|         144 |                 42 |            195.58 |
|         148 |                 46 |            216.54 |
|         197 |                 40 |            154.60 |
|         236 |                 42 |            175.58 |
|         469 |                 40 |            177.60 |
|         526 |                 45 |            221.55 |
+-------------+--------------------+-------------------+
```