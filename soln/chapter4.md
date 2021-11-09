# Chapter 4

## Exercise 4-1

Which of the payment IDs would be return by the following filter conditions?

```sql
customer_id <> 5 and (amount > 8 or date(payment_date) = '2005-08-23')
```

Solution
- 101, 107

## Exercise 4-2

Which of the payment IDs would be returned by the following filter conditions?

```sql
customer_id = 5 and NOT (amount > 6 OR date(payment_date) = '2005-06-19')
```

Solution
- 108, 110, 111, 112, 113, 115, 116, 117, 118, 119, 120

## Exercise 4-3

Construct a query that retrieves all rows from the payments table where thea mount is either 1.98, 7.98 or 9.98

```sql
SELECT amount FROM payment WHERE amount IN (1.98, 7.98, 9.98);
```

## Exercisse 4-4

Construct a query that finds all customers whose last name contains an A in the second position and a W anywhere after the A.

```sql
SELECT first_name, last_name FROM customer WHERE last_name LIKE '_A%W%';
```

Output

```bash
+------------+------------+
| first_name | last_name  |
+------------+------------+
| JILL       | HAWKINS    |
| ERICA      | MATTHEWS   |
| LAURIE     | LAWRENCE   |
| JEANNE     | LAWSON     |
| KAY        | CALDWELL   |
| JOHN       | FARNSWORTH |
| SAMUEL     | MARLOW     |
| LAWRENCE   | LAWTON     |
| LEE        | HAWKS      |
+------------+------------+
```

