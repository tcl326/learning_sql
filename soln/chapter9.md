# Chapter 9

## Exercise 9-1

Construct a query against the **film** table that uses a filter condition with a noncorrelated subquery against the **category** table to find all the action films (category.name = 'Action')


```sql
SELECT f.film_id, f.title
FROM film f WHERE f.film_id IN (
    SELECT fc.film_id
    FROM film_category fc
        INNER JOIN category ca
        ON fc.category_id = ca.category_id
    WHERE ca.name = 'Action');
```

Output

```bash
+---------+-------------------------+
| film_id | title                   |
+---------+-------------------------+
|      19 | AMADEUS HOLY            |
|      21 | AMERICAN CIRCUS         |
|      29 | ANTITRUST TOMATOES      |
|      38 | ARK RIDGEMONT           |
|      56 | BAREFOOT MANCHURIAN     |
|      67 | BERETS AGENT            |
|      97 | BRIDE INTRIGUE          |
|     105 | BULL SHAWSHANK          |
|     111 | CADDYSHACK JEDI         |
|     115 | CAMPUS REMEMBER         |
|     126 | CASUALTIES ENCINO       |
|     130 | CELEBRITY HORN          |
|     162 | CLUELESS BUCKET         |
|     194 | CROW GREASE             |
|     205 | DANCES NONE             |
|     210 | DARKO DORADO            |
|     212 | DARN FORRESTER          |
|     229 | DEVIL DESIRE            |
|     250 | DRAGON SQUAD            |
|     252 | DREAM PICKUP            |
|     253 | DRIFTER COMMANDMENTS    |
|     271 | EASY GLADIATOR          |
|     287 | ENTRAPMENT SATISFACTION |
|     292 | EXCITEMENT EVE          |
|     303 | FANTASY TROOPERS        |
|     318 | FIREHOUSE VIETNAM       |
|     327 | FOOL MOCKINGBIRD        |
|     329 | FORREST SONS            |
|     360 | GLASS DYING             |
|     371 | GOSFORD DONNIE          |
|     375 | GRAIL FRANKENSTEIN      |
|     395 | HANDICAP BOONDOCK       |
|     417 | HILLS NEIGHBORS         |
|     501 | KISSING DOLLS           |
|     511 | LAWRENCE LOVE           |
|     530 | LORD ARIZONA            |
|     542 | LUST LOCK               |
|     549 | MAGNOLIA FORRESTER      |
|     574 | MIDNIGHT WESTWARD       |
|     579 | MINDS TRUMAN            |
|     586 | MOCKINGBIRD HOLLYWOOD   |
|     594 | MONTEZUMA COMMAND       |
|     659 | PARK CITIZEN            |
|     664 | PATRIOT ROMAN           |
|     697 | PRIMARY GLASS           |
|     707 | QUEST MUSSOLINI         |
|     717 | REAR TRADING            |
|     732 | RINGS HEARTBREAKERS     |
|     748 | RUGRATS SHAKESPEARE     |
|     793 | SHRUNK DIVINE           |
|     794 | SIDE ARK                |
|     802 | SKY MIRACLE             |
|     823 | SOUTH WAIT              |
|     825 | SPEAKEASY DATE          |
|     838 | STAGECOACH ARMAGEDDON   |
|     850 | STORY SIDE              |
|     869 | SUSPECTS QUILLS         |
|     911 | TRIP NEWTON             |
|     915 | TRUMAN CRAZY            |
|     927 | UPRISING UPTOWN         |
|     964 | WATERFRONT DELIVERANCE  |
|     968 | WEREWOLF LOLA           |
|     982 | WOMEN DORADO            |
|     991 | WORST BANGER            |
+---------+-------------------------+
```

## Exercise 9-2

Rework the query from Exercise 9-1 using a *correlated* subquery against the category and film_category tables to achieve the same results.

```sql
SELECT f.film_id, f.title
FROM film f WHERE EXISTS (
    SELECT 1
    FROM film_category fc
        INNER JOIN category ca
        ON fc.category_id = ca.category_id
    WHERE fc.film_id = f.film_id AND ca.name = 'Action');
```

Output

