# Honors Peer-graded Assignment: Advanced SQL for Data Engineers

## Exercise 1, Question 1
Write and execute a SQL query to list the school names, community names, and average attendance for communities with a hardship index of 98

```sql
SELECT CPS.NAME_OF_SCHOOL, CPS.COMMUNITY_AREA_NAME, CPS.AVERAGE_STUDENT_ATTENDANCE, CD.HARDSHIP_INDEX 
FROM CENSUS_DATA CD
INNER JOIN CHICAGO_PUBLIC_SCHOOLS CPS
ON CPS.COMMUNITY_AREA_NUMBER = CD.COMMUNITY_AREA_NUMBER
WHERE CD.HARDSHIP_INDEX == 98;
```

### output:

| NAME_OF_SCHOOL |	COMMUNITY_AREA_NAME	| AVERAGE_STUDENT_ATTENDANCE | HARDSHIP_INDEX
| --- |  --- | --- | --- |
| George Washington Carver Military Academy High School	| Riverdale |	91.60%	| 98 |
| George Washington Carver Primary School	| Riverdale |	90.90% |	98 |
| Ira F Aldridge Elementary School |	Riverdale	| 92.90% |	98 |
| William E B Dubois Elementary School |	Riverdale	| 93.30%	| 98 |

## Exercise 1, Question 2
Write and execute a SQL query to list all crimes that took place at a school. Include case number, crime type, and community name.

```sql
SELECT C.CASE_NUMBER, C.PRIMARY_TYPE, C.DESCRIPTION, 
	   C.LOCATION_DESCRIPTION, CD.COMMUNITY_AREA_NAME 
FROM CHICAGO_CRIME_DATA C
INNER JOIN CENSUS_DATA SD
ON CD.COMMUNITY_AREA_NUMBER = C.COMMUNITY_AREA_NUMBER
WHERE C.LOCATION_DESCRIPTION LIKE '%SCHOOL%'
```

| CASE_NUMBER |	PRIMARY_TYPE |	DESCRIPTION	| LOCATION_DESCRIPTION	| COMMUNITY_AREA_NAME |
| --- | --- | --- | --- | ---| 
| HL353697	| BATTERY	| SIMPLE	SCHOOL PUBLIC GROUNDS	| South Shore |
| HL725506	| BATTERY	| PRO EMP HANDS NO/MIN INJURY	| SCHOOL PUBLIC BUILDING	| Lincoln Square |
| HP716225	| BATTERY	| SIMPLE	| SCHOOL PUBLIC BUILDING	| Douglas |
| HH639427	| BATTERY	| SIMPLE	| SCHOOL PUBLIC BUILDING	| Austin |
| JA460432	| BATTERY	| SIMPLE	| SCHOOL PUBLIC GROUNDS	| Ashburn |
| HS200939	| CRIMINAL DAMAGE	| TO VEHICLE	| SCHOOL PUBLIC GROUNDS	| Austin |
| HK577020	| NARCOTICS	| POSS: HEROIN(WHITE)	| SCHOOL PUBLIC GROUNDS	| Rogers Park |
| HS305355	| NARCOTICS	| MANU/DEL:CANNABIS 10GM OR LESS	| SCHOOL PUBLIC BUILDING	| Brighton Park |
| HT315369	| ASSAULT	| PRO EMP HANDS NO/MIN INJURY	SCHOOL | PUBLIC GROUNDS	East | Garfield Park |
| HR585012	| CRIMINAL TRESPASS	| TO LAND | SCHOOL PUBLIC GROUNDS	| Ashburn |

## Exercise 2, Question 1

Write and execute a SQL statement that returns just the school name and leaders' icon from the view

```sql
CREATE VIEW School_Icon
AS SELECT NAME_OF_SCHOOL AS "Name", Leaders_Icon AS "Icon"
FROM CHICAGO_PUBLIC_SCHOOLS;

SELECT * FROM School_Icon;
```

### Output

| Name	| Icon
| --- | --- |
| Abraham Lincoln Elementary School	| Weak
| Adam Clayton Powell Paideia Community Academy Elementary School	| Weak
| Adlai E Stevenson Elementary School	| Weak
| Agustin Lara Elementary Academy	| Weak
| Air Force Academy High School	| Weak
| Albany Park Multicultural Academy	| Weak
| Albert G Lane Technical High School	| Weak
| Albert R Sabin Elementary Magnet School	| Weak
| Alcott High School for the Humanities	| Weak
| Alessandro Volta Elementary School	| Weak
| Alexander Graham Bell Elementary School	| Weak
| Alexander Graham Elementary School	| Weak
.....	| .....

## Exercise 3, Question 1

Write the structure of a query to create or replace a stored procedure called `UPDATE_LEADERS_SCORE` that takes a `in_School_ID` parameter as an integer and a `in_Leader_Score` parameter as an integer. 

