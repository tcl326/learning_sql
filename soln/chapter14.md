# Chapter 14

## Exercise 14-1

Create a view definition that can be used by the following query to generate the given results:

```sql
SELECT title, category_name, first_name, last_name
FROM film_ctgry_actor
WHERE last_name = 'FAWCETT';
```

Answer

```sql
CREATE VIEW film_ctgry_actor
AS
SELECT f.film_id,
    f.title title,
    f_ca.category_id,
    ca.name category_name,
    f_a.actor_id,
    a.first_name first_name,
    a.last_name last_name
FROM film f
    INNER JOIN film_category f_ca
    ON f.film_id = f_ca.film_id
    INNER JOIN category ca
    ON f_ca.category_id = ca.category_id
    INNER JOIN film_actor f_a
    ON f_a.film_id = f.film_id
    INNER JOIN actor a
    ON f_a.actor_id = a.actor_id;
```

Output

```bash
+---------------------+---------------+------------+-----------+
| title               | category_name | first_name | last_name |
+---------------------+---------------+------------+-----------+
| ACE GOLDFINGER      | Horror        | BOB        | FAWCETT   |
| ADAPTATION HOLES    | Documentary   | BOB        | FAWCETT   |
| CHINATOWN GLADIATOR | New           | BOB        | FAWCETT   |
| CIRCUS YOUTH        | Children      | BOB        | FAWCETT   |
| CONTROL ANTHEM      | Comedy        | BOB        | FAWCETT   |
| DARES PLUTO         | Animation     | BOB        | FAWCETT   |
| DARN FORRESTER      | Action        | BOB        | FAWCETT   |
| DAZED PUNK          | Games         | BOB        | FAWCETT   |
| DYNAMITE TARZAN     | Classics      | BOB        | FAWCETT   |
| HATE HANDICAP       | Comedy        | BOB        | FAWCETT   |
| HOMICIDE PEACH      | Family        | BOB        | FAWCETT   |
| JACKET FRISCO       | Drama         | BOB        | FAWCETT   |
| JUMANJI BLADE       | New           | BOB        | FAWCETT   |
| LAWLESS VISION      | Animation     | BOB        | FAWCETT   |
| LEATHERNECKS DWARFS | Travel        | BOB        | FAWCETT   |
| OSCAR GOLD          | Animation     | BOB        | FAWCETT   |
| PELICAN COMFORTS    | Documentary   | BOB        | FAWCETT   |
| PERSONAL LADYBUGS   | Music         | BOB        | FAWCETT   |
| RAGING AIRPLANE     | Sci-Fi        | BOB        | FAWCETT   |
| RUN PACIFIC         | New           | BOB        | FAWCETT   |
| RUNNER MADIGAN      | Music         | BOB        | FAWCETT   |
| SADDLE ANTITRUST    | Comedy        | BOB        | FAWCETT   |
| SCORPION APOLLO     | Drama         | BOB        | FAWCETT   |
| SHAWSHANK BUBBLE    | Travel        | BOB        | FAWCETT   |
| TAXI KICK           | Music         | BOB        | FAWCETT   |
| BERETS AGENT        | Action        | JULIA      | FAWCETT   |
| BOILED DARES        | Travel        | JULIA      | FAWCETT   |
| CHISUM BEHAVIOR     | Family        | JULIA      | FAWCETT   |
| CLOSER BANG         | Comedy        | JULIA      | FAWCETT   |
| DAY UNFAITHFUL      | New           | JULIA      | FAWCETT   |
| HOPE TOOTSIE        | Classics      | JULIA      | FAWCETT   |
| LUKE MUMMY          | Animation     | JULIA      | FAWCETT   |
| MULAN MOON          | Comedy        | JULIA      | FAWCETT   |
| OPUS ICE            | Foreign       | JULIA      | FAWCETT   |
| POLLOCK DELIVERANCE | Foreign       | JULIA      | FAWCETT   |
| RIDGEMONT SUBMARINE | New           | JULIA      | FAWCETT   |
| SHANGHAI TYCOON     | Travel        | JULIA      | FAWCETT   |
| SHAWSHANK BUBBLE    | Travel        | JULIA      | FAWCETT   |
| THEORY MERMAID      | Animation     | JULIA      | FAWCETT   |
| WAIT CIDER          | Animation     | JULIA      | FAWCETT   |
+---------------------+---------------+------------+-----------+
```

## Exercise 14-2

The film rental compnany manager would like to have a report that includes the name of every country, along with the total payments for all customers who live in each country. Generate a view definition that queries the country table and uses a scalar subquery to calculate a value for a column named tot_payments.

```sql
CREATE VIEW country_pymnt_vw
AS
SELECT c.country_id, c.country, sum(p.amount)
FROM country c
    LEFT OUTER JOIN city ct
    ON ct.country_id = c.country_id
    LEFT OUTER JOIN address a
    ON ct.city_id = a.city_id
    LEFT OUTER JOIN customer cu
    ON cu.address_id = a.address_id
    LEFT OUTER JOIN payment p
    ON p.customer_id = cu.customer_id
GROUP BY c.country_id
ORDER BY c.country_id;
```

Output

