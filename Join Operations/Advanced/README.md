# Advanced Join Operations in SQL

Advanced join operations in SQL provide additional capabilities beyond basic joins, allowing for more complex data retrieval and manipulation. These operations include CROSS JOIN, Self Join, NATURAL JOIN, and APPLY.

## CROSS JOIN

The CROSS JOIN returns the Cartesian product of two tables, generating all possible combinations of rows from both tables.

### Syntax:
```sql
SELECT columns
FROM table1
CROSS JOIN table2;
```

### Example:
Suppose we have two tables, `products` and `customers`. To retrieve all possible combinations of products and customers, we can use a CROSS JOIN.

```sql
SELECT products.product_name, customers.customer_name
FROM products
CROSS JOIN customers;
```

## Self Join

A self join is a join that is used to join a table to itself. It is useful for comparing rows within the same table.

### Syntax:
```sql
SELECT a.columns, b.columns
FROM table_name a, table_name b
WHERE a.common_column = b.common_column;
```

### Example:
Suppose we have a table named `employees` containing employee information including a column named `manager_id` that refers to another employee in the same table who is the manager of the current employee. To retrieve the name of each employee along with the name of their manager, we can use a self join.

```sql
SELECT e1.employee_name AS employee, e2.employee_name AS manager
FROM employees e1
JOIN employees e2 ON e1.manager_id = e2.employee_id;
```

## NATURAL JOIN

The NATURAL JOIN performs a join by implicitly matching columns with the same name in two tables.

### Syntax:
```sql
SELECT columns
FROM table1
NATURAL JOIN table2;
```

### Example:
Suppose we have two tables, `employees` and `departments`, both containing a column named `department_id`. To retrieve all employees along with their respective department information using the common column `department_id`, we can use a NATURAL JOIN.

```sql
SELECT *
FROM employees
NATURAL JOIN departments;
```

## APPLY (CROSS APPLY and OUTER APPLY)

APPLY is used to apply a table-valued function to each row of the outer table expression. SQL Server supports two types of APPLY: CROSS APPLY and OUTER APPLY.

### Syntax:
```sql
SELECT columns
FROM table1
CROSS APPLY function(table1.column) AS alias;

SELECT columns
FROM table1
OUTER APPLY function(table1.column) AS alias;
```

### Example:
Suppose we have a table-valued function named `getOrders` that returns orders for a given customer ID. To retrieve all customers along with their respective orders using the `getOrders` function, we can use CROSS APPLY.

```sql
SELECT customers.customer_id, orders.order_id
FROM customers
CROSS APPLY getOrders(customers.customer_id) AS orders;
```


Advanced join operations in SQL provide powerful capabilities for querying and analyzing data from multiple tables, enabling complex data retrieval and manipulation.

---

## Practice Questions

<details>
<summary><b>SQL Project Planning</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   You are given a table, Projects, containing three columns: Task_ID, Start_Date and End_Date. It is guaranteed that the difference between the End_Date and the Start_Date is equal to 1 day for each row in the table.

   <img src="./assets/SQL_Project_Planning.png" alt="Table" style="height:100%; width:60%">

   If the End_Date of the tasks are consecutive, then they are part of the same project. Samantha is interested in finding the total number of different projects completed.

   Write a query to output the start and end dates of projects listed by the number of days it took to complete the project in ascending order. If there is more than one project that have the same number of completion days, then order by the start date of the project.

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    WITH A AS (
    SELECT Start_Date, ROW_NUMBER() OVER () AS rw
    FROM Projects
    WHERE Start_date NOT IN (SELECT End_Date FROM Projects)
    ),
    B AS (
        SELECT End_Date, ROW_NUMBER() OVER () AS rw
        FROM Projects
        WHERE End_date NOT IN (SELECT Start_Date FROM Projects)
    )

    SELECT A.Start_Date, B.End_Date
    FROM A
    INNER JOIN B ON A.rw = B.rw
    ORDER BY DATEDIFF(B.End_Date, A.Start_Date), A.Start_Date;

    ```
   </details>
</details>


<details>
<summary><b>Placements</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   You are given three tables: Students, Friends and Packages. Students contains two columns: ID and Name. Friends contains two columns: ID and Friend_ID (ID of the ONLY best friend). Packages contains two columns: ID and Salary (offered salary in $ thousands per month).

   <img src="./assets/Placements.png" alt="Table" style="height:100%; width:60%">

   Write a query to output the names of those students whose best friends got offered a higher salary than them. Names must be ordered by the salary amount offered to the best friends. It is guaranteed that no two students got same salary offer.

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    SELECT S.Name
    FROM Students S
    JOIN Friends F ON S.ID = F.ID
    JOIN Packages PS ON F.Friend_ID = PS.ID
    JOIN Packages PS2 ON S.ID = PS2.ID
    WHERE PS.Salary > PS2.Salary
    ORDER BY PS.Salary;

    ```
   </details>
</details>



