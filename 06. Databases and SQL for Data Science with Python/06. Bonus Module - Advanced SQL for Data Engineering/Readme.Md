# Advanced SQL for Data Engineering
## Views, Stored Procedures, and Transactions
### Views
A view is an alternative way of representing data that exists in one or more tables or views. A view can include all or some of the columns from one or more base tables or existing views. Creating a view creates a named specification of a results table, which can be queried in the same way as a table. Only the definition of the view is stored, not the data.

Views can:
* Show a selection of data for a given table
* Combine two or more tables in meaningful ways
* Simplify access to data
* Show only portions of data in the table

An example of why to use a view would be to display only non-sensitive data from an Employees table.

#### View Syntax
The syntax of a `CREATE VIEW` statement is as follows:
```sql
    CREATE VIEW view_name AS
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition ; 
```

The syntax of a `REPLACE VIEW` statement is as follows:
```sql
    CREATE OR REPLACE VIEW view_name AS
    SELECT column_1, column_2, ...
    FROM table_name
    WHERE condition ;
```

The syntax of a `DROP VIEW` statement is as follows:
```sql
    DROP VIEW view_name ;
```

### Stored Procedures
A stored procedure is a set of SQL statements stored and executed on the database server. It can be written in many different languages, accept information in the form of parameters, and return results to the client.

Some benefits include:

* Reduction in network traffic because only one call is needed to execute multiple statements.
* Improvement in performance because the processing happens on the server where the data is stored, with just the final result being passed back to the client.
* Reuse of code because multiple applications can use the same stored procedure for the same job. 
* Increase in security because:
  * You do not need to expose all your table and column information to client-side developers
  * You can use server-side logic to validate data before accepting it into the system.
* They can reduce network traffic, improve performance, reuse code, and increase security 
* Stored procedures can be called from external applications and dynamic SQL statements

#### Stored Procedure Syntax
The syntax of a stored procedure is as follows:

<img src="https://user-images.githubusercontent.com/13508894/279633562-5aa67b23-8e23-4fab-9369-792c90297e16.png" width="800" />

And to call the stored procedure, run the following:
```sql
  CALL RETRIEVE_ALL ; 
```

where `RETRIEVE_ALL` was the stored procedure defined previously.

### ACID Transactions
A transaction is an indivisible unit of work. It can consist of one or more SQL statements, but to be considered successful, either all of those SQL statements must complete successfully, leaving the database in a new stable state, or none must complete, leaving the database as it was before the transaction began.

ACID stands for:

* Atomic – all changes must be performed successfully, or not at all
* Consistent – data must be in a consistent state before and after the transaction
* Isolated – no other process can change the data while the transaction is running
* Durable – the changes made by the transaction must persist

SQL commands `BEGIN`, `COMMIT`, and `ROLLBACK` are used to manage ACID transactions. SQL commands can be called from languages like C, R and Python.

Example:
A classic example transaction is an item purchase from a shop. Consider the 2 tables below, `BankAccounts` and `ShoeShop`.

<img src="https://user-images.githubusercontent.com/13508894/279634689-79d3524f-3148-4f91-926c-1ddef89e1387.png" width="700" />

If Rose buys a pair of Boots for £200, the following ACID commands must all be followed:

<img src="https://user-images.githubusercontent.com/13508894/279635102-27e37055-e038-49e9-bbc7-26932ca585c3.png" width="800" />

Rose's balance, and the `ShoeShop` balance must be updated in the `BankAccounts` table. The Boots stock must also be updated in the `ShoeShop` table.

## `JOIN` Statements
A JOIN combines the rows from two or more tables based on a relationship between certain columns in these tables. The column/s in each table to be used as a link between the tables must first be identified, and to do this, a join is usually created between a primary key in one table and a foreign key in another.

<img src="https://user-images.githubusercontent.com/13508894/279635766-06adbf60-aa2b-4d9d-9a5b-e5f0ff4606f2.png" width="800" />

The syntax for all types of `JOIN` are shown below, and the following sections go into more detail, with examples.

<img src="https://user-images.githubusercontent.com/13508894/279635945-90257ebb-9a09-4897-a7db-833f6a52d2bd.png" width="800" />

How does a JOIN look like between more than 2 tables?
```sql
SELECT E.F_NAME, E.L_NAME, JH.START_DATE, J.JOB_TITLE
FROM EMPLOYEES E
INNER JOIN JOB_HISTORY JH ON E.EMP_ID = JH.EMPL_ID
INNER JOIN JOBS J ON J.JOB_IDENT = JH.JOBS_ID
where E.DEP_ID = '5'
```

How does a LEFT join look like that includes a condition?
```sql
SELECT E.EMP_ID, E.L_NAME, E.DEP_ID, D.DEP_NAME
FROM EMPLOYEES E LEFT JOIN DEPARTMENTS D
ON E.DEP_ID = D.DEPT_ID_DEP  
AND YEAR(E.B_DATE) < 1980
```



### `INNER JOIN`
An `INNER JOIN` displays only the rows from two tables that have matching value in a common column, usually the primary key of one table that exists as a foreign key in the second table.

For example, to retrieve a list of all people who are borrowing books, and the date of the loan, data is needed from the `borrower` table and the `loan` table.

