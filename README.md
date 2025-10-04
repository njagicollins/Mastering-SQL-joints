
## Mastering-SQL-joins
## collection of practical SQL joins examples (INNER, LEFT, RIGHT, FULL, CROSS, STRAIGHT, NATURAL, UNION & UNION ALL)

### 1) INNER JOIN
#### Inner join returns only the rows that have a match in both tables. The results set will contain columns from both tables.
#### Example; suppose we have two tables, customers_sales and products_info, and we want to find the customers who have purchased these products.


```sql
SELECT 
   customer_name,
   product_name
FROM customers_sales c
INNER JOIN products_info p
ON c.product_id = p.product_id;
```
 
#### Results; A list of customer names and the product names they purchased



### 2) LEFT JOIN
#### A left join returns all the rows from the left table and the matching rows from the right table. If there are no matches, the results set will contain NULL values for the right table columns.
#### Example: Suppose we want to find all customer names and the products name they purchased if any.


```sql
SELECT 
   customer_name,
   product_name
FROM customers_sales c
LEFT JOIN products_info p
ON c.product_id = p.product_id;
```

#### Results: A list of all customers names along with the product names they purchased. If they didn't purchase any product then the row on that product column will return NULL



### 3) RIGHT JOIN 
#### A right join is similar to a left join, but it returns all the rows from the right table and the matching rows from the left table.
#### Example: Suppose we want to find all the products names and the corresponding customer names who purchased them if any


```sql
SELECT
      customer_name,
      product_name
FROM products_info p
RIGHT JOIN customers_sales c
ON c.product_id = p.product_id;
```

#### Results: A list of products names, along with the customers names if the products have a matching customer. If the product does not have a matching customer, then the customer name column will return NULL



### 4) FULL JOIN
#### A full join returns all rows from both tables, with NULL values in the columns where there are no matches.
#### Suppose we want to find all customer names and product names, including those without matches.


```sql
SELECT 
      customer_name,
      product_name
FROM customers_sales c
FULL JOIN products_info p
ON c.product_id = p.product_id;
```

#### Results: A list of all customers names and products names, with NULL values in the columns where there are no matches.



### 5) CROSS JOIN 
#### A Cross join returns the cartesian product of rows from both tables. Each row of one table is combined with each row of the other table.
#### Example: Suppose we want to find all possible combinations of customers names and products names


```sql
SELECT
     c.customer_name,
     p.product_name
FROM customers_sales c
CROSS JOIN products p;
```



### 6) STRAIGHT JOIN 
#### How it works
#### its like inner join but forces the optimizer to read the tables in the order given, its useful in rare cases for performance tuning
#### Example; Suppose we want to find customers who have purchased products, with the optimizer reading customers names first


```sql
SELECT
    c.customer_name,
    p.product_name
FROM customers_sales c
STRAIGHT_JOIN products_info AS  p
ON c.product_id = p.product_id;
```



### 7) NATURAL JOIN
#### how it functions
#### Is a type of join that combines rows from two tables based on all columns with the same names
#### Example: Suppose we have two tables customers_sales and products_info with a common column product_id. Product_id it will join on that without you writing a condition


```sql
SELECT *
FROM customers_sales
NATURAL JOIN products_info;
```


### 8) UNION
#### How it works
#### it combines results of two queries and removes duplicates. 
#### For example we want to find all customers names and products names


```sql
SELECT sale_id,
customer_name
FROM customers_sales
UNION
SELECT product_id,
product_name
FROM products_info;
```



### 9) UNION ALL
#### How it works
#### Its same as union but keeps duplicates. Its faster because it doesn't check uniqueness.
#### Suppose we want to find all customers and products , including duplicates 


```sql
SELECT sale_id,
customer_name
FROM customers_sales
UNION ALL
SELECT product_id,
product_name
FROM products_info;
```
