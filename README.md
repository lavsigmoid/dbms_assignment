# RDBMS_ASSIGNMENT

## Query Questions


### 1. Create a database named employee, then import data_science_team.csv proj_table.csv and emp_record_table.csv into the employee database from the given resources.
<img width="213" alt="Screenshot 2023-02-23 at 4 55 08 PM" src="https://user-images.githubusercontent.com/122512155/220893231-76f55a7a-0e34-408f-ace2-568004cb1b1a.png">


### 2. Create an ER diagram for the given employee database.
![220892458-4b192ffc-a24d-43b2-b3c0-4bd2c01909e2](https://user-images.githubusercontent.com/122512155/221576860-cd727741-eabe-4d53-a6b9-304dad0eb527.jpg)


### 3. Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, and make a list of employees and details of their department.

```bash
SELECT EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT
FROM emp_record_table;
```

<img width="1222" alt="Screenshot 2023-02-23 at 4 57 50 PM" src="https://user-images.githubusercontent.com/122512155/220893538-b6a7aa08-ff9f-4e84-b38d-2c1f3d8bc36b.png">

### 4. Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT, and EMP_RATING if the EMP_RATING is:<br>
● less than two<br>
● greater than four<br>
● between two and four<br>

```bash
SELECT EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT, EMP_RATING
FROM emp_record_table
WHERE EMP_RATING<2;
```
<img width="1217" alt="Screenshot 2023-02-23 at 4 59 04 PM" src="https://user-images.githubusercontent.com/122512155/220893842-4de4bcc8-d00e-4b8b-af58-736541fe44bf.png">

```bash
SELECT EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT, EMP_RATING
FROM emp_record_table
WHERE EMP_RATING BETWEEN 2 AND 4;
```
<img width="1217" alt="Screenshot 2023-02-23 at 5 00 20 PM" src="https://user-images.githubusercontent.com/122512155/220894047-1dc3acf7-6ee4-4a3a-ac69-f2977b4cb849.png">

```bash
SELECT EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT, EMP_RATING
FROM emp_record_table
WHERE EMP_RATING>4;
```
<img width="1218" alt="Screenshot 2023-02-23 at 5 01 13 PM" src="https://user-images.githubusercontent.com/122512155/220894168-480a35ce-4434-4e44-b8a4-c2ccc99c8dcd.png">

### 5. Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and then give the resultant column alias as NAME.

```bash
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME) AS NAME 
FROM emp_record_table
WHERE DEPT='FINANCE';
```
<img width="1218" alt="Screenshot 2023-02-23 at 5 01 13 PM" src="https://user-images.githubusercontent.com/122512155/220894544-4fd03b3b-758e-4430-8bfe-0b15bb4ee160.png">


### 6. Write a query to list only those employees who have someone reporting to them. Also, show the number of reporters (including the President).

 ```bash
 SELECT CONCAT(emp.FIRST_NAME, ' ', EMP.LAST_NAME) AS NAME FROM (SELECT  COUNT(W.MANAGER_ID) CNT, MANAGER_ID
FROM emp_record_table W
GROUP BY W.MANAGER_ID
HAVING CNT<>0) A
join emp_record_table emp on emp.emp_id=a.manager_id;
 ```
 <img width="1217" alt="Screenshot 2023-02-23 at 5 05 07 PM" src="https://user-images.githubusercontent.com/122512155/220894923-5ac1bfe8-ea81-4216-af6f-cf4152e12ff8.png">

 
### 7. Write a query to list down all the employees from the healthcare and finance departments using union. Take data from the employee record table.

```bash
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME)
FROM emp_record_table
WHERE DEPT='HEALTHCARE'
UNION
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME)
FROM emp_record_table
WHERE DEPT='FINANCE';
```
<img width="1217" alt="Screenshot 2023-02-23 at 5 06 05 PM" src="https://user-images.githubusercontent.com/122512155/220895122-9bed56be-5ff5-418e-a2b0-87dbb4254987.png">



### 8. Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPARTMENT, and EMP_RATING grouped by dept. Also include the respective employee rating along with the max emp rating for the department.

```bash
SELECT EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPT, EMP_RATING, MAX(EMP_RATING) OVER(PARTITION BY DEPT) AS MAX_RATING
FROM emp_record_table;
```
<img width="1219" alt="Screenshot 2023-02-23 at 5 07 01 PM" src="https://user-images.githubusercontent.com/122512155/220895292-b8b05f29-cd09-44e8-80ca-04347146be5a.png">


### 9. Write a query to calculate the minimum and the maximum salary of the employees in each role. Take data from the employee record table.

```bash
SELECT DISTINCT ROLE, MIN(SALARY) OVER(PARTITION BY ROLE) AS MIN_SAL, MIN(SALARY) OVER(PARTITION BY ROLE) AS MAX_SAL
FROM emp_record_table;
```
<img width="1218" alt="Screenshot 2023-02-23 at 5 07 54 PM" src="https://user-images.githubusercontent.com/122512155/220895440-63559233-92ca-499c-911f-4791ff5227a9.png">


### 10. Write a query to assign ranks to each employee based on their experience. Take data from the employee record table.

```bash
SELECT *, row_NUMBER() OVER(ORDER BY EXP DESC) AS RANKING
FROM emp_record_table;
```
<img width="1217" alt="Screenshot 2023-02-23 at 5 08 49 PM" src="https://user-images.githubusercontent.com/122512155/220895681-b70d59da-4215-4359-99e6-d9a7ebb53025.png">


### 11. Write a query to create a view that displays employees in various countries whose salary is more than six thousand. Take data from the employee record table.

```bash
CREATE VIEW EMP_RECORD AS
SELECT FIRST_NAME, COUNTRY
FROM emp_record_table
WHERE SALARY>6000;
```
<img width="1216" alt="Screenshot 2023-02-23 at 5 11 49 PM" src="https://user-images.githubusercontent.com/122512155/220896241-9f9d9fd2-8f80-4f31-8cc5-6b79151f5042.png">


### 12. Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.

```bash
SELECT EMP_ID, FIRST_NAME, ROLE, EXP
FROM (SELECT *
FROM emp_record_table
where exp>10) A;
```
<img width="1216" alt="Screenshot 2023-02-23 at 5 11 49 PM" src="https://user-images.githubusercontent.com/122512155/220896470-c2da3c52-5847-4764-a0a9-416a85b42855.png">



### 13. Write a query to create a stored procedure to retrieve the details of the employees whose experience is more than three years. Take data from the employee record table.

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
<img width="1216" alt="Screenshot 2023-02-23 at 5 11 49 PM" src="https://user-images.githubusercontent.com/122512155/220896871-2ce23eb0-5d03-41e1-a271-04a3ceb48470.png">



### 14. Write a query using stored functions in the project table to check whether the job profile assigned to each employee in the data science team matches the organization’s set standard.
The standard being:
For an employee with experience less than or equal to 2 years assign 'JUNIOR DATA SCIENTIST', For an employee with the experience of 2 to 5 years assign 'ASSOCIATE DATA SCIENTIST',
For an employee with the experience of 5 to 10 years assign 'SENIOR DATA SCIENTIST',
For an employee with the experience of 10 to 12 years assign 'LEAD DATA SCIENTIST',
For an employee with the experience of 12 to 16 years assign 'MANAGER'.

```bash
DELIMITER $$
CREATE FUNCTION get_job_profile(experience INT, role VARCHAR(30))
RETURNS VARCHAR(50)
DETERMINISTIC

BEGIN
	DECLARE job_profile varchar(50);
    DECLARE flag varchar(30);
	IF experience<=2 THEN
		SET job_profile='JUNIOR DATA SCIENTIST';
	ELSEIF experience between 2 AND 5 THEN
		SET job_profile='ASSOCIATE DATA SCIENTIST';
	ELSEIF experience between 5 AND 10 THEN
		SET job_profile='SENIOR DATA SCIENTIST';
	ELSEIF experience between 10 AND 12 THEN
		SET job_profile='LEAD DATA SCIENTIST';
	ELSEIF experience between 12 AND 16 THEN
		SET job_profile='MANAGER';
	END IF;
	
    IF job_profile=role THEN
		SET flag='YES';
	ELSE 
		SET flag='NO';
	END IF;
    
    RETURN flag;
END $$ 
DELIMITER ;


SELECT EMP_ID, FIRST_NAME, EXP, ROLE, get_job_profile(EXP, ROLE) AS CHECK_PROFILE
FROM data_science_team;
```
<img width="1220" alt="Screenshot 2023-02-27 at 6 55 05 PM" src="https://user-images.githubusercontent.com/122512155/221575373-d4c982c7-fac6-4f03-9cda-0f87772518ef.png">



### 15. Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.

```bash
CREATE INDEX idx_first_name
ON emp_record_table(FIRST_NAME(20));
SELECT * FROM emp_record_table
WHERE FIRST_NAME='Eric';
```
<img width="1218" alt="Screenshot 2023-02-26 at 10 27 52 AM" src="https://user-images.githubusercontent.com/122512155/221393164-f3d02cb9-0ce6-4a6a-8e54-9f682adec6b8.png">


### 16. Write a query to calculate the bonus for all the employees, based on their ratings and salaries (Use the formula: 5% of salary * employee rating).

```
SELECT EMP_ID, CONCAT(FIRST_NAME, ' ', LAST_NAME) AS NAME, SALARY, ROUND(((SALARY*5)/100)*EMP_RATING) AS BONUS
FROM emp_record_table;
```
<img width="1217" alt="Screenshot 2023-02-23 at 5 17 03 PM" src="https://user-images.githubusercontent.com/122512155/220897282-5671975e-8b1a-4077-8abc-8a7355a3f25c.png">



### 17. Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.

```bash
SELECT  DISTINCT COUNTRY, AVG(SALARY) OVER(PARTITION BY COUNTRY) AS COUNTRY_AVG, CONTINENT, AVG(SALARY) OVER(PARTITION BY CONTINENT) AS CONTINENT_AVG
FROM emp_record_table;
```
<img width="1222" alt="Screenshot 2023-02-23 at 5 18 20 PM" src="https://user-images.githubusercontent.com/122512155/220897500-aab7b3a6-b74c-4cae-a8fb-536bca1cb3d5.png">

