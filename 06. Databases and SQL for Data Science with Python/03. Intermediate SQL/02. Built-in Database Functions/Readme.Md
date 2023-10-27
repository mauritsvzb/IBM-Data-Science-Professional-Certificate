
### Built-in Database Functions
Most databases come with built-in SQL functions, and these can be included as part of SQL statements. These functions can often significantly reduce the amount of data that needs to be retrieved, and will therefore speed up data processing.

## Aggregate or Column Functions
The input here is a collection of values (e.g. an entire column), and the output is a single value. Examples include:

* `SUM()`
* `MIN()`
* `MAX()`
* `AVG()`
For example, to return the sum of the cost column in TABLE,
```
SELECT SUM(COST) FROM TABLE ;
```
To explicitly name the returned column, use a column alias, as follows:
```
SELECT SUM(COST) AS SUM_OF_COST FROM TABLE ;
```

## Scalar and String Functions
These functions perform operations on every input value, and some examples include:

* `ROUND()`
* `LENGTH`
* `UCASE()`
* `LCASE()`
For example, the following will round up every value in the COST column:
```
SELECT ROUND(COST) FROM TABLE ;
```

and the following will return the length of each value in the ANIMAL column (i.e. the number of letters in the string):
```
SELECT LENGTH(ANIMAL) FROM TABLE ;
```

These functions can be used with the `WHERE` clause, e.g.
```
SELECT * FROM TABLE
    WHERE LCASE(ANIMAL) = 'cat' ;
```

## Date and Time Built-in Functions
Most databases contain special datatypes for dates and times, e.g.

* DATE: `YYYYMMDD`
* TIME: `HHMMSS`
* TIMESTAMP: `YYYYXXDDHHMMSSZZZZZZ`

Some common date/time functions include: 

* `YEAR()`
* `MONTH()`
* `DAY()`
* `DAYOFMONTH()`
* `DAYOFWEEK()`
* `DAYOFYEAR()`
* `WEEK()`
* `HOUR()`
* `MINUTE()`
* `SECOND()`

So, for example, to get the number of rescues during the month of May:
```
SELECT COUNT(*) FROM TABLE
    WHERE MONTH(RESCUEDATE) = '05' ;
```

The `INTERVAL` function is used to perform operations involving date and time intervals. It's typically used in conjunction with date and time functions to add or subtract a specific amount of time from a date or timestamp.
```
SELECT DATE_add(RESCUEDATE, INTERVAL 3 DAY) FROM PETRESCUE; -- adds 3 days to RESCUEDATE

select DATEDIFF(CURRENT_TIMESTAMP,RESCUEDATE) from PETRESCUE; -- calculates the length of time the animals have been rescued
```

Some further uses of functions are shown below:

<img src="https://user-images.githubusercontent.com/13508894/278385308-f2f9e550-265a-4b69-a8f6-b50ab9494f87.png" width="1000" />
