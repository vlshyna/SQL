#### MySQL
Link: [SQLZoo](https://www.sqlzoo.net/wiki/SQL_Tutorial).
These answers are not official, since I solved the exercises on my own, but they are correct. 

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

5) select name, concat(round(100*population/(select population from world where name = 'Germany'),0), '%')
    from world 
    where continent = 'Europe'

6) select name
    from world 
    where continent <> 'Europe' 
    and gdp >= all(select gdp from world where continent='Europe' and gdp > 0)

7) SELECT continent, name, area 
    FROM world x
      WHERE area >= ALL
        (SELECT area FROM world y
            WHERE y.continent=x.continent
              AND area >0)

8) select continent, min(name)
    from world
    group by continent
    order by continent asc, name asc

9) select name, continent, population
    from world
    where continent in
    (select continent from world group by continent having max(population) <= 25000000)

10) select name, continent
    from world w
    where population > 3 *
    (select max(population) from world x where w.continent=x.continent and x.name <> w.name)

### SUM and COUNT
---
1) SELECT SUM(population)
   FROM world

2) select distinct continent from world

3) select sum(gdp) from world where continent = 'Africa'

4) select count(*) from world where area >= 1000000

5) select sum(population) from world where name in ('Estonia', 'Latvia', 'Lithuania')

6) select continent, count(*) from world group by continent

7) select continent, count(*) 
    from world 
    where population >= 10000000
    group by continent

8) select continent
    from world 
    group by continent
    having sum(population) >= 100000000

### JOIN
---
1) SELECT game,team,player,gtime
   FROM goal 
   WHERE player = 'Leandro Trossard'

2) SELECT id, teamname, coach
   FROM team
   WHERE id = 'BEL'

3) SELECT player, gtime, teamname
   FROM goal JOIN team ON goal.team=team.id
   WHERE gtime < 8

4) SELECT g.player, 
       t.teamname, 
       t.coach
 FROM team t 
 JOIN goal g ON t.id = g.team
 WHERE coach LIKE 'Sébastien%'

5) SELECT go.player, ga.id, ga.city
   FROM goal go JOIN game ga ON go.game=ga.id
   WHERE player = 'Harry Edward Kane'

6) select go.player, go.team
    from goal go 
    join game ga ON go.game = ga.id
    where ga.city = 'Vancouver'

7) select go.player, t.teamname
    from goal go
    join team t on go.team=t.id
    join game ga on go.game=ga.id
    where ga.city = 'Vancouver'

8) SELECT game.city, team.teamname
  FROM game
  JOIN team ON team.id = game.team1 OR team.id = game.team2
  WHERE game.played = '2026-07-01'

9) SELECT t.teamname,  go.player
  FROM goal go
  JOIN team t ON go.team=t.id
  JOIN game ga ON go.game = ga.id
  WHERE ga.played = '2026-07-02'

10) select ga.played, go.player, p.pos
    from goal go 
    join game ga on go.game=ga.id
    join player p on go.player = p.playername
    where ga.city = 'Mexico City'

11) SELECT go.player, t.teamname
    FROM goal go
    JOIN player p ON go.player=p.playername
    JOIN team t ON p.team = t.id
    WHERE p.pos='DEF'

12) select go.player, p.pos, t.teamname, ga.city
    from goal go
    join player p on go.player = p.playername
    join team t on p.team = t.id
    join game ga on go.game=ga.id
    where go.gtime BETWEEN 91 AND 120


### More JOIN operations
---

1) SELECT id, title
   FROM movie
   WHERE yr=1962 and budget > 2000000 

2) select yr from movie where title = 'Citizen Kane'
   
3) select id, title, yr 
    from movie 
    where title like 'Star Trek%' 
    order by yr
   
4) select id 
    from actor
    where name = 'Glenn Close'

5) select id from movie where title = 'Casablanca' and yr = 1942

6) select a.name
    from actor a
    join casting c on a.id = c.actorid
    where c.movieid=11768

7) select a.name
    from actor a
    join casting c on a.id = c.actorid
    join movie m on c.movieid = m.id
    where m.title='Alien'

8) select m.title
    from movie m
    join casting c on m.id = c.movieid
    join actor a on c.actorid = a.id
    where a.name = 'Harrison Ford'

9) select m.title
    from movie m
    join casting c on m.id = c.movieid
    join actor a on c.actorid = a.id
    where a.name = 'Harrison Ford' and ord <> 1

