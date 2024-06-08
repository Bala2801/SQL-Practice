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

# How scattered is the man-power for each title?

SELECT
T.Title, COUNT(E.emp_No) AS Man_Power
FROM
Employees E
INNER JOIN
Titles T ON E.emp_No = T.emp_No
GROUP BY T.Title;

# How is the salary distribution between titles?

SELECT
T.title, S.salary
FROM
Titles T
INNER JOIN
salaries S ON T.emp_no = S.emp_no
ORDER BY S.salary;

# How scattered is the man-power in each department?

SELECT
de.dept_no, d.dept_name, COUNT(e.emp_no) AS man_power
FROM
departments d
INNER JOIN
dept_emp de ON de.dept_no = d.dept_no
INNER JOIN
employees e ON de.emp_no = e.emp_no
GROUP BY de.dept_no , d.dept_name
ORDER BY de.dept_no;

# Who is the highest and lowest paid employee in the company?

select e.emp_no, e.first_name, e.last_name, s.salary
from employees e
inner join
salaries s on e.emp_no = s.emp_no
where s.salary in (select max(salary) from salaries)
union
select e.emp_no, e.first_name, e.last_name, s.salary
from employees e
inner join
salaries s on e.emp_no = s.emp_no
where s.salary in (select min(salary) from salaries);

# Who are the managers for each department? List their names

SELECT
m.dept_no, d.dept_name, e.first_name, e.last_name
FROM
employees e
INNER JOIN
dept_manager m ON e.emp_no = m.emp_no
INNER JOIN
departments d ON d.dept_no = m.dept_no
order by d.dept_no;

# Using union only command, list all the employees who were hired in 1985, 1989 and 1994 only and sort them by hire dates

select first_name, last_name, emp_no, hire_date
from employees
where hire_date like '1985%'
union
select first_name, last_name, emp_no, hire_date
from employees
where hire_date like '1989%'
union
select first_name, last_name, emp_no, hire_date
from employees
where hire_date like '1994%';

# What is the average salary of those employees who were hired after 01st Jan 1986?

select e.emp_no, e.hire_date, avg(s.salary) as average_salary
from employees e
inner join
salaries s on e.emp_no = s.emp_no
where hire_date > '1986-01-01'
group by e.emp_no;

# Is there gender disparity in the company?

SELECT
d.dept_no,
SUM(gender = 'F') AS no_female_managers,
SUM(gender = 'M') AS no_male_managers
FROM Employees e
inner JOIN dept_manager d ON e.emp_no = d.emp_no
GROUP BY d.dept_no;

# Which department is best paid in the company?

SELECT de.dept_no, d.dept_name,
AVG(s.salary) AS Avg_Salary
FROM salaries s
inner JOIN dept_emp de ON s.emp_no = de.emp_no
inner join departments d on de.dept_no = d.dept_no
GROUP BY de.dept_no
ORDER BY de.dept_no;

# How has the salary changed over the years?

SELECT t.title,
YEAR(s.from_date) AS Year,
AVG(s.salary) AS Avg_Salary
FROM salaries s
inner JOIN titles t ON s.emp_no = t.emp_no
GROUP BY t.title, year
ORDER BY t.title, Year;

# Extract the information about all department managers who were hired between the 1st of January 1990 and the 1st of January 1995.

SELECT
e.first_name, e.last_name, e.hire_date, dm.emp_no
from employees e
JOIN dept_manager dm ON e.emp_no = dm.emp_no
where dm.emp_no in ( select emp_no from employees where hire_date BETWEEN '1990-01-01' and '1995-01-01');

# Extract information of all the “Female Managers”

select
e.emp_no, e.first_name, e.last_name, e.gender, dm.dept_no, dm.from_date, dm.to_date
from employees e
JOIN dept_manager dm on e.emp_no = dm.emp_no
where e.emp_no in (select emp_no from employees where gender='F');

# Select the entire information for all employees whose job title is “Assistant Engineer”.

SELECT *
FROM titles
WHERE emp_no IN (
SELECT emp_no
FROM employees
WHERE Title = 'Assistant Engineer');

# Please get the minimum, maximum and average salary of all the employees. Then, Add another column (“Salary Bracket) to the “Salaries” table with following conditions:
     a) Anyone with the salary less than or equal to 65000 should return “Low salaried” in the new column
     b) Anyone with salary between 65000 and 100,000 should return Medium
     c) Otherwise “High Salaried” in the new column


select emp_no, avg(salary) as avg_salary, max(salary), min(salary),
case when avg(salary) <= 65000 THEN 'Low salaried'
when avg(salary) > 65000 and avg(salary) < 100000 THEN 'medium'
else 'high salaried'
END Salary_Bracket
FROM salaries
group by emp_no;

# Add another column (name the column to your liking) to the “Titles” table with following conditions. Anyone with the title “Engineer” or “Technical” in it should return “Engineer” in the new column, otherwise “Admin” in the new column

SELECT
*,
CASE
WHEN Title LIKE 'Engineer' or 'Technical' Then 'Engineer'
ELSE 'Admin'
END NEW_Ttitle
FROM
Titles;

# Add another column to the “employees” table (call it hire_quarter), that returns the Quarter number for the respective hire month. For eg, if someone joined in either Jan, Feb or March, this column should return the value “Q1”

SELECT *,
CASE
WHEN MONTH(Hire_date) BETWEEN 1 And 3 THEN 'Q1'
WHEN MONTH(Hire_date) BETWEEN 4 And 6 THEN 'Q2'
WHEN MONTH(Hire_date) BETWEEN 7 And 9 THEN 'Q3'
WHEN MONTH(Hire_date) BETWEEN 10 And 12 THEN 'Q4'
END Hire_quarter
FROM Employees;

# Using “Case When”, in the “dept_emp” table, please add the respective department name

select *,
case
When dept_no='d001' Then 'Marketing'
When dept_no='d002' Then 'Finance'
When dept_no='d003' Then 'Human resources'
When dept_no='d004' Then 'Production'
When dept_no='d005' Then 'Development'
When dept_no='d006' Then 'Quality Management'
When dept_no='d007' Then 'Sales'
When dept_no='d008' Then 'Research'
When dept_no='d009' Then 'Customer Service'
End as department_name
from dept_emp;

# 


# 
