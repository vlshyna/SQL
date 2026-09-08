#### DB: MySQL
Link: [SQLZoo](https://www.sqlzoo.net/wiki/SQL_Tutorial)

</br>

### SELECT basics
---
1) SELECT population FROM world 
  WHERE name = 'Germany'

2) SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');

3) SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000

### SELECT from WORLD Tutorial
---

1) SELECT name, continent, population FROM world
   
2) SELECT name FROM world
   WHERE population >= 200000000

3) select name, GDP/population
    from world
    where population >= 200000000

4) select name, population/1000000 
    from world
    where continent = 'South America'

5) select name, population 
    from world
    where name in ('France', 'Germany', 'Italy')

6) select name
    from world
    where name like '%United%'

7) select  name, population, area
    from world
    where area > 3000000 or population > 250000000

8) select  name, population, area
    from world
    where area > 3000000 xor population > 250000000

9) select 
    name, 
    round(population/1000000.0, 2), 
    round(GDP/1000000000.0,2)
    from world
    where continent = 'South America'

10) select name, round(gdp/population/1000, 0) * 1000
    from world
    where gdp >= 1000000000000

11) SELECT name, capital
    FROM world
    WHERE LENGTH(name) = LENGTH(capital)

12) SELECT name, capital
    FROM world
    where LEFT(name,1) = LEFT(capital,1) 
    and name <> capital

13) SELECT name
    FROM world
    WHERE name LIKE '%a%'
      AND name LIKE '%e%'
      AND name LIKE '%i%'
      AND name LIKE '%o%'
      AND name LIKE '%u%'
      AND name NOT LIKE '% %';

14) SELECT winner, subject
    FROM nobel
    WHERE yr=1984
    ORDER BY
          CASE WHEN subject IN ('Chemistry','Physics') THEN 1 ELSE 0 END, 
          subject, winner


### SELECT within SELECT Tutorial
---
1) SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')

2) select name
    from world
    where continent = 'Europe'
    and gdp/population > (select gdp/population from world where name='United Kingdom')

3) select name, continent
    from world
    where continent in (select continent from world where name = 'Argentina' or name = 'Australia')
    order by name

4) select name, population
    from world
    where population > (select population from world where name = 'United Kingdom')
    and population < (select population from world where name = 'Germany')
    order by name