* In the `FROM` clause, specify the join between the borrower table and the loan table as `BORROWER INNER JOIN LOAN`.
* Identify the `borrower` table as `B`, and the `loan` table as `L` (and use these aliases).
* The table specified on the left of the `JOIN` clause is known as the left table – in this case, the `borrower` table is the left table.
* For this join, select borrower ID, last name, and country from the `borrower` table, and the borrower ID and the loan date from the `loan` table.
* In the `ON` clause, specify the `JOIN` predicate, in this case the condition that the borrower ID in the `borrower` table is equal to the borrower ID in the `loan` table.

<img src="https://user-images.githubusercontent.com/13508894/279637106-445bd92f-10d4-4537-9bbd-c9643deba2a9.png" width="800" />

The result set shows only the rows from both tables that have the same borrower ID. The rows are displayed if the `Borrower_Id` matches. Rows with `Borrower_IDs` that do not match are not displayed.

<img src="https://user-images.githubusercontent.com/13508894/279637705-4f385232-d0fa-401a-a60f-43b45470e67f.png" width="800" />

The `Borrower_Id`, `Lastname`, and `Country` columns are taken from the `Borrower` table and joined to the `Borrower_Id` and `Loan_Date` columns from the `Loan` table to make the result set.

### `OUTER JOIN`
Outer joins, like inner joins, return the rows from each table that have matching values in the join columns. Unlike inner joins, outer joins also return the rows that do not have a match between the tables.

SQL offers three types of outer joins:

* `LEFT OUTER JOIN`
* `RIGHT OUTER JOIN`
* `FULL OUTER JOIN`

<img src="https://user-images.githubusercontent.com/13508894/279638368-350678b2-2d56-4648-adcb-3f025230c0a2.png" width="800" />

#### `LEFT JOIN` Operator
A left outer join returns all the rows from the left table, and any matching rows from the right table. An example is shown below:

<img src="https://user-images.githubusercontent.com/13508894/279638589-f5359b91-49e3-44ad-add5-dd04cc7c59ab.png" width="800" />

* The `Borrower` table is the first table specified in the `FROM` clause of the `SELECT` statement, so the `Borrower` table is the LEFT table, and the `Loan` table is the RIGHT table.
* In the `FROM` clause, `Borrower` is listed on the left side of the join operator, therefore all rows from the `Borrower` table will be selected and combined with the contents of the `Loan` table based on the criteria specified in the query.
* In this example, the criteria is the `BORROWER ID` column. For a `LEFT OUTER JOIN`, simply called a `LEFT JOIN`, the following columns from the `Borrower` table will be selected: `BorrowerID`, `LastName`, and `Country`, and the following columns will also be selected from the `Loan` table: `BorrowerID`, and `LoanDate`.
* The `LEFT JOIN` selects each `BORROWER ID` in the `Borrower` table and displays the `LoanDate` from the `Loan` table. The result set shows each `Borrower ID` from the `Borrower` table, and the loan date for that borrower. For example, there is no loan date for the last three rows, so the borrower ID and loan date show null values.

#### `RIGHT JOIN` Operator
A right outer join returns all the rows from the right table, and any matching rows from the left table. An example is shown below:

<img src="https://user-images.githubusercontent.com/13508894/279639692-e88d4a25-8238-4f82-842c-b41bad300c8a.png" width="800" />

* In the `FROM` clause, the `Loan` table is listed on the right side of the join operator, therefore all rows from the Loan table will be selected and combined with the contents of the `Borrower` table based on the criteria specified in the query.
* The criteria is the `BORROWER_ID` column. For a `RIGHT JOIN`, the following columns will be selected from the `Loan` table: `Borrower_ID`, and `LoanDate`, and the following columns will also be selected from the `Borrower` table: `Borrower_ID`, `LastName`, and `Country` where the `Borrower_ID` in the `Loan` table matches the `Borrower_ID` in the `Borrower` table.
* The result set shows each `Borrower_ID` from the `Loan` table and the `LoanDate` for that Borrower, where the `Borrower_ID` in the `Loan` table also exists in the `Borrower` table.
* For the last row, there is no matching row in the `Borrower` table, so the `Borrower_ID`, `Lastname`, and `Country` show null values. This could indicate a problem for the library; it indicates there is a book on loan to an unknown person.

#### `FULL JOIN` Operator
A full outer join, or full join, returns all rows from both tables. An example is shown below:

<img src="https://user-images.githubusercontent.com/13508894/279640530-320553cb-0b74-4668-8d11-747e61f2467e.png" width="800" />

* For a `FULL JOIN`, all rows are selected from the `Borrower` table and all rows from the `Loan` table are also selected.
* The result set shows all eight records from the `Borrower` table listed with the corresponding data from the `Loan` table.

Example:
Perform a Full Join on the EMPLOYEES and DEPARTMENT tables and select the First name, Last name and Department name of all employees.

```sql
select E.F_NAME,E.L_NAME,D.DEP_NAME
from EMPLOYEES AS E 
LEFT OUTER JOIN DEPARTMENTS AS D ON E.DEP_ID=D.DEPT_ID_DEP

UNION

select E.F_NAME,E.L_NAME,D.DEP_NAME
from EMPLOYEES AS E 
RIGHT OUTER JOIN DEPARTMENTS AS D ON E.DEP_ID=D.DEPT_ID_DEP
```
