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
| HR585012	| CRIMINAL TRESPASS	| TO LAND	SCHOOL PUBLIC GROUNDS	| Ashburn |
