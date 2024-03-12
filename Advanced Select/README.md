#   Advanced Select Operations
Advanced SELECT operations in SQL involve more complex queries and additional features to retrieve and manipulate data. Here are some advanced SELECT operations:

**1. Joining Tables:**
   - **INNER JOIN:**
     ```sql
     SELECT * FROM table1 INNER JOIN table2 ON table1.column = table2.column;
     ```
     Retrieves rows when there is a match in both tables based on the specified condition.

   - **LEFT JOIN (or LEFT OUTER JOIN):**
     ```sql
     SELECT * FROM table1 LEFT JOIN table2 ON table1.column = table2.column;
     ```
     Retrieves all rows from the left table and matching rows from the right table.

   - **RIGHT JOIN (or RIGHT OUTER JOIN):**
     ```sql
     SELECT * FROM table1 RIGHT JOIN table2 ON table1.column = table2.column;
     ```
     Retrieves all rows from the right table and matching rows from the left table.

   - **FULL JOIN (or FULL OUTER JOIN):**
     ```sql
     SELECT * FROM table1 FULL JOIN table2 ON table1.column = table2.column;
     ```
     Retrieves all rows when there is a match in either the left or the right table.

**2. Subqueries:**
   - **Scalar Subquery:**
     ```sql
     SELECT column1, (SELECT MAX(column2) FROM table2) AS max_value FROM table1;
     ```
     Uses a subquery to retrieve a single value.

   - **Correlated Subquery:**
     ```sql
     SELECT column1 FROM table1 WHERE column1 > (SELECT AVG(column2) FROM table2 WHERE table2.id = table1.id);
     ```
     Uses values from the outer query in the subquery.

   - **Subquery in FROM clause (Derived Table):**
     ```sql
     SELECT * FROM (SELECT column1 FROM table1) AS derived_table;
     ```
     Creates a temporary table for the subquery.

**3. Aggregation with GROUP BY and HAVING:**
   ```sql
   SELECT department, AVG(salary) AS avg_salary FROM employees GROUP BY department HAVING AVG(salary) > 50000;
   ```
   Groups data based on a column and applies a condition to the grouped data.

**4. Window Functions:**
   ```sql
   SELECT department, salary, ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank FROM employees;
   ```
   Performs calculations across a specified range of rows related to the current row.

**5. UNION, INTERSECT, and EXCEPT (or MINUS):**
   ```sql
   SELECT column1 FROM table1
   UNION
   SELECT column1 FROM table2;
   ```
   Combines the results of two or more SELECT statements.

**6. CASE Statement:**
   ```sql
   SELECT column1, CASE WHEN condition1 THEN 'Category A' WHEN condition2 THEN 'Category B' ELSE 'Category C' END AS category FROM table1;
   ```
   Provides conditional logic within the SELECT statement.

These advanced SELECT operations provide powerful tools for querying and analyzing data in a relational database.


##   Practice Questions

<details>
<summary><b>Type of Triangle</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

    - **Equilateral:** It's a triangle with sides of equal length.
    - **Isosceles:** It's a triangle with sides of equal length.
    - **Scalene:** It's a triangle with sides of differing lengths.
    - **Not A Triangle:** The given values of A, B, and C don't form a triangle.

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    SELECT
    CASE
        WHEN A + B > C AND A + C > B AND B + C > A THEN
            CASE
                WHEN A = B AND B = C THEN
                    'Equilateral'
                WHEN A = B OR B = C OR A = C THEN
                    'Isosceles'
                ELSE
                    'Scalene'
            END
        ELSE
            'Not A Triangle'
    END 
    FROM TRIANGLES;

    ```
   </details>
</details>

<details>
<summary><b>The PADS</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   Generate the following two result sets:

    1. Query an alphabetically ordered list of all names in **OCCUPATIONS**, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: `AnActorName(A)`, `ADoctorName(D)`, `AProfessorName(P)`, and `ASingerName(S)`.

    2. Query the number of ocurrences of each occupation in **OCCUPATIONS**. Sort the occurrences in ascending order, and output them in the following format:

        ```
        There are a total of [occupation_count] [occupation]s.
        ```

    where `[occupation_count]` is the number of occurrences of an occupation in OCCUPATIONS and `[occupation]` is the lowercase occupation name. If more than one Occupation has the same `[occupation_count]`, they should be ordered alphabetically.

    **Note:** There will be at least two entries in the table for each type of occupation.

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    SELECT 
      CONCAT(NAME,'(', LEFT(OCCUPATION, 1), ')') AS Result
    FROM OCCUPATIONS
    ORDER BY Name;

    SELECT
        CONCAT('There are a total of ', COUNT(Occupation),' ',LOWER(Occupation), 's.') AS Result
    FROM OCCUPATIONS
    GROUP BY Occupation
    ORDER BY COUNT(Occupation), LOWER(Occupation);

    ```
   </details>
</details>

<details>
<summary><b>Occupations</b></summary>

+ <details>
    <summary><b>Questions</b></summary>
    Pivot the Occupation column in **OCCUPATIONS** so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.

    **Note:** Print **NULL** when there are no more names corresponding to an occupation.

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    SELECT
    MAX(Doctor) AS Doctor,
    MAX(Professor) AS Professor,
    MAX(Singer) AS Singer,
    MAX(Actor) AS Actor
    FROM (
        SELECT
            CASE WHEN Occupation = 'Doctor' THEN Name END AS Doctor,
            CASE WHEN Occupation = 'Professor' THEN Name END AS Professor,
            CASE WHEN Occupation = 'Singer' THEN Name END AS Singer,
            CASE WHEN Occupation = 'Actor' THEN Name END AS Actor,
            ROW_NUMBER() OVER (PARTITION BY Occupation ORDER BY Name) AS rn
        FROM OCCUPATIONS
    ) AS PivotTable
    GROUP BY rn
    ORDER BY rn;

    ```
   </details>
</details>