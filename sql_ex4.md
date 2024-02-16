https://www.hackerrank.com/challenges/


station table:

id number
city varchar2(21)
state varchar(2)
lat_n number
long_w number 



### 1. Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.

select distinct(city)
from station 
where id % 2 = 0 

### 2. Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

select count(*) - count(distinct(city))
from station

### 3. Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

SELECT city, LENGTH(city) AS city_length
FROM station
ORDER BY city_length ASC, city
LIMIT 1; -- Shortest city

SELECT city, LENGTH(city) AS city_length
FROM station
ORDER BY city_length DESC, city
LIMIT 1; -- Longest city

### 4. Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

SELECT DISTINCT city
FROM station
WHERE city LIKE 'a%' OR city LIKE 'e%' OR city LIKE 'i%' OR city LIKE 'o%' OR city LIKE 'u%';


SELECT DISTINCT city
FROM station
WHERE LOWER(SUBSTRING(city, 1, 1)) IN ('a', 'e', 'i', 'o', 'u');

### 5. Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.

SELECT DISTINCT city
FROM station
WHERE city LIKE '%a' OR city LIKE '%e' OR city LIKE '%i' OR city LIKE '%o' OR city LIKE '%u';

SELECT DISTINCT city
FROM station
WHERE LOWER(SUBSTRING(city, -1, 1)) IN ('a', 'e', 'i', 'o', 'u');

### 6. Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.

SELECT DISTINCT city
FROM station
WHERE LOWER(SUBSTRING(city, 1, 1)) IN ('a', 'e', 'i', 'o', 'u')
  AND LOWER(SUBSTRING(city, -1, 1)) IN ('a', 'e', 'i', 'o', 'u');


### 7. Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.

SELECT DISTINCT city
FROM station
WHERE LOWER(SUBSTRING(city, 1, 1)) not IN ('a', 'e', 'i', 'o', 'u');

### 8. Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.

SELECT DISTINCT city
FROM station
WHERE LOWER(SUBSTRING(city, -1, 1)) not IN ('a', 'e', 'i', 'o', 'u');

### 9. Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

SELECT DISTINCT city
FROM station
WHERE LOWER(SUBSTRING(city, 1, 1)) not IN ('a', 'e', 'i', 'o', 'u')
  or LOWER(SUBSTRING(city, -1, 1)) not IN ('a', 'e', 'i', 'o', 'u');

### 10. Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

SELECT DISTINCT city
FROM station
WHERE LOWER(SUBSTRING(city, 1, 1)) not IN ('a', 'e', 'i', 'o', 'u')
  and LOWER(SUBSTRING(city, -1, 1)) not IN ('a', 'e', 'i', 'o', 'u');





