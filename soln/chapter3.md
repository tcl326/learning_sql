# Chapter 3

## Exercise 3-1

Retrieve the actor ID, first name, and last name for all actors. Sort by last name and then by first name

```sql
SELECT actor_id, first_name, last_name FROM actor ORDER BY last_name, first_name;
```

Output 

```bash
+----------+-------------+--------------+
| actor_id | first_name  | last_name    |
+----------+-------------+--------------+
|       58 | CHRISTIAN   | AKROYD       |
|      182 | DEBBIE      | AKROYD       |
|       92 | KIRSTEN     | AKROYD       |
|      118 | CUBA        | ALLEN        |
|      145 | KIM         | ALLEN        |
|      194 | MERYL       | ALLEN        |
|       76 | ANGELINA    | ASTAIRE      |
...
|      147 | FAY         | WINSLET      |
|       68 | RIP         | WINSLET      |
|      144 | ANGELA      | WITHERSPOON  |
|      156 | FAY         | WOOD         |
|       13 | UMA         | WOOD         |
|       63 | CAMERON     | WRAY         |
|      111 | CAMERON     | ZELLWEGER    |
|      186 | JULIA       | ZELLWEGER    |
|       85 | MINNIE      | ZELLWEGER    |
+----------+-------------+--------------+
```

## Exervise 3-2

Retrieve the actor ID, first name, and last name for all actors whose last name equals 'WILLIAMS' or 'DAVIS'.

```sql
SELECT actor_id, first_name, last_name FROM actor WHERE last_name = 'WILLIAMS' OR last_name = 'DAVIS';
```

Output

```bash
+----------+------------+-----------+
| actor_id | first_name | last_name |
+----------+------------+-----------+
|        4 | JENNIFER   | DAVIS     |
|      101 | SUSAN      | DAVIS     |
|      110 | SUSAN      | DAVIS     |
|       72 | SEAN       | WILLIAMS  |
|      137 | MORGAN     | WILLIAMS  |
|      172 | GROUCHO    | WILLIAMS  |
+----------+------------+-----------+
```

## Exercise 3-3

Write a query against the rental table that returns the IDs of the customers who rented a film on July 5, 2005 (use the rental.rental_date column, and you can use the date() function to ignore the time component). Include a single row for each distinct customer ID.

```sql
SELECT DISTINCT customer_id FROM rental WHERE DATE(rental.rental_date) = "2005-07-05";
```

Output

```
+-------------+
| customer_id |
+-------------+
|           8 |
|          37 |
|          60 |
|         111 |
|         114 |
|         138 |
...
|         490 |
|         520 |
|         536 |
|         553 |
|         565 |
|         586 |
|         594 |
+-------------+
```

## Exercise 3-4

Fill in the blancks (denoted by <#>) for this multitable query to achieve the following results.

```sql
SELECT c.email, r.return_date
FROM customer c
    INNER JOIN rental r
    ON c.customer_id = r.customer_id
WHERE date(r.rental_date) = '2005-06-14'
ORDER BY r.return_date DESC;
```

Output
```
+---------------------------------------+---------------------+
| email                                 | return_date         |
+---------------------------------------+---------------------+
| DANIEL.CABRAL@sakilacustomer.org      | 2005-06-23 22:00:38 |
| TERRANCE.ROUSH@sakilacustomer.org     | 2005-06-23 21:53:46 |
| MIRIAM.MCKINNEY@sakilacustomer.org    | 2005-06-21 17:12:08 |
| GWENDOLYN.MAY@sakilacustomer.org      | 2005-06-20 02:40:27 |
| JEANETTE.GREENE@sakilacustomer.org    | 2005-06-19 23:26:46 |
| HERMAN.DEVORE@sakilacustomer.org      | 2005-06-19 03:20:09 |
| JEFFERY.PINSON@sakilacustomer.org     | 2005-06-18 21:37:33 |
| MATTHEW.MAHAN@sakilacustomer.org      | 2005-06-18 05:18:58 |
| MINNIE.ROMERO@sakilacustomer.org      | 2005-06-18 01:58:34 |
| SONIA.GREGORY@sakilacustomer.org      | 2005-06-17 21:44:11 |
| TERRENCE.GUNDERSON@sakilacustomer.org | 2005-06-17 05:28:35 |
| ELMER.NOE@sakilacustomer.org          | 2005-06-17 02:11:13 |
| JOYCE.EDWARDS@sakilacustomer.org      | 2005-06-16 21:00:26 |
| AMBER.DIXON@sakilacustomer.org        | 2005-06-16 04:02:56 |
| CHARLES.KOWALSKI@sakilacustomer.org   | 2005-06-16 02:26:34 |
| CATHERINE.CAMPBELL@sakilacustomer.org | 2005-06-15 20:43:03 |
+---------------------------------------+---------------------+
```