```bash
+------------+---------------------------------------+---------------+
| country_id | country                               | sum(p.amount) |
+------------+---------------------------------------+---------------+
|          1 | Afghanistan                           |         67.82 |
|          2 | Algeria                               |        383.10 |
|          3 | American Samoa                        |         71.80 |
|          4 | Angola                                |        215.48 |
|          5 | Anguilla                              |        106.65 |
|          6 | Argentina                             |       1434.48 |
|          7 | Armenia                               |        118.75 |
|          8 | Australia                             |          NULL |
|          9 | Austria                               |        307.22 |
|         10 | Azerbaijan                            |        245.43 |
|         11 | Bahrain                               |        112.75 |
|         12 | Bangladesh                            |        402.05 |
|         13 | Belarus                               |        277.34 |
|         14 | Bolivia                               |        183.53 |
|         15 | Brazil                                |       3200.52 |
|         16 | Brunei                                |        113.65 |
|         17 | Bulgaria                              |        204.50 |
|         18 | Cambodia                              |        191.47 |
|         19 | Cameroon                              |        200.46 |
|         20 | Canada                                |        593.63 |
|         21 | Chad                                  |        135.68 |
|         22 | Chile                                 |        328.29 |
|         23 | China                                 |       5802.73 |
|         24 | Colombia                              |        709.41 |
|         25 | Congo, The Democratic Republic of the |        212.50 |
|         26 | Czech Republic                        |        133.71 |
|         27 | Dominican Republic                    |        318.23 |
|         28 | Ecuador                               |        390.13 |
|         29 | Egypt                                 |        694.39 |
|         30 | Estonia                               |        115.70 |
|         31 | Ethiopia                              |         91.77 |
|         32 | Faroe Islands                         |        114.72 |
|         33 | Finland                               |        101.74 |
|         34 | France                                |        374.04 |
|         35 | French Guiana                         |        103.78 |
|         36 | French Polynesia                      |        235.46 |
|         37 | Gambia                                |        129.70 |
|         38 | Germany                               |        831.04 |
|         39 | Greece                                |        232.46 |
|         40 | Greenland                             |        137.66 |
|         41 | Holy See (Vatican City State)         |        152.66 |
|         42 | Hong Kong                             |        142.70 |
|         43 | Hungary                               |        111.71 |
|         44 | India                                 |       6630.27 |
|         45 | Indonesia                             |       1510.33 |
|         46 | Iran                                  |        950.75 |
|         47 | Iraq                                  |        111.73 |
|         48 | Israel                                |        422.01 |
|         49 | Italy                                 |        831.11 |
|         50 | Japan                                 |       3471.74 |
|         51 | Kazakstan                             |        198.48 |
|         52 | Kenya                                 |        253.46 |
|         53 | Kuwait                                |        111.74 |
|         54 | Latvia                                |        262.40 |
|         55 | Liechtenstein                         |        114.72 |
|         56 | Lithuania                             |         73.76 |
|         57 | Madagascar                            |         93.78 |
|         58 | Malawi                                |        123.72 |
|         59 | Malaysia                              |        369.15 |
|         60 | Mexico                                |       3307.04 |
|         61 | Moldova                               |        127.66 |
|         62 | Morocco                               |        307.29 |
|         63 | Mozambique                            |        344.20 |
|         64 | Myanmar                               |        194.48 |
|         65 | Nauru                                 |        148.69 |
|         66 | Nepal                                 |        116.78 |
|         67 | Netherlands                           |        586.66 |
|         68 | New Zealand                           |         92.76 |
|         69 | Nigeria                               |       1511.48 |
|         70 | North Korea                           |        113.69 |
|         71 | Oman                                  |        187.50 |
|         72 | Pakistan                              |        525.72 |
|         73 | Paraguay                              |        275.38 |
|         74 | Peru                                  |        468.88 |
|         75 | Philippines                           |       2381.32 |
|         76 | Poland                                |        877.97 |
|         77 | Puerto Rico                           |        254.39 |
|         78 | Romania                               |        235.38 |
|         79 | Runion                                |        216.54 |
|         80 | Russian Federation                    |       3045.87 |
|         81 | Saint Vincent and the Grenadines      |         96.75 |
|         82 | Saudi Arabia                          |        523.79 |
|         83 | Senegal                               |        100.75 |
|         84 | Slovakia                              |         89.74 |
|         85 | South Africa                          |       1204.15 |
|         86 | South Korea                           |        574.65 |
|         87 | Spain                                 |        606.58 |
|         88 | Sri Lanka                             |        116.70 |
|         89 | Sudan                                 |        227.46 |
|         90 | Sweden                                |        144.66 |
|         91 | Switzerland                           |        252.39 |
|         92 | Taiwan                                |       1210.94 |
|         93 | Tanzania                              |        341.17 |
|         94 | Thailand                              |        419.04 |
|         95 | Tonga                                 |         73.82 |
|         96 | Tunisia                               |         78.77 |
|         97 | Turkey                                |       1662.12 |
|         98 | Turkmenistan                          |        136.73 |
|         99 | Tuvalu                                |        120.74 |
|        100 | Ukraine                               |        730.42 |
|        101 | United Arab Emirates                  |        333.16 |
|        102 | United Kingdom                        |        924.80 |
|        103 | United States                         |       4110.32 |
|        104 | Venezuela                             |        683.30 |
|        105 | Vietnam                               |        746.28 |
|        106 | Virgin Islands, U.S.                  |        122.68 |
|        107 | Yemen                                 |        510.83 |
|        108 | Yugoslavia                            |        259.43 |
|        109 | Zambia                                |        134.67 |
+------------+---------------------------------------+---------------+
```