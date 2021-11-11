# Chapter 15

## Exercise 15-1

Write a query that lists all of the indexes in the Sakila schmea. Include the table names.

```sql
SELECT table_name, index_name
FROM information_schema.statistics
WHERE table_schema = 'sakila';
```

Output

```
+---------------+-----------------------------+
| TABLE_NAME    | INDEX_NAME                  |
+---------------+-----------------------------+
| actor         | PRIMARY                     |
| actor         | idx_actor_last_name         |
| address       | PRIMARY                     |
| address       | idx_fk_city_id              |
| address       | idx_location                |
| category      | PRIMARY                     |
| city          | PRIMARY                     |
| city          | idx_fk_country_id           |
| country       | PRIMARY                     |
| customer      | PRIMARY                     |
| customer      | idx_fk_store_id             |
| customer      | idx_fk_address_id           |
| customer      | idx_last_name               |
| film          | PRIMARY                     |
| film          | idx_title                   |
| film          | idx_fk_language_id          |
| film          | idx_fk_original_language_id |
| film_actor    | PRIMARY                     |
| film_actor    | PRIMARY                     |
| film_actor    | idx_fk_film_id              |
| film_category | PRIMARY                     |
| film_category | PRIMARY                     |
| film_category | fk_film_category_category   |
| film_text     | PRIMARY                     |
| film_text     | idx_title_description       |
| film_text     | idx_title_description       |
| inventory     | PRIMARY                     |
| inventory     | idx_fk_film_id              |
| inventory     | idx_store_id_film_id        |
| inventory     | idx_store_id_film_id        |
| language      | PRIMARY                     |
| staff         | PRIMARY                     |
| staff         | idx_fk_store_id             |
| staff         | idx_fk_address_id           |
| store         | PRIMARY                     |
| store         | idx_unique_manager          |
| store         | idx_fk_address_id           |
| rental        | PRIMARY                     |
| rental        | rental_date                 |
| rental        | rental_date                 |
| rental        | rental_date                 |
| rental        | idx_fk_inventory_id         |
| rental        | idx_fk_customer_id          |
| rental        | idx_fk_staff_id             |
| payment       | PRIMARY                     |
| payment       | idx_fk_staff_id             |
| payment       | idx_fk_customer_id          |
| payment       | fk_payment_rental           |
| payment       | idx_datetime_amount         |
| payment       | idx_datetime_amount         |
+---------------+-----------------------------+
```

## Exercise 15-2

Write a query that generates output that can be used to create all of the indexes on the sakila.customer table. Output should be of the form

```sql
ALTER TABLE <table_name> ADD INDEX <index_name> (<column_list>)
```

```sql
SELECT concat('ALTER TABLE ', table_name, ' ADD INDEX ', index_name, ' (',
              group_concat(column_name ORDER BY seq_in_index SEPARATOR ', '), ');') create_statement
FROM information_schema.statistics
WHERE table_schema = 'sakila' and table_name = 'customer' 
GROUP BY table_name, index_name;