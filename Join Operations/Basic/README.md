# Basic Join Operations in SQL

Join operations in SQL are used to combine rows from two or more tables based on related columns. They allow for retrieving related data from multiple tables in a single query. Basic join operations include INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL JOIN.

## INNER JOIN

The INNER JOIN returns rows when there is at least one match in both tables being joined. It only returns rows where the join condition is met.

### Syntax:
```sql
SELECT columns
FROM table1
INNER JOIN table2 ON table1.column = table2.column;
```

### Example:
Suppose we have two tables: `orders` and `customers`. The `orders` table contains order information, while the `customers` table contains customer details. To retrieve orders along with customer information for matched orders, we can use an INNER JOIN.

```sql
SELECT orders.order_id, customers.customer_name
FROM orders
INNER JOIN customers ON orders.customer_id = customers.customer_id;
```

## LEFT JOIN (or LEFT OUTER JOIN)

The LEFT JOIN returns all rows from the left table and the matched rows from the right table. If there is no match, NULL values are returned for the columns from the right table.

### Syntax:
```sql
SELECT columns
FROM table1
LEFT JOIN table2 ON table1.column = table2.column;
```

### Example:
Continuing with the previous example, if we want to retrieve all orders along with customer information, including orders with no matching customer, we can use a LEFT JOIN.

```sql
SELECT orders.order_id, customers.customer_name
FROM orders
LEFT JOIN customers ON orders.customer_id = customers.customer_id;
```

## RIGHT JOIN (or RIGHT OUTER JOIN)

The RIGHT JOIN returns all rows from the right table and the matched rows from the left table. If there is no match, NULL values are returned for the columns from the left table.

### Syntax:
```sql
SELECT columns
FROM table1
RIGHT JOIN table2 ON table1.column = table2.column;
```

### Example:
If we want to retrieve all customers along with their orders, including customers with no orders, we can use a RIGHT JOIN.

```sql
SELECT orders.order_id, customers.customer_name
FROM orders
RIGHT JOIN customers ON orders.customer_id = customers.customer_id;
```

## FULL JOIN (or FULL OUTER JOIN)

The FULL JOIN returns all rows when there is a match in one of the tables. It returns NULL values for columns from the table that does not have a match.

### Syntax:
```sql
SELECT columns
FROM table1
FULL JOIN table2 ON table1.column = table2.column;
```

### Example:
If we want to retrieve all orders along with customer information, including unmatched orders and customers, we can use a FULL JOIN.

```sql
SELECT orders.order_id, customers.customer_name
FROM orders
FULL JOIN customers ON orders.customer_id = customers.customer_id;
```

##   Practice Questions

<details>
<summary><b>African Cities</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   Given the **CITY** and **COUNTRY** tables, query the names of all cities where the **CONTINENT** is 'Africa'.

   **Note:** CITY.CountryCode and COUNTRY.Code are matching key columns.

   **Input Format**

   The **CITY** and **COUNTRY** tables are described as follows: 

   <img src="./assets/CityTable.jpg" alt="Table" style="height:100%; width:60%">
   <img src="./assets/CountryTable.jpg" alt="Table" style="height:100%; width:60%">

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    SELECT CITY.NAME
    FROM CITY
    JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE
    WHERE COUNTRY.CONTINENT = 'Africa';

    ```
   </details>
</details>


<details>
<summary><b>Average Population of Each Continent</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   Given the **CITY** and **COUNTRY** tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.

   **Note:** CITY.CountryCode and COUNTRY.Code are matching key columns.

   **Input Format**

   The **CITY** and **COUNTRY** tables are described as follows:

   <img src="./assets/CityTable.jpg" alt="Table" style="height:100%; width:60%">
   <img src="./assets/CountryTable.jpg" alt="Table" style="height:100%; width:60%">


   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql
    SELECT COUNTRY.CONTINENT, FLOOR(AVG(CITY.Population))
    FROM CITY
    JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE
    GROUP BY COUNTRY.CONTINENT

    ```
   </details>
</details>


<details>
<summary><b>The Report</b></summary>

+ <details>
    <summary><b>Questions</b></summary>

   You are given two tables: Students and Grades. Students contains three columns ID, Name and Marks.

   <img src="./assets/grade_format.png" alt="Table" style="height:100%; width:60%">

   Grades contains the following data:

   <img src="./assets/grade_contain.png" alt="Table" style="height:100%; width:60%">

   Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

    Write a query to help Eve.

   </details>
+ <details>
    <summary><b>Code</b></summary>
    
    ```sql

    ```
   </details>
</details>