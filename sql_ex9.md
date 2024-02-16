https://www.etutorialspoint.com/index.php/exercise/mysql-exercises
 
+------------------------+------------------------------+----------+----------+
| first_name             | last_name                    | age      | dept     |
+------------------------+------------------------------+----------+----------+
| Mesa                   | Loop                         |  30      |  Acct    |
| Smith                  | Oak                          |  27      |  Devl    | 
| John                   | Jorz                         |  37      |  QA      | 
| Hary                   | Gaga                         |  32      |  QA      | 
+------------------------+------------------------------+----------+----------+

### 1. Write a mysql statement to find the concatenated first_name, last_name where the age of the employee is greater than 30.

select CONCAT(first_name,' ',last_name)
from employee
where age > 30

+-----------+--------------+----------------+
| ITEM_ID   | ITEM         | PRICE          |
+-----------+--------------+----------------+
| 1001      | Book         | 1200           |
| 1002      | Pen          | 930            |
| 1003      | Bag          | 1430           |
| 1004      | Copy         | 1030           |
+-----------+--------------+----------------+

### 2. Write a mysql statement to get item id, item, price of the most expensive item.

select item_id, item, price
from item
where price = (select max(price) from item)


+----+--------------+------------+-----+
| id | name         | department | age |
+----+--------------+------------+-----+
|  1 | Maria Gloria | CS         |  22 |
|  2 | John Smith   | IT         |  23 |
|  3 | Gal Rao      | CS         |  22 |
|  4 | Jakey Smith  | EC         |  24 |
|  5 | Rama Saho    | IT         |  22 |
|  6 | Maria Gaga   | EC         |  23 |
+----+--------------+------------+-----+

### 3. Write a mysql statement to select data of only CS and IT departments.

select *
from table1
where department in ("CS", "IT")

### 4. Write a mysql statement to select data of all departments in descending order by age.

select *
from table1
order by age desc

+----+--------------+------------+------------+
| id | name         | department | birth      |
+----+--------------+------------+------------+
|  1 | Maria Gloria | CS         | 1994-03-12 |
|  2 | John Smith   | IT         | 1993-02-07 |
|  3 | Gal Rao      | CS         | 1992-09-11 |
|  4 | Jakey Smith  | EC         | 1990-08-31 |
|  5 | Rama Saho    | IT         | 1994-12-09 |
|  6 | Maria Gaga   | EC         | 1993-10-09 |
+----+--------------+------------+------------+

### 5. Write a mysql statement to determine the age of each of the students.

select name, DATEDIFF(CURDATE(), BIRTH) as age
from table1

### 6. Write a mysql statement to retrieve name beginning with 'm'.

select name
from table
where name like "M%"

+----+--------------+------------+------------+   
| id | name         | dept_id    | birth      |
+----+--------------+------------+------------+
|  1 | Maria Gloria | 2          | 1994-03-12 |
|  2 | John Smith   | 1          | 1993-02-07 |
|  3 | Gal Rao      | 4          | 1992-09-11 |
|  4 | Jakey Smith  | 2          | 1990-08-31 |
|  5 | Rama Saho    | 1          | 1994-12-09 |
|  6 | Maria Gaga   | 4          | 1993-10-09 |
+----+--------------+------------+------------+

+---------+--------------------------+------------+
| dept_id | dept_name                | dept_block |
+---------+--------------------------+------------+
|       1 | Computer Science         | B-Block    |
|       2 | Information Technology   | C-Block    |
|       3 | Mechanical               | A-Block    |
|       4 | Electronic Communication | D-Block    |
+---------+--------------------------+------------+

### 7. Write a mysql statement to find the name, birth, department name, department block from the given tables.

select table1.name, table1.birth, table2.dept_name, table2.dept_block
from table1
join table2 on table1.dept_id = table2.dept_is

### 8. Write a mysql statement to get name of students containing exactly four characters.

select name
from table1
where name like "____"


