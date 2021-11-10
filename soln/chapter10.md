# Chapter 10

## Exercise 10-1

Using the following table definitions and data, write a query that returns each customer name along with their total payments:

Customer:

| customer_id   | name |
| ------------  | ---- |
| 1             | John Smith |
| 2             | Kathy Jones |
| 3             | Greg Oliver |

Payment:

| payment_id | customer_id | amount |
| ---------  | ----------- | ------ |
| 101        | 1           | 8.99   |
| 102        | 3           | 4.99   |
| 103        | 1           | 7.99   |


```sql
SELECT c.name, SUM(p.amount) total_payments
FROM customer c
    LEFT OUTER JOIN payment p
    ON c.customer_id = p.customer_id
GROUP BY c.name;
```

## Exercise 10-2

Reformulate your query from Exercise 10-1 to use the other JOIN

```sql
SELECT c.name, SUM(p.amount) total_payments
FROM payment p
    RIGHT OUTER JOIN customer c
    ON c.customer_id = p.customer_id
GROUP BY c.name;
```

## Exercise 10-3

Devise a query that will generate the set {1, 2, 3, ..., 99, 100}. {Hint: use a cross join with at least two from clause subqueries.}

```sql
WITH ones AS (
    SELECT 9 num UNION ALL
    SELECT 8 num UNION ALL
    SELECT 7 num UNION ALL
    SELECT 6 num UNION ALL
    SELECT 5 num UNION ALL
    SELECT 4 num UNION ALL
    SELECT 3 num UNION ALL
    SELECT 2 num UNION ALL
    SELECT 1 num UNION ALL
    SELECT 0 num
),
tens AS (
    SELECT 0 num UNION ALL
    SELECT 10 num UNION ALL
    SELECT 20 num UNION ALL
    SELECT 30 num UNION ALL
    SELECT 40 num UNION ALL
    SELECT 50 num UNION ALL
    SELECT 60 num UNION ALL
    SELECT 70 num UNION ALL
    SELECT 80 num UNION ALL
    SELECT 90 num
)
SELECT ones.num + tens.num + 1
FROM ones CROSS JOIN tens;
```

Output

```bash
+-------------------------+
| ones.num + tens.num + 1 |
+-------------------------+
|                       1 |
|                       2 |
|                       3 |
|                       4 |
|                       5 |
|                       6 |
|                       7 |
|                       8 |
|                       9 |
|                      10 |
|                      11 |
|                      12 |
|                      13 |
|                      14 |
|                      15 |
|                      16 |
|                      17 |
|                      18 |
|                      19 |
|                      20 |
|                      21 |
|                      22 |
|                      23 |
|                      24 |
|                      25 |
|                      26 |
|                      27 |
|                      28 |
|                      29 |
|                      30 |
|                      31 |
|                      32 |
|                      33 |
|                      34 |
|                      35 |
|                      36 |
|                      37 |
|                      38 |
|                      39 |
|                      40 |
|                      41 |
|                      42 |
|                      43 |
|                      44 |
|                      45 |
|                      46 |
|                      47 |
|                      48 |
|                      49 |
|                      50 |
|                      51 |
|                      52 |
|                      53 |
|                      54 |
|                      55 |
|                      56 |
|                      57 |
|                      58 |
|                      59 |
|                      60 |
|                      61 |
|                      62 |
|                      63 |
|                      64 |
|                      65 |
|                      66 |
|                      67 |
|                      68 |
|                      69 |
|                      70 |
|                      71 |
|                      72 |
|                      73 |
|                      74 |
|                      75 |
|                      76 |
|                      77 |
|                      78 |
|                      79 |
|                      80 |
|                      81 |
|                      82 |
|                      83 |
|                      84 |
|                      85 |
|                      86 |
|                      87 |
|                      88 |
|                      89 |
|                      90 |
|                      91 |
|                      92 |
|                      93 |
|                      94 |
|                      95 |
|                      96 |
|                      97 |
|                      98 |
|                      99 |
|                     100 |
+-------------------------+
```