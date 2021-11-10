# Chapter 11

## Exercise 11-1

Rewrite the following query, which uses a simple case expression, so that the same results are achieved using a searched case expression. Try to use as few when clauses as possible

```sql
SELECT name,
    CASE name
        WHEN 'English' THEN 'latin1'
        WHEN 'Italian' then 'latin1'
        WHEN 'French' THEN 'latin1'
        WHEN 'German' THEN 'latin1'
        WHEN 'Japanese' THEN 'utf8'
        WHEN 'Mandarin' THEN 'utf8'
        ELSE 'Unknown'
    END character_set
FROM language;
```

Answer

```sql
SELECT name,
    CASE
        WHEN name IN ('English', 'Italian', 'French', 'German') THEN 'latin1'
        WHEN name IN ('Japanese', 'Mandarin') THEN 'utf8'
        ELSE 'Unknown'
    END character_set
FROM language;
```

Output

```bash
+----------+---------------+
| name     | character_set |
+----------+---------------+
| English  | latin1        |
| Italian  | latin1        |
| Japanese | utf8          |
| Mandarin | utf8          |
| French   | latin1        |
| German   | latin1        |
+----------+---------------+
```

## Exercise 11-2

Rewrite the following query so that the result set contains a single row with five columns (one for each rating). Name the five columns G, PG, PG_13, R, and NC_17

```sql
SELECT rating, count(*)
FROM film
GROUP BY rating;
```

Answer

```sql
SELECT
    SUM(CASE WHEN rating = 'G' THEN 1 ELSE 0 END) G,
    SUM(CASE WHEN rating = 'PG' THEN 1 ELSE 0 END) PG,
    SUM(CASE WHEN rating = 'PG-13' THEN 1 ELSE 0 END) PG_13,
    SUM(CASE WHEN rating = 'R' THEN 1 ELSE 0 END) R,
    SUM(CASE WHEN rating = 'NC-17' THEN 1 ELSE 0 END) NC_17
FROM film;
```

Output

```bash
+------+------+-------+------+-------+
| G    | PG   | PG_13 | R    | NC_17 |
+------+------+-------+------+-------+
|  178 |  194 |   223 |  195 |   210 |
+------+------+-------+------+-------+
```