```sql
DELIMITER @
CREATE PROCEDURE UPDATE_LEADERS_SCORE (
	IN in_School_ID INTEGER, IN in_Leader_Score INTEGER)
BEGIN

END @

DELIMITER ;
```

## Exercise 3, Question 2
Inside your stored procedure, write a SQL statement to update the `Leaders_Score` in `CHICAGO_PUBLIC_SCHOOLS` table for the school indentified by `in_School_ID` to the value in the `in_Leader_Score` parameter.

* Reference: SQL Cheat Sheet: Views, Stored Procedures and Transactions

```sql
DELIMITER @
CREATE PROCEDURE UPDATE_LEADERS_SCORE (
	IN in_School_ID INTEGER, IN in_Leader_Score INTEGER)
BEGIN
	UPDATE chicago_public_schools
	SET Leaders_Score = in_Leader_Score
	WHERE School_ID = in_School_ID

END @

DELIMITER ;
```

## Exercise 3, Question 3
Inside your stored procedure, write a SQL IF statement to update the Leaders_Icon field in the CHICAGO_PUBLIC_SCHOOLS table for the school identified by in_School_ID using the following information.

| Score lower limit | Score upper limit |  Icon
| --- | ---| --- |
| 80	| 99 | 	Very strong
60 | 	79 | 	Strong
40 | 	59 | 	Average
20 | 	39 | 	Weak
0 | 	19 | 	Very weak
* Note: Since REORG TABLE is a DB2 command line, there fore CALL SYSPROC.ADMIN_CMD() has to be used.
* Reference: [https://www.ibm.com/docs/en/db2/11.5?topic=commands-reorg-table-command-using-admin-cmd](https://www.ibm.com/docs/en/db2/11.5?topic=commands-reorg-table-command-using-admin-cmd)

```sql
DELIMITER @
CREATE PROCEDURE UPDATE_LEADERS_SCORE (
	IN in_School_ID INTEGER, IN in_Leader_Score INTEGER)
BEGIN
	IF in_Leader_Score BETWEEN 80 AND 99 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Very Strong'
			WHERE School_ID = in_School_ID;
		ELSEIF in_Leader_Score BETWEEN 60 AND 79 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Strong'
			WHERE School_ID = in_School_ID;
		ELSEIF in_Leader_Score BETWEEN 40 AND 59 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Average'
			WHERE School_ID = in_School_ID;		
		ELSEIF in_Leader_Score BETWEEN 20 AND 39 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Weak'
			WHERE School_ID = in_School_ID;	
		ELSE 	
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Very Weak'
			WHERE School_ID = in_School_ID;	
		END IF;

END @

DELIMITER ;
```

## Exercise 4, Question 1
Update your stored procedure definition. Add  generic `ELSE` clause to the IF statement that rolls back the current score if the score did not fit any of the preceding categories.

```sql
DELIMITER @
CREATE PROCEDURE UPDATE_LEADERS_SCORE (
	IN in_School_ID INTEGER, IN in_Leader_Score INTEGER)
BEGIN
	IF in_Leader_Score BETWEEN 80 AND 99 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Very Strong'
			WHERE School_ID = in_School_ID;
		ELSEIF in_Leader_Score BETWEEN 60 AND 79 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Strong'
			WHERE School_ID = in_School_ID;
		ELSEIF in_Leader_Score BETWEEN 40 AND 59 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Average'
			WHERE School_ID = in_School_ID;		
		ELSEIF in_Leader_Score BETWEEN 20 AND 39 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Weak'
			WHERE School_ID = in_School_ID;	
		ELSEIF 	in_Leader_Score BETWEEN 0 AND 19 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Very Weak'
			WHERE School_ID = in_School_ID;	
		ELSE
			ROLLBACK;
		END IF;

END @

DELIMITER ;
```

## Exercise 4, Question 2

Update your stored procedure definition again. Add a statement to commit the current unit of work at the end of the procedure. 

```sql
DELIMITER @
CREATE PROCEDURE UPDATE_LEADERS_SCORE (
	IN in_School_ID INTEGER, IN in_Leader_Score INTEGER)
BEGIN
	IF in_Leader_Score BETWEEN 80 AND 99 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Very Strong'
			WHERE School_ID = in_School_ID;
		ELSEIF in_Leader_Score BETWEEN 60 AND 79 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Strong'
			WHERE School_ID = in_School_ID;
		ELSEIF in_Leader_Score BETWEEN 40 AND 59 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Average'
			WHERE School_ID = in_School_ID;		
		ELSEIF in_Leader_Score BETWEEN 20 AND 39 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Weak'
			WHERE School_ID = in_School_ID;	
		ELSEIF 	in_Leader_Score BETWEEN 0 AND 19 THEN
			UPDATE chicago_public_schools 
			SET Leaders_Score = in_Leader_Score, Leaders_Icon = 'Very Weak'
			WHERE School_ID = in_School_ID;	
		ELSE
			ROLLBACK;
		END IF;

		COMMIT;

END @

DELIMITER ;
```
