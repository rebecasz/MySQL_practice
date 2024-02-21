
https://www.sqlzoo.net/

world(name, continent, area, population, gdp)

name	continent	area	population	gdp
Afghanistan	Asia	652230	25500100	20343000000
Albania	Europe	28748	2831741	12960000000
Algeria	Africa	2381741	37100000	188681000000
Andorra	Europe	468	78115	3712000000
Angola	Africa	1246700	20609294	100990000000
...

### 1. Show the total population of the world.

select sum(population) 
from world

### 2. List all the continents - just once each.

select distinct(continent)
from world

### 3. Give the total GDP of Africa

select sum(gdp)
from world
where continent = 'Africa'

### 4. How many countries have an area of at least 1000000

select count(continent)
from world
where area >1000000

### 5. What is the total population of ('Estonia', 'Latvia', 'Lithuania')

select sum(population)
from world
where name in ('Estonia', 'Latvia', 'Lithuania')

### 6. For each continent show the continent and number of countries.

select continent, count(name)
from world
group by continent

### 7. For each continent show the continent and number of countries with populations of at least 10 million.

select continent, count(name)
from world
where population > 10000000
group by continent

### 8. List the continents that have a total population of at least 100 million.

select continent
from world
group by continent
having sum(population)>= 100000000

### 9. Show the name for the countries that have a population of at least 200 million. 

select name
from world
where population > 200000000

### 10. Give the name and the per capita GDP for those countries with a population of at least 200 million.

select name, gdp/population
from world 
where population >200000000

### 11. Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.

select name, population/1000000
from world
where continent =  'South America'

### 12. Show the name and population for France, Germany, Italy

select name, population
from world
where name in ('France', 'Germany', 'Italy')

### 13. Show the countries which have a name that includes the word 'United'

select name
from world
where name like '%United%'

### 14.  A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million. Show the countries that are big by area or big by population. Show name, population and area.

select name, population, area
from world
where population > 250000000 or area > 3000000

### 15. Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.

Australia has a big area but a small population, it should be included.
Indonesia has a big population but a small area, it should be included.
China has a big population and big area, it should be excluded.
United Kingdom has a small population and a small area, it should be excluded.

select name, population, area
from world
where population > 250000000 xor area > 3000000

### 16. Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.

select name, round(population / 1000000,2) , round(gdp / 1000000000,2) 
from world
where continent ='South America'

### 17. Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

select name, round(gdp/ population/1000)*1000
from world
where gdp > 1000000000000

### 18. Greece has capital Athens. Each of the strings 'Greece', and 'Athens' has 6 characters.Show the name and capital where the name and the capital have the same number of characters.

select name, capital
from world
where length(name)= length(capital)

### 19. The capital of Sweden is Stockholm. Both words start with the letter 'S'.
Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.

SELECT name, capital
FROM world
where Left(name,1) = left(capital, 1) and name <> capital


### 20. Equatorial Guinea and Dominican Republic have all of the vowels (a e i o u) in the name. They don't count because they have more than one word in the name. Find the country that has all the vowels and no spaces in its name.

SELECT name
   FROM world
WHERE name like '%a%' and name like '%e%' and name like '%i%' and name like '%o%' and name like '%u%' and name not like "% %"


### 21. List each country name where the population is larger than that of 'Russia'.

SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')

### 22. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

select name
from world 
where continent = 'Europe' and gdp/population > (select gdp/population from world where name ='United Kingdom')

### 23. List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

select name, continent
from world
where continent in (select continent from world where name = 'Argentina' or name = 'Australia')
order by name 

### 24. Which country has a population that is more than United Kingdom but less than Germany? Show the name and the population.

select name, population
from world 
where population > (select population from world where name = 'United Kingdom') and population < (select population from world where name = 'Germany')

### 25. Germany (population 80 million) has the largest population of the countries in Europe. Austria (population 8.5 million) has 11% of the population of Germany.Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
The format should be Name.

select name, concat(round((100*population /(select population from world where name='Germany')),0),'%')
from world
where continent = 'Europe' 

### 26. Which countries have a GDP greater than every country in Europe? [Give the name only.

select name
from world 
where gdp > (select max(gdp) from world where continent = 'Europe')

### 27. Find the largest country (by area) in each continent, show the continent, the name and the area:

SELECT continent, name, area
FROM world w1
WHERE area = (
    SELECT MAX(w2.area)
    FROM world w2
    WHERE w2.continent = w1.continent
);


### 28. List each continent and the name of the country that comes first alphabetically.

select continent, name
from world 
group by continent
order by name asc

### 29. Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.

select name, continent, population
from world
where continent in (select continent from world where population <= 25000000) 

### 30. Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.

SELECT name, continent
FROM world w1
WHERE population > 3 * (
    SELECT MAX(population)
    FROM world w2
    WHERE w2.continent = w1.continent AND w2.name <> w1.name
)