10) select m.title, a.name
    from movie m
    join casting c on m.id = c.movieid
    join actor a on c.actorid = a.id
    where c.ord = 1 and m.yr = 1962

11) SELECT yr, COUNT(title) 
    FROM movie 
            JOIN casting ON movie.id=movieid
            JOIN actor   ON actorid=actor.id
    WHERE name='Rock Hudson'
    GROUP BY yr
    HAVING COUNT(title) > 2

12) SELECT m.title, a.name
    FROM movie m 
    JOIN casting c ON (m.id = c.movieid and ord = 1)
    JOIN actor a ON c.actorid = a.id
    WHERE m.id IN (
      SELECT movieid FROM casting
      WHERE actorid IN (
               SELECT id FROM actor 
               WHERE name = 'Julie Andrews')
    )

13) select a.name from actor a
    join casting c on a.id = c.actorid
    join movie m on c.movieid = m.id
    where c.ord = 1
    group by a.name
    having count(m.title) >= 15
    order by name asc

14) select m.title, count(c.actorid)
    from movie m join casting c on m.id = c.movieid
    where m.yr = 1978
    group by m.title
    order by count(c.actorid) desc, m.title

15) select a.name from actor a
    join casting c on a.id = c.actorid
    where c.movieid IN (
    select c.movieid 
    from casting c join actor a on c.actorid = a.id 
    where a.name = 'Art Garfunkel') and a.name <> 'Art Garfunkel'


### Using Null
---

1) select name from teacher where dept is null
   
2) SELECT teacher.name, dept.name
   FROM teacher INNER JOIN dept
           ON (teacher.dept=dept.id)
   
3) SELECT teacher.name, dept.name
 FROM teacher LEFT JOIN dept
           ON (teacher.dept=dept.id)
   
4) SELECT teacher.name, dept.name
 FROM teacher RIGHT JOIN dept
           ON (teacher.dept=dept.id)
  
5) select name, COALESCE(mobile,'07986 444 2266') from teacher

6) select t.name, COALESCE(d.name,'None')
    from teacher t 
    left join dept d on t.dept = d.id

7) select count(name), count(mobile) from teacher

8) select d.name, count(t.name)
    from dept d 
    left join teacher t on d.id = t.dept
    group by d.name

9) select t.name, (
    case when d.id = 1 or d.id = 2 then 'Sci' 
         else 'Art' 
    end
    ) as dep
    from teacher t
    left join dept d on t.dept = d.id

10) select t.name, (
    case when d.id = 1 or d.id = 2 then 'Sci' 
         when d.id = 3 then 'Art'
         else 'None' 
    end
    ) as dep
    from teacher t
    left join dept d on t.dept = d.id

### Self join
---
1) select count(*) from stops

2) select id from stops where name = 'Craiglockhart'

3) select id, name from stops s 
    join route r on s.id = r.stop 
    where company='LRT' and num=4

4) SELECT company, num, COUNT(*)
    FROM route WHERE stop=149 OR stop=53
    GROUP BY company, num
    HAVING COUNT(*) = 2

5) SELECT a.company, a.num, a.stop, b.stop as b
  FROM route a JOIN route b ON
    (a.company=b.company AND a.num=b.num)
  WHERE a.stop=53 and b.stop = 149

6) SELECT a.company, a.num, stopa.name, stopb.name
    FROM route a JOIN route b ON
      (a.company=b.company AND a.num=b.num)
      JOIN stops stopa ON (a.stop=stopa.id)
      JOIN stops stopb ON (b.stop=stopb.id)
    WHERE stopa.name='Craiglockhart' and stopb.name='London Road'

7) SELECT DISTINCT R1.company, R1.num
    FROM route R1, route R2
    WHERE R1.num = R2.num
      AND R1.company = R2.company
      AND R1.stop = 115
      AND R2.stop = 137

8) SELECT R1.company, R1.num
    FROM route R1, route R2, stops S1, stops S2
    WHERE R1.num = R2.num
      AND R1.company = R2.company
      AND R1.stop = S1.id
      AND R2.stop = S2.id
      AND S1.name = 'Craiglockhart'
      AND S2.name = 'Tollcross'

9) SELECT DISTINCT S2.name, R2.company, R2.num
    FROM stops S1, stops S2, route R1, route R2
    WHERE S1.name = 'Craiglockhart'
      AND S1.id = R1.stop
      AND R1.company = R2.company
      AND R1.num = R2.num
      AND R2.stop = S2.id
      AND R2.company = 'LRT'

