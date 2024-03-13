#   Alternative Queries
Alternate Queries in SQL, also known as alternative or optimized queries, are SQL statements that achieve the same result as another query but may differ in syntax, performance, or readability. These queries are often used to provide different perspectives or to optimize query execution. Below are some examples of alternate queries:

### 1. Using JOIN vs. Subquery

**Original Query:**
```sql
SELECT column1, column2
FROM table1
WHERE column3 IN (SELECT column4 FROM table2);
```

**Alternate Query using JOIN:**
```sql
SELECT t1.column1, t1.column2
FROM table1 t1
JOIN table2 t2 ON t1.column3 = t2.column4;
```

### 2. Using EXISTS vs. IN

**Original Query:**
```sql
SELECT column1, column2
FROM table1
WHERE column1 IN (SELECT column1 FROM table2 WHERE condition);
```

**Alternate Query using EXISTS:**
```sql
SELECT column1, column2
FROM table1 t1
WHERE EXISTS (SELECT 1 FROM table2 t2 WHERE t2.column1 = t1.column1 AND condition);
```

### 3. Using UNION vs. OR

**Original Query:**
```sql
SELECT column1 FROM table1 WHERE condition1
UNION
SELECT column1 FROM table1 WHERE condition2;
```

**Alternate Query using OR:**
```sql
SELECT column1 FROM table1 WHERE condition1 OR condition2;
```

### 4. Using CASE vs. UNION ALL

**Original Query:**
```sql
SELECT column1, column2, 'A' AS type FROM table1 WHERE condition1
UNION ALL
SELECT column1, column2, 'B' AS type FROM table1 WHERE condition2;
```

**Alternate Query using CASE:**
```sql
SELECT column1, column2, 
       CASE WHEN condition1 THEN 'A' ELSE 'B' END AS type
FROM table1
WHERE condition1 OR condition2;
```

### 5. Using JOIN vs. Subquery for Aggregation

**Original Query:**
```sql
SELECT t1.column1, SUM(t2.column2) AS total
FROM table1 t1
JOIN table2 t2 ON t1.id = t2.id
GROUP BY t1.column1;
```

**Alternate Query using Subquery for Aggregation:**
```sql
SELECT t1.column1, 
       (SELECT SUM(column2) FROM table2 WHERE id = t1.id) AS total
FROM table1 t1;
```

### 6. Using EXISTS vs. LEFT JOIN

**Original Query:**
```sql
SELECT t1.column1
FROM table1 t1
LEFT JOIN table2 t2 ON t1.id = t2.id
WHERE t2.id IS NULL;
```

**Alternate Query using EXISTS:**
```sql
SELECT t1.column1
FROM table1 t1
WHERE NOT EXISTS (SELECT 1 FROM table2 t2 WHERE t1.id = t2.id);
```

These alternate queries in SQL provide different ways to achieve the same result, allowing for flexibility, optimization, and better readability in database queries. Choosing the appropriate query depends on factors such as performance considerations, database schema, and personal preference.

##  Practice Questions

<details>
<summary><b>Draw The Triangle 1</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):
    ```
    * * * * * 
    * * * * 
    * * * 
    * * 
    *
    ```
    Write a query to print the pattern P(20).

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    WITH RECURSIVE asterisks AS
        (SELECT cast('*' AS char(39)) AS STR
        UNION ALL SELECT concat(STR, ' *') AS STR
        FROM asterisks
        LIMIT 20)
    SELECT STR
    FROM asterisks
    ORDER BY STR DESC;

    ```
   </details>
</details>


<details>
<summary><b>Draw The Triangle 2</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):
    ```
    * 
    * * 
    * * * 
    * * * * 
    * * * * *
    ```
    Write a query to print the pattern P(20).

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    WITH RECURSIVE asterisks AS
        (SELECT cast('*' AS char(39)) AS STR
        UNION ALL SELECT concat(STR, ' *') AS STR
        FROM asterisks
        LIMIT 20)
    SELECT STR
    FROM asterisks
    ORDER BY STR;

    ```
   </details>
</details>