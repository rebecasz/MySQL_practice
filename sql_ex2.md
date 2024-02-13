https://oindrilasen.com/2021/04/sql-interview-practice/ 

CREATE TABLE departments
    ( department_id INTEGER PRIMARY KEY
    , department_name VARCHAR(30)
    , location_id INTEGER
    ) ;

CREATE TABLE employees
   ( employee_id INTEGER
   , first_name VARCHAR(20)
   , last_name VARCHAR(25) 
   , email VARCHAR(25)
   , phone_number VARCHAR(20)
   , hire_date DATE
   , job_id VARCHAR(10)
   , salary INTEGER
   , commission_pct INTEGER
   , manager_id INTEGER
   , department_id INTEGER
   , constraint pk_emp primary key (employee_id) 
   , constraint fk_deptno foreign key (department_id) references departments(department_id)  
   ) ;


   ## Insert insto Departments table
 INSERT INTO departments VALUES ( 20,'Marketing',  180);
 INSERT INTO departments VALUES ( 30,'Purchasing',  1700);
 INSERT INTO departments VALUES ( 40, 'Human Resources',  2400);
 INSERT INTO departments VALUES ( 50, 'Shipping',  1500);
 INSERT INTO departments VALUES ( 60 , 'IT',  1400);
 INSERT INTO departments VALUES ( 70, 'Public Relations',  2700);
 INSERT INTO departments VALUES ( 80 , 'Sales',  2500 );
 INSERT INTO departments VALUES ( 90 , 'Executive',  1700);
 INSERT INTO departments VALUES ( 100 , 'Finance',  1700);
 INSERT INTO departments VALUES ( 110 , 'Accounting',  1700);
 INSERT INTO departments VALUES ( 120 , 'Treasury' ,  1700);
 INSERT INTO departments VALUES ( 130 , 'Corporate Tax' ,  1700 );
 INSERT INTO departments VALUES ( 140, 'Control And Credit' ,  1700);
 INSERT INTO departments VALUES ( 150 , 'Shareholder Services', 1700);
 INSERT INTO departments VALUES ( 160 , 'Benefits', 1700);
 INSERT INTO departments VALUES ( 170 , 'Payroll' , 1700);


