https://www.hackerrank.com/challenges/

city table:

id number
name varchar(17)
countrycode varchar(3)
district varchar(20)
population number

### 1. Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.

select * 
from city
where population >100000 and countrycode = "USA"

### 2. Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.

select name 
from city
where population > 120000 and countrycode = "USA"

### 3. Query all columns (attributes) for every row in the CITY table.

select *
from city

### 4. Query all columns for a city in CITY with the ID 1661.

select * from city
where id = 1661

### 5. Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.

select *
from city 
where countrycode="JPN"

### 6. Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.

select name
from city
where countrycode = "JPN"

### 7. Query a list of CITY and STATE from the STATION table.

select city, state 
from station

### 8. Query a count of the number of cities in CITY having a Population larger than 100.000 .

select count(id)
from city
where population> 100000

### 9. Query the total population of all cities in CITY where District is California.

select sum(population) 
from city
where district = "California"

### 10. Query the average population of all cities in CITY where District is California.

select avg(population)
from city
where district = "California"

### 11. Query the average population for all cities in CITY, rounded down to the nearest integer.

select round(avg(population),0)
from city

### 12. Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.

SELECT SUM(population)
FROM city
WHERE countrycode = 'JPN';

### 13. Query the difference between the maximum and minimum populations in CITY.

select max(population) - min(population)
from city;
