# Chapter 7

## Exercise 7-1

Write a query that returns the 17th through 25th characters of the string 'please find the substring in this string'

```sql
SELECT SUBSTRING('please find the substring in this string', 17, 25 - 17 + 1);
```

Output

```bash
+------------------------------------------------------------------------+
| SUBSTRING('please find the substring in this string', 17, 25 - 17 + 1) |
+------------------------------------------------------------------------+
| substring                                                              |
+------------------------------------------------------------------------+
```

## Exercise 7-2

Write a query that returns the absolute value and sign (-1, 0, 1) of the number -25.76823. Also return the number rounded to the neareth hundredth

```sql
SELECT ABS(-25.76823), SIGN(-25.76823), ROUND(-25.76823, 2);
```

Output

```bash
+----------------+-----------------+---------------------+
| ABS(-25.76823) | SIGN(-25.76823) | ROUND(-25.76823, 2) |
+----------------+-----------------+---------------------+
|       25.76823 |              -1 |              -25.77 |
+----------------+-----------------+---------------------+
```

## Exercise 7-3

Write a query to return just the month of the current date

```sql
SELECT EXTRACT(MONTH FROM CURRENT_DATE());
```

Output

```bash
+------------------------------------+
| EXTRACT(MONTH FROM CURRENT_DATE()) |
+------------------------------------+
|                                 11 |
+------------------------------------+
```