# RDBMS_ASSIGNMENT

## Query Questions

2. Create an ER diagram for the given employee database.
![Image 23-02-23 at 4 48 PM](https://user-images.githubusercontent.com/122512155/220892458-4b192ffc-a24d-43b2-b3c0-4bd2c01909e2.jpg)


3. Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, and make a list of employees and details of their department.

```bash
SELECT EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT
FROM emp_record_table;
```
4. Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT, and EMP_RATING if the EMP_RATING is:<br>
● less than two<br>
● greater than four<br>
● between two and four<br>

```bash
SELECT EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT, EMP_RATING
FROM emp_record_table
WHERE EMP_RATING<2;

SELECT EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT, EMP_RATING
FROM emp_record_table
WHERE EMP_RATING BETWEEN 2 AND 4;

SELECT EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT, EMP_RATING
FROM emp_record_table
WHERE EMP_RATING>4;
```
5. Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and then give the resultant column alias as NAME.

```bash
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME) AS NAME 
FROM emp_record_table
WHERE DEPT='FINANCE';
```

6. Write a query to list only those employees who have someone reporting to them. Also, show the number of reporters (including the President).

 ```bash
 SELECT CONCAT(emp.FIRST_NAME, ' ', EMP.LAST_NAME) FROM (SELECT  COUNT(W.MANAGER_ID) CNT, MANAGER_ID
FROM emp_record_table W
GROUP BY W.MANAGER_ID
HAVING CNT<>0) A
join emp_record_table emp on emp.emp_id=a.manager_id;
 ```
 
 7. Write a query to list down all the employees from the healthcare and finance departments using union. Take data from the employee record table.

```bash
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME)
FROM emp_record_table
WHERE DEPT='HEALTHCARE'
UNION
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME)
FROM emp_record_table
WHERE DEPT='FINANCE';
```


8. Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPARTMENT, and EMP_RATING grouped by dept. Also include the respective employee rating along with the max emp rating for the department.

```bash
SELECT EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPT, EMP_RATING, MAX(EMP_RATING) OVER(PARTITION BY DEPT) AS MAX_RATING
FROM emp_record_table;
```

9. Write a query to calculate the minimum and the maximum salary of the employees in each role. Take data from the employee record table.

```bash
SELECT DISTINCT ROLE, MIN(SALARY) OVER(PARTITION BY ROLE) AS MIN_SAL, MIN(SALARY) OVER(PARTITION BY ROLE) AS MAX_SAL
FROM emp_record_table;
```

10. Write a query to assign ranks to each employee based on their experience. Take data from the employee record table.

```bash
SELECT *, row_NUMBER() OVER(ORDER BY EXP DESC) AS RANKING
FROM emp_record_table;
```

11. Write a query to create a view that displays employees in various countries whose salary is more than six thousand. Take data from the employee record table.

```bash
CREATE VIEW EMP_RECORD AS
SELECT FIRST_NAME, COUNTRY
FROM emp_record_table
WHERE SALARY>6000;
```

12. Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.

```bash
SELECT EMP_ID, FIRST_NAME, ROLE, EXP
FROM (SELECT *
FROM emp_record_table
where exp>10) A;
```

13. Write a query to create a stored procedure to retrieve the details of the employees whose experience is more than three years. Take data from the employee record table.

```bash
DELIMITER $$
CREATE PROCEDURE EMP_DET()
BEGIN
	SELECT * FROM emp_record_table
    WHERE EXP>3;
END $$
DELIMITER ;

CALL EMP_DET();
```

14. Write a query using stored functions in the project table to check whether the job profile assigned to each employee in the data science team matches the organization’s set standard.
The standard being:
For an employee with experience less than or equal to 2 years assign 'JUNIOR DATA SCIENTIST', For an employee with the experience of 2 to 5 years assign 'ASSOCIATE DATA SCIENTIST',
For an employee with the experience of 5 to 10 years assign 'SENIOR DATA SCIENTIST',
For an employee with the experience of 10 to 12 years assign 'LEAD DATA SCIENTIST',
For an employee with the experience of 12 to 16 years assign 'MANAGER'.

```bash

```

15. Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.

```bash

```

16. Write a query to calculate the bonus for all the employees, based on their ratings and salaries (Use the formula: 5% of salary * employee rating).

```
SELECT EMP_ID, CONCAT(FIRST_NAME, ' ', LAST_NAME) AS NAME, SALARY, ROUND(((SALARY*5)/100)*EMP_RATING) AS BONUS
FROM emp_record_table;
```


17. Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.

```bash
SELECT  DISTINCT COUNTRY, AVG(SALARY) OVER(PARTITION BY COUNTRY) AS COUNTRY_AVG, CONTINENT, AVG(SALARY) OVER(PARTITION BY CONTINENT) AS CONTINENT_AVG
FROM emp_record_table;
```
