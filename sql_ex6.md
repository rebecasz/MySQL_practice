https://www.hackerrank.com/challenges/

employee table:

employee_id integer
name string
months integer
salary integer

### 1. Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.

select name 
from employee
order by name asc

### 2. Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than 2000$ per month who have been employees for less than 10 months. Sort your result by ascending employee_id.

select name
from employee
where salary > 2000 and months< 10
order by employee_id


### 3. We define an employee's total earnings to be their monthly salary x months worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as 2 space-separated integers.

SELECT 
    MAX(months * salary) AS max_earnings,
    COUNT(*) AS employee_count
FROM 
    Employee
WHERE 
    months * salary = (SELECT MAX(months * salary) FROM Employee);

