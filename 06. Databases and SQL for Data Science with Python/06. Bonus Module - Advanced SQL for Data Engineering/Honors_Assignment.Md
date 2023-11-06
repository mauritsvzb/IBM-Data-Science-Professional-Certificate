# Honors Peer-graded Assignment: Advanced SQL for Data Engineers

## Exercise 1, Question 1
Write and execute a SQL query to list the school names, community names, and average attendance for communities with a hardship index of 98

```sql
SELECT CPS.NAME_OF_SCHOOL, CPS.COMMUNITY_AREA_NAME, CPS.AVERAGE_STUDENT_ATTENDANCE, CSD.HARDSHIP_INDEX
FROM CHICAGO_PUBLIC_SCHOOLS CSD LEFT JOIN CHICAGO_PUBLIC_SCHOOLS CPS 
ON CPS.COMMUNITY_AREA_NUMBER = CSD.COMMUNITY_AREA_NUMBER
WHERE CENSUS_DATA.HARDSHIP_INDEX == 98;
```

