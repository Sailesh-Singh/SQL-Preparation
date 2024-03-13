# Join Operations in SQL

Join operations in SQL are used to combine rows from two or more tables based on related columns. This allows for retrieving related data from multiple tables in a single query. SQL supports various types of join operations, ranging from basic to advanced techniques.

## [Basic Joins](./Basic/README.md) 
1. **INNER JOIN**: Returns rows when there is at least one match in both tables.

2. **LEFT JOIN**: Returns all rows from the left table and matched rows from the right table.

3. **RIGHT JOIN**: Returns all rows from the right table and matched rows from the left table.

4. **FULL JOIN**: Returns all rows when there is a match in one of the tables.

[Click to learn more ...](./Basic/README.md)

## [Advanced Joins](./Advanced/README.md)

1. **CROSS JOIN**: Returns the Cartesian product of two tables, generating all possible combinations.

2. **Self Join**: Joins a table to itself, useful for comparing rows within the same table.

3. **NATURAL JOIN**: Performs a join by implicitly matching columns with the same name in two tables.

4. **CROSS APPLY and OUTER APPLY** (SQL Server): Applies a table-valued function to each row of the outer table expression.

[Click to learn more ...](./Advanced/README.md)
