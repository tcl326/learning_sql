# Chapter 16

## Exercise 16-1

Write a query that retrieves every row from Sales_Fact, and add a column to generate a ranking based on the tot_sales column values. The highest value should receive a ranking of 1, and the lowest a ranking of 24.

```sql
SELECT year_no, month_no, tot_sales,
    rank() OVER (ORDER BY tot_sales DESC) ranking
FROM sales_fact
```

## Exercise 16-2

Modify the query from the previous exercise to generate two sets of rankings from 1 to 12, one for 2019 data and one for 2020.

```sql
SELECT year_no, month_no, tot_sales,
    rank() OVER (PARTITION BY year_no
                 ORDER BY tot_sales DESC) ranking
FROM sales_fact
```