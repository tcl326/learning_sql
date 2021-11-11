# Chapter 13

## Exercise 13-1

Generate an alter table statement for the rental table so that an error will be raised if a row having a value found in rental.costumer_id column is deleted from the customer table.

```sql
ALTER TABLE  rental
ADD CONSTRAINT fk_customer_id FOREIGN KEY (customer_id)
REFERENCES customer (customer_id) ON DELETE RESTRICT;
```

## Exercise 13-2

Generate a multicolumn index on the payment table that could be used by both of the following queries:

```sql
SELECT customer_id, payment_date, amount
FROM payment
WHERE payment_date > cast('2019-12-31 23:59:59' as datetime);

SELECT customer_id, payment_date, amount
FROM payment
WHERE payment_date > cast('2019-12-31 23:59:50' as datetime)
    AND amount < 5;
```

Answer

```sql
ALTER TABLE payment
ADD INDEX idx_datetime_amount (payment_date, amount);
```

Output from EXPLAIN query

```bash
mysql> EXPLAIN
    -> SELECT customer_id, payment_date, amount
    -> FROM payment
    -> WHERE payment_date > cast('2019-12-31 23:59:59' as datetime);
+----+-------------+---------+------------+-------+---------------------+---------------------+---------+------+------+----------+-----------------------+
| id | select_type | table   | partitions | type  | possible_keys       | key                 | key_len | ref  | rows | filtered | Extra                 |
+----+-------------+---------+------------+-------+---------------------+---------------------+---------+------+------+----------+-----------------------+
|  1 | SIMPLE      | payment | NULL       | range | idx_datetime_amount | idx_datetime_amount | 5       | NULL |    1 |   100.00 | Using index condition |
+----+-------------+---------+------------+-------+---------------------+---------------------+---------+------+------+----------+-----------------------+
```

```bash
mysql> EXPLAIN
    -> SELECT customer_id, payment_date, amount
    -> FROM payment
    -> WHERE payment_date > cast('2019-12-31 23:59:50' as datetime)
    ->     AND amount < 5;
+----+-------------+---------+------------+-------+---------------------+---------------------+---------+------+------+----------+-----------------------+
| id | select_type | table   | partitions | type  | possible_keys       | key                 | key_len | ref  | rows | filtered | Extra                 |
+----+-------------+---------+------------+-------+---------------------+---------------------+---------+------+------+----------+-----------------------+
|  1 | SIMPLE      | payment | NULL       | range | idx_datetime_amount | idx_datetime_amount | 5       | NULL |    1 |    33.33 | Using index condition |
+----+-------------+---------+------------+-------+---------------------+---------------------+---------+------+------+----------+-----------------------+
```