## Insert into Employees table
INSERT INTO employees VALUES (100, 'Steven', 'King', 'SKING', '515.123.4567', '1987-06-17' , 'AD_PRES', 24000 , NULL, NULL, 20);
INSERT INTO employees VALUES (101, 'Neena' , 'Kochhar' , 'NKOCHHAR' , '515.123.4568' , '1989-11-21' , 'AD_VP' , 17000 , NULL , 100 , 20);
INSERT INTO employees VALUES (102 , 'Lex' , 'De Haan' , 'LDEHAAN' , '515.123.4569' , '1993-09-12' , 'AD_VP' , 17000 , NULL , 100 , 30);
INSERT INTO employees VALUES (103 , 'Alexander' , 'Hunold' , 'AHUNOLD' , '590.423.4567' , '1990-09-30', 'IT_PROG' , 9000 , NULL , 102 , 60);
INSERT INTO employees VALUES (104 , 'Bruce' , 'Ernst' , 'BERNST' , '590.423.4568' , '1991-05-21',  'IT_PROG' , 6000 , NULL , 103 , 60);
INSERT INTO employees VALUES (105 , 'David' , 'Austin' , 'DAUSTIN' , '590.423.4569' , '1997-06-25',  'IT_PROG' , 4800 , NULL , 103 , 60);
INSERT INTO employees VALUES (106 , 'Valli' , 'Pataballa' , 'VPATABAL' , '590.423.4560' , '1998-02-05',  'IT_PROG' , 4800 , NULL , 103 , 40);
INSERT INTO employees VALUES (107 , 'Diana' , 'Lorentz' , 'DLORENTZ' , '590.423.5567' , '1999-02-09',  'IT_PROG' , 4200 , NULL , 103 , 40);
INSERT INTO employees VALUES (108 , 'Nancy' , 'Greenberg' , 'NGREENBE' , '515.124.4569' , '1994-08-17',  'FI_MGR' , 12000 , NULL , 101 , 100);
INSERT INTO employees VALUES (109 , 'Daniel' , 'Faviet' , 'DFAVIET' , '515.124.4169' , '1994-08-12',  'FI_ACCOUNT' , 9000 , NULL , 108 , 170);
INSERT INTO employees VALUES (110 , 'John' , 'Chen' , 'JCHEN' , '515.124.4269' , '1997-04-09',  'FI_ACCOUNT' , 8200 , NULL , 108 , 170);
INSERT INTO employees VALUES (111 , 'Ismael' , 'Sciarra' , 'ISCIARRA' , '515.124.4369' , '1997-02-01',  'FI_ACCOUNT' , 7700 , NULL , 108 , 160);
INSERT INTO employees VALUES (112 , 'Jose Manuel' , 'Urman' , 'JMURMAN' , '515.124.4469' , '1998-06-03', 'FI_ACCOUNT' , 7800 , NULL , 108 , 150);
INSERT INTO employees VALUES (113 , 'Luis' , 'Popp' , 'LPOPP' , '515.124.4567' , '1999-12-07',  'FI_ACCOUNT' , 6900 , NULL , 108 , 140);
INSERT INTO employees VALUES (114 , 'Den' , 'Raphaely' , 'DRAPHEAL' , '515.127.4561' , '1994-11-08',  'PU_MAN' , 11000 , NULL , 100 , 30);
INSERT INTO employees VALUES (115 , 'Alexander' , 'Khoo' , 'AKHOO' , '515.127.4562' , '1995-05-12',  'PU_CLERK' , 3100 , NULL , 114 , 80);
INSERT INTO employees VALUES (116 , 'Shelli' , 'Baida' , 'SBAIDA' , '515.127.4563' ,'1997-12-13', 'PU_CLERK' , 2900 , NULL , 114 , 70);
INSERT INTO employees VALUES (117 , 'Sigal' , 'Tobias' , 'STOBIAS' , '515.127.4564' , '1997-09-10', 'PU_CLERK' , 2800 , NULL , 114 , 30);
INSERT INTO employees VALUES (118 , 'Guy' , 'Himuro' , 'GHIMURO' , '515.127.4565' , '1998-01-02',  'PU_CLERK' , 2600 , NULL , 114 , 60);
INSERT INTO employees VALUES (119 , 'Karen' , 'Colmenares' , 'KCOLMENA' , '515.127.4566' , '1999-04-08',  'PU_CLERK' , 2500 , NULL , 114 , 130);
INSERT INTO employees VALUES (120 , 'Matthew' , 'Weiss' , 'MWEISS' , '650.123.1234' ,'1996-07-18',  'ST_MAN' , 8000 , NULL , 100 , 50);
INSERT INTO employees VALUES (121 , 'Adam' , 'Fripp' , 'AFRIPP' , '650.123.2234' , '1997-08-09',  'ST_MAN' , 8200 , NULL , 100 , 50);
INSERT INTO employees VALUES (122 , 'Payam' , 'Kaufling' , 'PKAUFLIN' , '650.123.3234' ,'1995-05-01',  'ST_MAN' , 7900 , NULL , 100 , 40);
INSERT INTO employees VALUES (123 , 'Shanta' , 'Vollman' , 'SVOLLMAN' , '650.123.4234' , '1997-10-12',  'ST_MAN' , 6500 , NULL , 100 , 50);
INSERT INTO employees VALUES (124, 'Kevin' , 'Mourgos' , 'KMOURGOS' , '650.123.5234' , '1999-11-12',  'ST_MAN' , 5800 , NULL , 100 , 80);
INSERT INTO employees VALUES (125, 'Julia' , 'Nayer' , 'JNAYER' , '650.124.1214' , '1997-07-02',  'ST_CLERK' , 3200 , NULL , 120 , 50);
INSERT INTO employees VALUES (126, 'Irene' , 'Mikkilineni' , 'IMIKKILI' , '650.124.1224' , '1998-11-12', 'ST_CLERK' , 2700 , NULL , 120 , 50);
INSERT INTO employees VALUES (127, 'James' , 'Landry' , 'JLANDRY' , '650.124.1334' , '1999-01-02' , 'ST_CLERK' , 2400 , NULL , 120 , 90);
INSERT INTO employees VALUES (128, 'Steven' , 'Markle' , 'SMARKLE' , '650.124.1434' , '2000-03-04' , 'ST_CLERK' , 2200 , NULL , 120 , 50);
INSERT INTO employees VALUES (129, 'Laura' , 'Bissot' , 'LBISSOT' , '650.124.5234' ,'1997-09-10' , 'ST_CLERK' , 3300 , NULL , 121 , 50);
INSERT INTO employees VALUES (130, 'Mozhe' , 'Atkinson' , 'MATKINSO' , '650.124.6234' , '1997-10-12' , 'ST_CLERK' , 2800 , NULL , 121 , 110);


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





