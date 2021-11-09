# Chapter 6

## Exercise 6-1

If set A = {L M N O P} and set B = {P Q R S T}, what sets are generated by the following operations?

- A **union** B = {L M N O P Q R S T}
- A **union all** B = {L M N O P P Q R S T}
- A **intersect** B = {P}
- A **except** B = {L M N O}

## Exercise 6-2

Write a compound query that finds the first and last names of all actors and customers whose last name starts with L.

```sql
SELECT a.first_name first_name, a.last_name last_name
FROM actor a
WHERE a.last_name LIKE 'L%'
UNION
SELECT c.first_name, c.last_name
FROM customer c
WHERE c.last_name LIKE 'L%';
```

Output

```bash
+------------+--------------+
| first_name | last_name    |
+------------+--------------+
| MATTHEW    | LEIGH        |
| JOHNNY     | LOLLOBRIGIDA |
| MISTY      | LAMBERT      |
| JACOB      | LANCE        |
| RENEE      | LANE         |
| HEIDI      | LARSON       |
| DARYL      | LARUE        |
| LAURIE     | LAWRENCE     |
| JEANNE     | LAWSON       |
| LAWRENCE   | LAWTON       |
| KIMBERLY   | LEE          |
| LOUIS      | LEONE        |
| SARAH      | LEWIS        |
| GEORGE     | LINTON       |
| MAUREEN    | LITTLE       |
| DWIGHT     | LOMBARDI     |
| JACQUELINE | LONG         |
| AMY        | LOPEZ        |
| BARRY      | LOVELACE     |
| PRISCILLA  | LOWE         |
| VELMA      | LUCAS        |
| WILLARD    | LUMPKIN      |
| LEWIS      | LYMAN        |
| JACKIE     | LYNCH        |
+------------+--------------+
```

## Exercise 6-3

Sort the results from Exercise 6-2 by the last_name column

```sql
SELECT a.first_name first_name, a.last_name last_name
FROM actor a
WHERE a.last_name LIKE 'L%'
UNION
SELECT c.first_name, c.last_name
FROM customer c
WHERE c.last_name LIKE 'L%'
ORDER BY last_name;
```