https://oindrilasen.com/2021/04/sql-interview-practice/ 

### 1. Select employees first name, last name, job_id and salary whose first name starts with alphabet S
 
 SELECT first_name, last_name, job_id, salary
 FROM sys.employees
 WHERE first_name like "S%"


### 2. Write a query to select employee with the highest salary

select first_name , last_name
from sys.employees
order by salary desc
limit 1 

select first_name , last_name, max(salary)
from sys.employees

### 3. Select employee with the second highest salary

select first_name, last_name, salary
from sys.employees
order by salary desc
limit 1 offset 1

### 4. Fetch employees with 2nd or 3rd highest salary

select first_name, last_name, salary
from sys.employees
order by salary desc
limit 2 offset 1

### 5. Write a query to select employees and their corresponding managers and their salaries

SELECT 
    e1.first_name AS employee_first_name,
    e1.last_name AS employee_last_name,
    e1.salary AS employee_salary,
    e2.first_name AS manager_first_name,
    e2.last_name AS manager_last_name,
    e2.salary AS manager_salary
FROM 
    sys.employees e1
JOIN 
    sys.employees e2 ON e1.manager_id = e2.employee_id;

### 6. Write a query to show count of employees under each manager in descending order


SELECT 
    e2.employee_id AS manager_id,
    COUNT(e1.employee_id) AS employee_count
FROM sys.employees e1
JOIN sys.employees e2 ON e1.manager_id = e2.employee_id
GROUP BY e2.employee_id
ORDER BY employee_count DESC;

### 7. Find the count of employees in each department

SELECT count(employees.employee_id) , departments.department_id, departments.department_name
FROM sys.employees
join sys.departments on departments.department_id=employees.department_id
group by department_id;



### 8. Get the count of employees hired year wise

SELECT count(concat(first_name , last_name)) , year(hire_date)
FROM sys.employees
group by year(hire_date);


### 9. Find the salary range of employees

select min(salary) as "min_salary" , max(salary) as "max salary"
from sys.employees

### 10. Write a query to divide people into three groups based on their salaries

select first_name, last_name, salary,
case
	when salary between 2000 and 6000 then "low"
    when salary between 6001 and 15000 then "medium"
    when salary > 15000 then "high"
end as salary_value    
from sys.employees

### 11. Select the employees whose first_name contains “an”

select first_name
from sys.employees
where first_name like "%an%"

### 12. Select employee first name and the corresponding phone number in the format
### (_ _ _)-(_ _ _)-(_ _ _ _)

select first_name, replace(phone_number, ".", "-")
from sys.employees

### 13. Find the employees who joined in August, 1994.

select first_name, last_name
from sys.employees
where year(hire_date)=1994 and month(hire_date) = 8

### 14. Write an SQL query to display employees who earn more than the average salary in that company

select 
 emp.first_name, 
 emp.last_name,
 dept.department_name department,
 dept.department_id,
 emp.salary
 from sys.departments dept
 JOIN sys.employees emp on dept.department_id = emp.department_id
 where emp.salary > (select avg(salary) from sys.employees)
 order by dept.department_id;

### 15. Find the maximum salary from each department.

select departments.department_name, max(employees.salary)
from sys.departments
join sys.employees on departments.department_id = employees.department_id
group by departments.department_name

### 16. Write a SQL query to display the 5 least earning employees

select first_name, last_name, salary
from sys.employees
order by salary asc 
limit 5

### 17. Find the employees hired in the 80s

select first_name, last_name, year(hire_date)
from sys.employees
where year(hire_date) between 1980 and 1989


### 18. Display the employees first name and the name in reverse order

SELECT  first_name, REVERSE(first_name) AS reversed_name
FROM  sys.employees;

### 19. Find the employees who joined the company after 15th of the month

select first_name, last_name, day(hire_date)
from sys.employees
where day(hire_date) >=15


### 20. Display the managers and the reporting employees who work in different departments

SELECT 
    CONCAT(mgr.first_name, ' ', mgr.last_name) AS Manager,
    CONCAT(emp.first_name, ' ', emp.last_name) AS Employee
FROM 
    sys.employees AS emp
JOIN 
    sys.employees AS mgr ON emp.manager_id = mgr.employee_id
WHERE 
    emp.department_id != mgr.department_id
ORDER BY 
    Manager;





