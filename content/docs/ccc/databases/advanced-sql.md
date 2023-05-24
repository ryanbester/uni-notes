---
title: "6. Advanced SQL"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 6. Advanced SQL

## SQL - Join

Join is used to combine columns from one or more tables based on the values of the common columns between the tables.

The common columns are typically the primary key columns of the first table and foreign key columns of the second table.

Types of joins:

- Inner join
- Left join
- Right join
- Full outer join
- Cross join
- Natural join
- Self-join

![SQL Join Types](/img/ccc/y1/databases/sql-joins.png)

## Table Example

![Table Example](/img/ccc/y1/databases/sql-joins-table-example.png)

### Cross Join

A `CROSS JOIN` produces the Cartesian Product of rows in two or more tables.

The `CROSS JOIN` does not have any matching condition in the join clause.

```sql
SELECT * FROM table1 CROSS JOIN table2;
/* Same as */
SELECT * FROM table1, table2;
/* Also equivalent to */
SELECT * FROM table1 INNER JOIN table2 ON true;
```

![Cross Join](/img/ccc/y1/databases/cross-join.png)

### Natural Join

A `NATURAL JOIN` creates a implicit join based on the same column names in the joined tables.

A natural join can be an `INNER JOIN`, `LEFT JOIN`, or `RIGHT JOIN`. If you do not specify it will be an `INNER JOIN` by default.

If you use a `*` in the select list, the result will contain the following columns:

- All the common columns, which are the columns in both tables that have the same name
- Every column in the first and second tables that is not a common column

```sql
/* Natural Inner Join */
SELECT * FROM table1 NATURAL JOIN table2;
```
![Natural Join Example](/img/ccc/y1/databases/natural-join-example.png)

### Inner Join

An `INNER JOIN` specifies a condition which the pairs of rows satisfy.

Chooses rows where the given columns are equal (relates to the primary key).

```sql
SELECT column_names FROM table1 INNER JOIN table2 ON table1.column_name = table2.column_name;
```

![Inner Join](/img/ccc/y1/databases/inner-join.png)

![Inner Join Example](/img/ccc/y1/databases/inner-join-example.png)

### Left Join or Left Outer Join

The `LEFT JOIN` keyword returns all records from the left table, and the matching records from the right table.

The result is null values from the right side if there is no match.

Unwanted rows can be executed from the right table using the `WHERE` clause.

```sql
SELECT column_names FROM table1 LEFT JOIN table2 ON table1.column_name = table2.column_name;
```

![Left Join](/img/ccc/y1/databases/left-outer-join.png)

![Left Join Example](/img/ccc/y1/databases/left-join-example.png)

### Right Join or Right Outer Join

Opposite version of the left join, it produces a result set that contains all rows from the right table with matching rows from the left table.

If there is no match, the left side will contain null values.

```sql
SELECT column_names FROM table1 RIGHT JOIN table2 ON table1.column_name = table2.column_name;
```

![Right Join](/img/ccc/y1/databases/right-join.png)

![Right Join Example](/img/ccc/y1/databases/right-join-example.png)

### Full Join or Full Outer Join

The `FULL OUTER JOIN` or `FULL JOIN` produces a result set that contains all rows from both the left and right tables, with the matching rows from both sides where available.

If there is no match, the missing side contains null values.

```sql
SELECT column_names FROM table1 FULL OUTER JOIN table2 ON table.column_name = table2.column_name;
```

![Full Join](/img/ccc/y1/databases/full-join.png)

![Full Join Example](/img/ccc/y1/databases/full-join-example.png)

### Self Join

A `SELF JOIN` is a query in which a table is joined to itself.

Self joins are useful for comparing values in a column of rows within the same table.

To form a self-join, you specify the same table twice with different aliases, set up the comparison, and eliminate cases where a value would be equal to itself.

```sql
/* table1 and table2 are aliases for the same table */
SELECT column_names FROM table1, table2;
```

![Self Join Example](/img/ccc/y1/databases/self-join-example.png)
