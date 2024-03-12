# Aggregation and its Operations

### What is Aggregation?

Aggregation in SQL refers to the process of summarizing and combining multiple rows of data into a single result. It involves the use of aggregate functions to perform calculations on groups of rows, returning a single value for each group. Common aggregate functions include COUNT, SUM, AVG, MIN, and MAX.

### Aggregate Functions:

1. **COUNT():** Returns the number of rows in a result set or the number of non-null values in a column.

   Example:
   ```sql
   SELECT COUNT(*) FROM table_name;
   ```

2. **SUM():** Calculates the sum of values in a numeric column.

   Example:
   ```sql
   SELECT SUM(sales_amount) FROM sales_data;
   ```

3. **AVG():** Calculates the average of values in a numeric column.

   Example:
   ```sql
   SELECT AVG(salary) FROM employees;
   ```

4. **MIN():** Returns the minimum value in a column.

   Example:
   ```sql
   SELECT MIN(order_date) FROM orders;
   ```

5. **MAX():** Returns the maximum value in a column.

   Example:
   ```sql
   SELECT MAX(order_date) FROM orders;
   ```

### Grouping Data:

Grouping data allows you to partition the result set into groups based on one or more columns and then perform aggregate calculations on each group.

**GROUP BY Clause:**
```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

### Filtering Grouped Data:

You can further filter aggregated data using the HAVING clause. It works similarly to the WHERE clause but is used with aggregate functions.

**HAVING Clause:**
```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

### Advanced Aggregation Techniques:

1. **Rollup:**
   The ROLLUP operator generates subtotals and a grand total for each group in a result set.

   Example:
   ```sql
   SELECT department, city, SUM(sales_amount)
   FROM sales_data
   GROUP BY ROLLUP(department, city);
   ```

2. **Cube:**
   The CUBE operator produces a result set that represents all possible combinations of grouping sets.

   Example:
   ```sql
   SELECT department, city, SUM(sales_amount)
   FROM sales_data
   GROUP BY CUBE(department, city);
   ```

### Window Functions:

Window functions perform calculations across a set of rows related to the current row within a query result. They are used with an OVER clause to define the window of rows over which the calculation is performed.

**Example:**
```sql
SELECT department, salary,
       AVG(salary) OVER (PARTITION BY department) AS avg_salary
FROM employees;
```

Aggregation operations in SQL are crucial for data analysis, reporting, and decision-making tasks, enabling users to derive meaningful insights from large datasets.

##   Practice Questions

<details>
<summary><b>Top Earners</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

    We define an employee's total earnings to be their monthly *salary x months* worked, and the maximum total earnings to be the maximum total earnings for any employee in the **Employee** table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as 2 space-separated integers.

    **Input Format**

    The **Employee** table containing employee data for a company is described as follows: 

   <img src="assets/topEarners.png" alt="Table" style="height:100%; width:60%">

   where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is the their monthly salary.

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    SELECT MONTHS * SALARY AS EARNINGS, COUNT(EMPLOYEE_ID)
    FROM EMPLOYEE
    GROUP BY EARNINGS
    ORDER BY EARNINGS DESC
    LIMIT 1

    ```
   </details>
</details>

<details>
<summary><b>Weather Observation Station 2</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   Query the following two values from the **STATION** table:
    1. The sum of all values in LAT_N rounded to a scale of  decimal places.
    2. The sum of all values in LONG_W rounded to a scale of decimal places.

    **Input Format**
    The **STATION** table is described as follows:

   <img src="../Basic Select/assets/Weather_Observation_Station-1.jpg" alt="Table" style="height:100%; width:60%">

   where LAT_N is the northern latitude and LONG_W is the western longitude.

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql

    ```
   </details>
</details>