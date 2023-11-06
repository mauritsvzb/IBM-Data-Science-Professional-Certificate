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
| _______________ | ______ | ____| ____ |
| George Washington Carver Military Academy High School	| Riverdale |	91.60%	| 98 |
| George Washington Carver Primary School	| Riverdale |	90.90%	98 |
| Ira F Aldridge Elementary School |	Riverdale	| 92.90% |	98 |
| William E B Dubois Elementary School |	Riverdale	| 93.30%	| 98 |
