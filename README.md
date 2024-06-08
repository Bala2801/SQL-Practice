# SQL-Practice
This is a Practice Project repository.

# In the “salaries” table, retrieve a list with all employees whose salary is not in 60000s

 
 SELECT 
    Emp_No, Salary
FROM
    Salaries
WHERE
    Salary NOT BETWEEN 60000 AND 69999;
    
# In the table “Employee”, choose all the employees whose name is either Denis/ Giri – list all columns


SELECT 
    *
FROM
    Employees
WHERE
    first_name IN ('Denis' , 'Giri')
        OR last_name IN ('Denis' , 'Giri');

# In the table “Employee”, choose all the Female employees whose employee ID is more than 10200 – list all columns and get only 50 results

SELECT
*
FROM
Employees
WHERE
Emp_No > 10200 AND (Gender = 'F')
LIMIT 50;

# In the table “Employee”, choose all the employees whose name is “Shen” & Gender is either Males/ Females – list only first, last names and gender

SELECT
First_Name, Last_name, gender
FROM
Employees
WHERE
first_name IN ('Shen') AND (Gender = 'M' OR 'F')
OR last_name IN ('Shen') AND (Gender = 'M' OR 'F');

# In the table “Employee”, choose all the Female employees whose first name is either Denis/ Elvis – list all columns

SELECT
*
FROM
Employees
WHERE
First_Name IN ('Denis' , 'Elvis') AND (Gender = 'F');

# In the table “Employee”, choose all the employees except for those whose first name is either John/ Mark/ Jacob – list all column and get only 200 results observations

SELECT
*
FROM
Employees
WHERE First_Name NOT IN ('John' 'Mark' 'Jacob')
LIMIT 200;

# In the “Employees” table, retrieve a list with all employees who were born in 1950s

SELECT
*
FROM
employees
WHERE
birth_date LIKE '195%';

# In the “Employees” table, choose all individuals whose first name does not start with “M”

SELECT
*
FROM
employees
WHERE
First_Name NOT LIKE 'M%';

# In the “Titles” table, retrieve the list that has “engineer” in the title

SELECT
*
FROM
Titles
WHERE
Title LIKE '%Engineer%';

# In the “Employees” tables, retrieve a list with all employees whose employee number is written with 5 characters, and start with “100”

SELECT
*
FROM
Employees
WHERE
 Emp_No LIKE '100__';
 
#  In the “Employees” table, retrieve a list with all employees who were born between Jan 1950 to Oct 1956 – select only birth_date, first, last names and gender and get only 500 results

SELECT
birth_date, first_Name, Last_name, gender
FROM
employees
WHERE Birth_Date BETWEEN '1950-01-01' AND '1956-10-31'
LIMIT 500;

#  In the “titles” table, retrieve the list of all the titles unduplicated which has “staff” in the title unduplicated

SELECT DISTINCT *
FROM Titles
WHERE Title = 'Staff';

# In the “titles” table, Count the number of unique titles there are

SELECT COUNT(DISTINCT Title)
FROM Titles;

# From the “salaries” table, retrieve the average salary of first 200 employees sort this in descending order (there are multiple entries for each employee because of the yearly increments) – also, rename the average salary column to “average_sal”

SELECT
Emp_No, AVG(Salary) AS average_sal
FROM Salaries
GROUP BY Emp_No
ORDER BY average_sal DESC
LIMIT 200;

# From the “employees” table, retrieve the number of Female hires on each date of the year 1986 and sort them by hire date – rename the count of female hires column to “number_of_female_hires”

SELECT
Hire_date, COUNT(Emp_No) AS number_of_female_hires
FROM
Employees
WHERE
Hire_date LIKE '1986%'
AND (Gender = 'F')
GROUP BY Hire_Date
ORDER BY Hire_Date ASC;