<details>
<summary><b>Symmetric Pairs</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   You are given a table, Functions, containing two columns: X and Y.
   <img src="./assets/SymmetricPairs.png" alt="Table" style="height:100%; width:60%">

   Two pairs (X1, Y1) and (X2, Y2) are said to be symmetric pairs if X1 = Y2 and X2 = Y1.

   Write a query to output all such symmetric pairs in ascending order by the value of X. List the rows such that X1 ≤ Y1. 


   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    SELECT f1.x,
        f1.y
    FROM   functions AS f1
        INNER JOIN functions AS f2
                ON f1.x = f2.y
                    AND f1.y = f2.x
    GROUP  BY f1.x,
            f1.y
    HAVING f1.x < f1.y
            OR f1.x = f1.y
            AND Count(*) > 1
    ORDER  BY f1.x; 

    ```
   </details>
</details>


<details>
<summary><b>Interviews</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   Samantha interviews many candidates from different colleges using coding challenges and contests. Write a query to print the contest_id, hacker_id, name, and the sums of total_submissions, total_accepted_submissions, total_views, and total_unique_views for each contest sorted by contest_id. Exclude the contest from the result if all four sums are 0.

   **Note:** A specific contest can be used to screen candidates at more than one college, but each college only holds 1 screening contest.

   **Input Format**

   The following tables hold interview data:

    + Contests: The contest_id is the id of the contest, hacker_id is the id of the hacker who created the contest, and name is the name of the hacker.
   <img src="./assets/InterviewContests.png" alt="Table" style="height:100%; width:60%">

    + Colleges: The college_id is the id of the college, and contest_id is the id of the contest that Samantha used to screen the candidates.
   <img src="./assets/InterviewColleges.png" alt="Table" style="height:100%; width:60%">

    + Challenges: The challenge_id is the id of the challenge that belongs to one of the contests whose contest_id Samantha forgot, and college_id is the id of the college where the challenge was given to candidates.
   <img src="./assets/InterviewChallenges.png" alt="Table" style="height:100%; width:60%">

    + View_Stats: The challenge_id is the id of the challenge, total_views is the number of times the challenge was viewed by candidates, and total_unique_views is the number of times the challenge was viewed by unique candidates.
   <img src="./assets/InterviewView_stats.png" alt="Table" style="height:100%; width:60%">

    + Submission_Stats: The challenge_id is the id of the challenge, total_submissions is the number of submissions for the challenge, and total_accepted_submission is the number of submissions that achieved full scores. 
   <img src="./assets/InterviewsSubmission_Stats.png" alt="Table" style="height:100%; width:60%">

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    WITH sum_view_stats AS (
    SELECT challenge_id, SUM(total_views) AS sum_views, SUM(total_unique_views) AS sum_unique_views
    FROM view_stats
    GROUP BY challenge_id
    ),
    sum_submission AS (
        SELECT challenge_id, SUM(total_submissions) AS sum_submissions, SUM(total_accepted_submissions) AS sum_accepted_submissions
        FROM submission_stats
        GROUP BY challenge_id
    )

    SELECT c.contest_id, hacker_id, name,
        SUM(ss.sum_submissions) AS total_submissions,
        SUM(ss.sum_accepted_submissions) AS total_accepted_submissions,
        SUM(svs.sum_views) AS total_views,
        SUM(svs.sum_unique_views) AS total_unique_views
    FROM contests c
    LEFT JOIN colleges ON c.contest_id = colleges.contest_id
    LEFT JOIN challenges ch ON colleges.college_id = ch.college_id
    LEFT JOIN sum_view_stats svs ON ch.challenge_id = svs.challenge_id
    LEFT JOIN sum_submission ss ON ch.challenge_id = ss.challenge_id 
    GROUP BY c.contest_id, hacker_id, name
    HAVING
        SUM(ss.sum_submissions) +
        SUM(ss.sum_accepted_submissions) +
        SUM(svs.sum_views) +
        SUM(svs.sum_unique_views) <> 0
    ORDER BY c.contest_id;

    ```
   </details>
</details>


<details>
<summary><b>15 Days of Learning SQL</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   Julia conducted a 15 days of learning SQL contest. The start date of the contest was March 01, 2016 and the end date was March 15, 2016. Write a query to print total number of unique hackers who made at least 1 submission each day (starting on the first day of the contest), and find the hacker_id and name of the hacker who made maximum number of submissions each day. If more than one such hacker has a maximum number of submissions, print the lowest hacker_id. The query should print this information for each day of the contest, sorted by the date.

   **Input Format**

   The following tables hold contest data:

    + Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker.
   <img src="./assets/Hackers15ays.png" alt="Table" style="height:100%; width:60%">

    + Submissions: The submission_date is the date of the submission, submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, and score is the score of the submission.
   <img src="./assets/Submissions15ays.png" alt="Table" style="height:100%; width:60%">

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql

    ```
   </details>
</details>