# Chapter 5

## Exercise 5-1

Fill in the blanks (denoted by <#>) for the following query to obtain the results that follow:

```sql
SELECT c.first_name, c.last_name, a.address, ct.city
FROM customer c
    INNER JOIN address a
    ON c.address_id = a.address_id
    INNER JOIN city ct
    ON a.city_id = ct.city_id
WHERE a.district = 'California';
```

Output

```bash
+------------+-----------+------------------------+----------------+
| first_name | last_name | address                | city           |
+------------+-----------+------------------------+----------------+
| PATRICIA   | JOHNSON   | 1121 Loja Avenue       | San Bernardino |
| BETTY      | WHITE     | 770 Bydgoszcz Avenue   | Citrus Heights |
| ALICE      | STEWART   | 1135 Izumisano Parkway | Fontana        |
| ROSA       | REYNOLDS  | 793 Cam Ranh Avenue    | Lancaster      |
| RENEE      | LANE      | 533 al-Ayn Boulevard   | Compton        |
| KRISTIN    | JOHNSTON  | 226 Brest Manor        | Sunnyvale      |
| CASSANDRA  | WALTERS   | 920 Kumbakonam Loop    | Salinas        |
| JACOB      | LANCE     | 1866 al-Qatif Avenue   | El Monte       |
| RENE       | MCALISTER | 1895 Zhezqazghan Drive | Garden Grove   |
+------------+-----------+------------------------+----------------+
```

## Exercise 5-2

Write a query that returns the title of every film in which an actor with the first name JOHN appeared.

```sql
SELECT f.title
FROM film f
    INNER JOIN film_actor fa
    ON f.film_id = fa.film_id
    INNER JOIN actor a
    ON fa.actor_id = a.actor_id
WHERE a.first_name = "JOHN";
```

Output

```bash
+---------------------------+
| title                     |
+---------------------------+
| ALLEY EVOLUTION           |
| BEVERLY OUTLAW            |
| CANDLES GRAPES            |
| CLEOPATRA DEVIL           |
| COLOR PHILADELPHIA        |
| CONQUERER NUTS            |
| DAUGHTER MADIGAN          |
| GLEAMING JAWBREAKER       |
| GOLDMINE TYCOON           |
| HOME PITY                 |
| INTERVIEW LIAISONS        |
| ISHTAR ROCKETEER          |
| JAPANESE RUN              |
| JERSEY SASSY              |
| LUKE MUMMY                |
| MILLION ACE               |
| MONSTER SPARTACUS         |
| NAME DETECTIVE            |
| NECKLACE OUTBREAK         |
| NEWSIES STORY             |
| PET HAUNTING              |
| PIANIST OUTFIELD          |
| PINOCCHIO SIMON           |
| PITTSBURGH HUNCHBACK      |
| QUILLS BULL               |
| RAGING AIRPLANE           |
| ROXANNE REBEL             |
| SATISFACTION CONFIDENTIAL |
| SONG HEDWIG               |
+---------------------------+
```

## Exercise 5-3

Construct a query that returns all addresses that are in the same city. You will need ot join the address table to itself, and each row should include two different addresses.

```sql
SELECT a1.address address_1, a2.address address_2
FROM address a1
    INNER JOIN address a2
    ON a1.city_id = a2.city_id
WHERE a1.address_id <> a2.address_id;
```

Ouptut

```bash
+----------------------+----------------------+
| address_1            | address_2            |
+----------------------+----------------------+
| 47 MySakila Drive    | 23 Workhaven Lane    |
| 28 MySQL Boulevard   | 1411 Lillydale Drive |
| 23 Workhaven Lane    | 47 MySakila Drive    |
| 1411 Lillydale Drive | 28 MySQL Boulevard   |
| 1497 Yuzhou Drive    | 548 Uruapan Street   |
| 587 Benguela Manor   | 43 Vilnius Manor     |
| 548 Uruapan Street   | 1497 Yuzhou Drive    |
| 43 Vilnius Manor     | 587 Benguela Manor   |
+----------------------+----------------------+
```

