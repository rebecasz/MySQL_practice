employees table:

id integer
name string 
salary integer

### 1. Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's 0 key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeros removed), and the actual average salary.

Write a query calculating the amount of error (i.e.:  average monthly salaries), and round it up to the next integer.

SELECT CEIL(AVG(salary) - AVG(CAST(REPLACE(salary, '0', '') )))
FROM employees;

#### REPLACE(salary, '0', ''): This function replaces all occurrences of '0' in the salary column with an empty string. It is used to remove zeros from the salary.