```bash
+---------+-------------------------+
| film_id | title                   |
+---------+-------------------------+
|      19 | AMADEUS HOLY            |
|      21 | AMERICAN CIRCUS         |
|      29 | ANTITRUST TOMATOES      |
|      38 | ARK RIDGEMONT           |
|      56 | BAREFOOT MANCHURIAN     |
|      67 | BERETS AGENT            |
|      97 | BRIDE INTRIGUE          |
|     105 | BULL SHAWSHANK          |
|     111 | CADDYSHACK JEDI         |
|     115 | CAMPUS REMEMBER         |
|     126 | CASUALTIES ENCINO       |
|     130 | CELEBRITY HORN          |
|     162 | CLUELESS BUCKET         |
|     194 | CROW GREASE             |
|     205 | DANCES NONE             |
|     210 | DARKO DORADO            |
|     212 | DARN FORRESTER          |
|     229 | DEVIL DESIRE            |
|     250 | DRAGON SQUAD            |
|     252 | DREAM PICKUP            |
|     253 | DRIFTER COMMANDMENTS    |
|     271 | EASY GLADIATOR          |
|     287 | ENTRAPMENT SATISFACTION |
|     292 | EXCITEMENT EVE          |
|     303 | FANTASY TROOPERS        |
|     318 | FIREHOUSE VIETNAM       |
|     327 | FOOL MOCKINGBIRD        |
|     329 | FORREST SONS            |
|     360 | GLASS DYING             |
|     371 | GOSFORD DONNIE          |
|     375 | GRAIL FRANKENSTEIN      |
|     395 | HANDICAP BOONDOCK       |
|     417 | HILLS NEIGHBORS         |
|     501 | KISSING DOLLS           |
|     511 | LAWRENCE LOVE           |
|     530 | LORD ARIZONA            |
|     542 | LUST LOCK               |
|     549 | MAGNOLIA FORRESTER      |
|     574 | MIDNIGHT WESTWARD       |
|     579 | MINDS TRUMAN            |
|     586 | MOCKINGBIRD HOLLYWOOD   |
|     594 | MONTEZUMA COMMAND       |
|     659 | PARK CITIZEN            |
|     664 | PATRIOT ROMAN           |
|     697 | PRIMARY GLASS           |
|     707 | QUEST MUSSOLINI         |
|     717 | REAR TRADING            |
|     732 | RINGS HEARTBREAKERS     |
|     748 | RUGRATS SHAKESPEARE     |
|     793 | SHRUNK DIVINE           |
|     794 | SIDE ARK                |
|     802 | SKY MIRACLE             |
|     823 | SOUTH WAIT              |
|     825 | SPEAKEASY DATE          |
|     838 | STAGECOACH ARMAGEDDON   |
|     850 | STORY SIDE              |
|     869 | SUSPECTS QUILLS         |
|     911 | TRIP NEWTON             |
|     915 | TRUMAN CRAZY            |
|     927 | UPRISING UPTOWN         |
|     964 | WATERFRONT DELIVERANCE  |
|     968 | WEREWOLF LOLA           |
|     982 | WOMEN DORADO            |
|     991 | WORST BANGER            |
+---------+-------------------------+
```

## Exercise 9-3

Join the following query to a subquery against the **film_actor** table to show the level of each actor:

```sql
SELECT 'Hollywood Star' level, 30 min_roles, 99999 max_roles
UNION ALL
SELECT 'Prolific Actor' level, 20 min_roles, 29 max_roles
UNION ALL
SELECT 'Newcomer' level, 1 min_roles, 19 max_roles
```

The subquery against the **film_actor** table should count the number of rows for each actor using group by actor_id and the count should be compared to the min_roles/max_roles columns to determine which level each actor belongs to.


```sql
WITH actor_grps AS (
    SELECT 'Hollywood Star' level, 30 min_roles, 99999 max_roles
    UNION ALL
    SELECT 'Prolific Actor' level, 20 min_roles, 29 max_roles
    UNION ALL
    SELECT 'Newcomer' level, 1 min_roles, 19 max_roles
),
actor_agg AS (
    SELECT fa.actor_id, count(*) num_roles
    FROM film_actor fa
    GROUP BY fa.actor_id
)
SELECT actor_agg.actor_id, actor_agg.num_roles, actor_grps.level
FROM actor_agg 
    INNER JOIN actor_grps
    ON actor_agg.num_roles
        BETWEEN actor_grps.min_roles AND actor_grps.max_roles;
```

Output

```bash
+----------+-----------+----------------+
| actor_id | num_roles | level          |
+----------+-----------+----------------+
|        1 |        19 | Newcomer       |
|        2 |        25 | Prolific Actor |
|        3 |        22 | Prolific Actor |
|        4 |        22 | Prolific Actor |
|        5 |        29 | Prolific Actor |
...
|      190 |        27 | Prolific Actor |
|      191 |        30 | Hollywood Star |
|      192 |        29 | Prolific Actor |
|      193 |        23 | Prolific Actor |
|      194 |        22 | Prolific Actor |
|      195 |        27 | Prolific Actor |
|      196 |        30 | Hollywood Star |
|      197 |        33 | Hollywood Star |
|      198 |        40 | Hollywood Star |
|      199 |        15 | Newcomer       |
|      200 |        20 | Prolific Actor |
+----------+-----------+----------------+
```