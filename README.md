# sql-zoo-practices



My solutions to the the tutorials and quizzes of [SQL Zoo](https://sqlzoo.net/wiki/SQL_Tutorial). Uses MySQL engine.

## Table of Contents

1. [SELECT basics](#select-basics)
2. [SELECT names](#select-names)
3. [SELECT Quiz](#select-quiz)
4. [SELECT from WORLD Tutorial](#select-from-world-tutorial)
5. [BBC QUIZ](#bbc-quiz)
6. [SELECT from Nobel Tutorial](#select-from-nobel-tutorial)
7. [Nobel Quiz](#nobel-quiz)
8. [SELECT within SELECT Tutorial](#select-within-select-tutorial)
9. [Nested SELECT Quiz](#nested-select-quiz)
10. [SUM and COUNT](#sum-and-count)
11. [SUM and COUNT Quiz](#sum-and-count-quiz)
12. [Nobel Prizes Aggregate functions](#nobel-prizes-aggregate-functions)
13. [The JOIN operation](#the-join-operation)
14. [JOIN Quiz](#join-quiz)
15. [Old JOIN Tutorial](#old-join-tutorial)
16. [More JOIN operations](#more-join-operations)
17. [JOIN Quiz 2](#join-quiz-2)
18. [Using Null](#using-null)
19. [Numeric Examples](#numeric-examples)
20. [Window function](#window-function)
21. [Self join](#self-join)
22. [Self join Quiz](#self-join-quiz)

## Select Basics

1. ///Modify it to show the population of Germany

SELECT population
FROM world
WHERE name = 'Germany';
```

2.Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.

SELECT name, population
FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

3.

```sql
SELECT name, area
FROM world
WHERE area BETWEEN 200000 AND 250000;
```

## SELECT Quiz

1.

```sql
SELECT name, population
  FROM world
 WHERE population BETWEEN 1000000 AND 1250000
```

2.

Table-E

3.

```sql
SELECT name FROM world
 WHERE name LIKE '%a' OR name LIKE '%l'
```

4.

3rd Table

5.

4th Table

6.

```sql
SELECT name, area, population
  FROM world
 WHERE area > 50000 AND population < 10000000
```

7.

```sql
SELECT name, population/area
  FROM world
 WHERE name IN ('China', 'Nigeria', 'France', 'Australia')
```

## SELECT names

1. Find the country that start with Y

```sql
SELECT name
FROM world
WHERE name LIKE 'Y%';
```

2. Find the countries that end with y

```sql
SELECT name
FROM world
WHERE name LIKE '%Y';
```

3. ind the countries that contain the letter x

```sql
SELECT name
FROM world
WHERE name LIKE '%x%';
```

4. Find the countries that end with land

```sql
SELECT name
FROM world
WHERE name LIKE '%land';
```

5. Find the countries that start with C and end with ia

```sql
SELECT name
FROM world
WHERE name LIKE 'C%ia';
```

6. Find the country that has oo in the name

```sql
SELECT name
FROM world
WHERE name LIKE '%oo%';
```

7. Find the countries that have three or more a in the name

```sql
SELECT name
FROM world
WHERE name LIKE '%a%a%a%';
```

8. Find the countries that have "t" as the second character.

```sql
SELECT name
FROM world
WHERE name LIKE '_t%'
ORDER BY name;
```

9. Find the countries that have two "o" characters separated by two others

```sql
SELECT name
FROM world
WHERE name LIKE '%o__o%';
```

10. Find the countries that have exactly four characters.

```sql
SELECT name
FROM world
WHERE name LIKE '____';
```

11. Find the country where the name is the capital city.

```sql
SELECT name
FROM world
WHERE name = capital;
```

12. Find the country where the capital is the country plus "City".

```sql
SELECT name
FROM world
WHERE capital = CONCAT(name, ' City');
```

13. Find the capital and the name where the capital includes the name of the country.

```sql
SELECT capital, name
FROM world
WHERE capital LIKE CONCAT('%', name, '%');
```

14. Find the capital and the name where the capital is an extension of name of the country.

```sql
SELECT capital, name
FROM world
WHERE capital LIKE CONCAT(name, '%')
  AND capital <> name;
```

15. Show the name and the extension where the capital is a proper (non-empty) extension of name of the country.

```sql
SELECT name,
  SUBSTRING(capital, LENGTH(name) + 1, LENGTH(capital)) as ext
FROM world
WHERE capital LIKE CONCAT(name, '%')
  AND capital <> name;
```

## SELECT from WORLD Tutorial

1. Observe the result of running this SQL command to show the name, continent and population of all countries.

```sql
SELECT name, continent, population FROM world
```

2. Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

```sql
SELECT name FROM world
WHERE population >= 200000000;
```

3. Give the name and the per capita GDP for those countries with a population of at least 200 million.
```sql
SELECT name, (gdp / population)
FROM world
WHERE population >= 200000000
```

4. Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.

```sql
SELECT name, (population / 1000000)
FROM world
WHERE continent = 'South America';
```

5. France, Germany, Italy

```sql
SELECT name, population
FROM world
WHERE name in ('France', 'Germany', 'Italy')
```

6. Show the countries which have a name that includes the word 'United'.

```sql
SELECT name
FROM world
WHERE name LIKE 'United%';
```

7. Show the countries that are big by area or big by population. Show name, population and area.

```sql
SELECT name, population, area
FROM world
WHERE area > 3000000 OR population > 250000000;
```

8. Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.

```sql
SELECT name, population, area
FROM world
WHERE area > 3000000 XOR population > 250000000;
```

9. Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.

```sql
SELECT name, ROUND(population / 1000000, 2), ROUND(gdp / 1000000000, 2)
FROM world
WHERE continent = 'South America';
```

10. Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

```sql
SELECT name, ROUND(gdp / population, -3) as per_capita_gdp
FROM world
WHERE gdp >= 1000000000000;
```

11. Show the name and capital where the name and the capital have the same number of characters.

```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

12. Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.


```sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1) AND name <> capital;
```

13. Find the country that has all the vowels and no spaces in its name.

```sql
SELECT name
FROM world
WHERE
  name LIKE '%a%' AND
  name LIKE '%e%' AND
  name LIKE '%i%' AND
  name LIKE '%o%' AND
  name LIKE '%u%' AND
  name NOT LIKE '% %';
```

## BBC QUIZ

1. 

```sql
SELECT name
FROM world
WHERE name LIKE 'U%'
```

2.

```sql
SELECT population
FROM world
WHERE name = 'United Kingdom'
```

3.
'name' should be name

4.

Nauru | 990

5.

```sql
SELECT name, population
  FROM world
 WHERE continent IN ('Europe', 'Asia')
```

6.

```sql
SELECT name FROM world
 WHERE name IN ('Cuba', 'Togo')
```

7.

Brazil
Colombia

## SELECT from Nobel Tutorial

1.

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950;
```

2. Show who won the 1962 prize for literature.

```sql
SELECT winner
FROM nobel
WHERE yr = 1962
  AND subject = 'Literature'
```

3. Show the year and subject that won 'Albert Einstein' his prize.

```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein';
```

4. Give the name of the 'Peace' winners since the year 2000, including 2000.

```sql
SELECT winner
FROM nobel
WHERE subject = 'Peace'
  AND yr >= 2000;
```

5. Show all details (yr, subject, winner) of the literature prize winners for 1980 to 1989 inclusive.

```sql
SELECT *
FROM nobel
WHERE subject = 'Literature'
  AND yr BETWEEN 1980 AND 1989;
```

6. Show all details of the presidential winners:

Theodore Roosevelt
Thomas Woodrow Wilson
Jimmy Carter
Barack Obama

```sql
SELECT *
FROM nobel
WHERE winner IN ('Theodore Roosevelt',
                 'Woodrow Wilson',
                 'Jimmy Carter',
                 'Barack Obama');
```

7. Show the winners with first name John

```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%';
```

8. Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984.

```sql
SELECT *
FROM nobel
WHERE (subject = 'Physics' AND yr = 1980) OR
      (subject = 'Chemistry' AND yr = 1984);
```

9. Show the year, subject, and name of winners for 1980 excluding chemistry and medicine

```sql
SELECT *
FROM nobel
WHERE yr = 1980 AND
  subject NOT IN ('Chemistry', 'Medicine');
```

### Harder Questions

10. Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)

```sql
SELECT *
FROM nobel
WHERE (subject = 'Medicine' AND yr < 1910) OR
      (subject = 'Literature' AND yr > 2003);
```

11. Find all details of the prize won by PETER GRÜNBERG

```sql
SELECT *
FROM nobel
WHERE winner = 'PETER GRÜNBERG';
```

12. Find all details of the prize won by EUGENE O'NEILL

```sql
SELECT *
FROM nobel
WHERE winner = "EUGENE O'NEILL";
```

13. List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.
 
```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC;
```

14. Show the 1984 winners and subject ordered by subject and winner name; but list chemistry and physics last.

```sql
SELECT winner, subject
FROM nobel
WHERE yr = 1984
ORDER BY CASE WHEN subject IN ('Physics', 'Chemistry') THEN 1 ELSE 0 END,
  subject, winner;
```

## Nobel Quiz

1.

```sql
SELECT winner FROM nobel
 WHERE winner LIKE 'C%' AND winner LIKE '%n'
```

2.

```sql
SELECT COUNT(subject) FROM nobel
 WHERE subject = 'Chemistry'
   AND yr BETWEEN 1950 and 1960
```

3.

```sql
SELECT COUNT(DISTINCT yr) FROM nobel
 WHERE yr NOT IN (SELECT DISTINCT yr FROM nobel WHERE subject = 'Medicine')
```

4.

Medicine | Sir John Eccles<br>
Medicine | Sir Frank Macfarlane Burnet

5.

```sql
SELECT yr FROM nobel
 WHERE yr NOT IN(SELECT yr
                   FROM nobel
                 WHERE subject IN ('Chemistry','Physics'))
```

6.

```sql
SELECT DISTINCT yr
  FROM nobel
 WHERE subject='Medicine'
   AND yr NOT IN(SELECT yr FROM nobel
                  WHERE subject='Literature')
   AND yr NOT IN (SELECT yr FROM nobel
                   WHERE subject='Peace')
```

7.

Chemistry | 1<br>
Literature | 1<br>
Medicine | 2<br>
Peace | 1<br>
Physics | 1

## SELECT within SELECT Tutorial

1.

```sql
SELECT name
FROM world
WHERE population > (
  SELECT population from world WHERE name = 'Russia');
```

2.

```sql
SELECT name
FROM world
WHERE continent = 'Europe' AND
  (gdp / population) > (SELECT (gdp / population)
    from world
    WHERE name = 'United Kingdom');
```

3.

```sql
SELECT name, continent
FROM world
WHERE continent IN (SELECT continent
  FROM world
  WHERE name = 'Argentina' OR name = 'Australia')
ORDER BY name;
```

4.

```sql
SELECT name, population
FROM world
WHERE population > (
  SELECT population
  FROM world
  WHERE name = 'Canada')
AND population < (
  SELECT population
  FROM world
  WHERE name = 'Poland');
```

5.

```sql
SELECT
  name,
  CONCAT(ROUND((population / (SELECT population FROM world WHERE name = 'Germany') * 100)), '%')
FROM world
WHERE continent = 'Europe';
```

6.

```sql
SELECT name
FROM world
WHERE gdp > ALL(SELECT gdp
  FROM world
  WHERE (continent = 'Europe') AND (gdp > 0));
```

7.

```sql
SELECT continent, name, area
FROM world AS x
WHERE area >= ALL
  (SELECT area
     FROM world AS y
     WHERE y.continent = x.continent AND
       area > 0);
```

8.

```sql
SELECT continent, name
FROM world
GROUP BY continent;
```

9.

```sql
SELECT name, continent, population
FROM world AS x
WHERE 25000000 > ALL (
  SELECT population
  FROM world AS y
  WHERE y.continent = x.continent
    AND population > 0
  );
```

10.

```sql
SELECT name, continent
FROM world AS x
WHERE population > ALL (
  SELECT population * 3
  FROM world as y
  WHERE y.continent = x.continent
    AND y.name <> x.name
  );
```

## Nested SELECT Quiz

1.

```sql
 SELECT region, name, population FROM bbc x WHERE population <= ALL (SELECT population FROM bbc y WHERE y.region=x.region AND population>0)
```

2.

```sql
 SELECT name,region,population FROM bbc x WHERE 50000 < ALL (SELECT population FROM bbc y WHERE x.region=y.region AND y.population>0)
```

3.

```sql
SELECT name, region FROM bbc x
 WHERE population < ALL (SELECT population/3 FROM bbc y WHERE y.region = x.region AND y.name != x.name)
```

4.

Table-D

5.

```sql
SELECT name FROM bbc
 WHERE gdp > (SELECT MAX(gdp) FROM bbc WHERE region = 'Africa')
```

6.

```sql
SELECT name FROM bbc
 WHERE population < (SELECT population FROM bbc WHERE name='Russia')
   AND population > (SELECT population FROM bbc WHERE name='Denmark')
```

7.

Table-B

## SUM and COUNT

1. Show the total population of the world.

```sql
SELECT SUM(population)
FROM world;
```

2. List all the continents - just once each.

```sql
SELECT DISTINCT continent
FROM world;
```

3. Give the total GDP of Africa

```sql
SELECT SUM(gdp)
FROM world
WHERE continent = 'Africa';
```

4. How many countries have an area of at least 1000000

```sql
SELECT COUNT(area)
FROM world
WHERE area >= 1000000;
```

5. What is the total population of ('Estonia', 'Latvia', 'Lithuania')

```sql
SELECT SUM(population)
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania');
```

6. For each continent show the continent and number of countries.

```sql
SELECT continent, COUNT(name)
FROM world
GROUP BY continent;
```

7. For each continent show the continent and number of countries with populations of at least 10 million.

```sql
SELECT continent, COUNT(name)
FROM world
WHERE population > 10000000
GROUP BY continent;
```

8. List the continents that have a total population of at least 100 million.

```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000;
```

## SUM and COUNT Quiz

1. Select the statement that shows the sum of population of all countries in 'Europe'

```sql
SELECT SUM(population) FROM bbc WHERE region = 'Europe'
```

2. Select the statement that shows the number of countries with population smaller than 150000

```sql
SELECT COUNT(name) FROM bbc WHERE population < 150000
```

3. Select the list of core SQL aggregate functions

AVG(), COUNT(), MAX(), MIN(), SUM()

4.

No result due to invalid use of the WHERE function

5.Select the statement that shows the average population of 'Poland', 'Germany' and 'Denmark'

```sql
SELECT AVG(population) FROM bbc WHERE name IN ('Poland', 'Germany', 'Denmark')
```

6. Select the statement that shows the medium population density of each region

```sql
SELECT region, SUM(population)/SUM(area) AS density FROM bbc GROUP BY region
```

7.  Select the statement that shows the name and population density of the country with the largest population
```sql
SELECT name, population/area AS density FROM bbc WHERE population = (SELECT MAX(population) FROM bbc)
```



Table-D

## Nobel Prizes Aggregate functions

1.

```sql
SELECT COUNT(winner) FROM nobel;
```

2.

```sql
SELECT DISTINCT subject
FROM nobel;
```

3.

```sql
SELECT COUNT(subject)
FROM nobel
WHERE subject = 'Physics';
```

4.

```sql
SELECT subject, COUNT(subject) as prices
FROM nobel
GROUP BY subject;
```

5.

```sql
SELECT subject, MIN(yr) as first_year
FROM nobel
GROUP BY subject;
```

6.

```sql
SELECT subject, COUNT(subject) as awards_in_2000
FROM nobel
WHERE yr = 2000
GROUP BY subject;
```

7.

```sql
SELECT subject, COUNT(DISTINCT winner) as distinct_winners
FROM nobel
GROUP BY subject;
```

8.

```sql
SELECT subject, COUNT(DISTINCT yr) as distinct_yr
FROM nobel
GROUP BY subject;
```

9.

```sql
SELECT yr
FROM nobel
WHERE subject = 'Physics'
GROUP BY yr
HAVING COUNT(yr) = 3;
```

10.

```sql
SELECT winner
FROM nobel
GROUP BY winner
HAVING COUNT(winner) > 1;
```

11.

```sql
SELECT winner
FROM nobel
GROUP BY winner
HAVING COUNT(DISTINCT subject) > 1
```

12.

```sql
SELECT yr, subject
FROM nobel
WHERE yr > 1999
GROUP BY yr, subject
HAVING COUNT(yr) > 2;
```

## The JOIN operation

1. Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'

```sql
SELECT matchid, player
FROM goal
WHERE teamid = 'GER';
```

2. Show id, stadium, team1, team2 for just game 1012


```sql
SELECT id,stadium,team1,team2
FROM game
WHERE id = 1012;
```

3. Modify it to show the player, teamid, stadium and mdate for every German goal.

```sql
SELECT goal.player, goal.teamid, game.stadium, game.mdate
FROM game
INNER JOIN goal
ON game.id = goal.matchid
WHERE goal.teamid = 'GER';
```

4. Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'

```sql
SELECT game.team1, game.team2, goal.player
FROM game
INNER JOIN goal
ON game.id = goal.matchid
WHERE goal.player LIKE 'Mario%';
```

5. Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10


```sql
SELECT goal.player, goal.teamid, eteam.coach, goal.gtime
FROM goal
INNER JOIN eteam
ON goal.teamid = eteam.id
WHERE goal.gtime <= 10;
```

6. List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.

```sql
SELECT game.mdate, eteam.teamname
FROM game
INNER JOIN eteam
ON game.team1 = eteam.id
WHERE eteam.coach = 'Fernando Santos';
```

7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'



```sql
SELECT goal.player
FROM game
INNER JOIN goal
ON goal.matchid = game.id
WHERE game.stadium = 'National Stadium, Warsaw';
```

8.Instead show the name of all players who scored a goal against Germany.



```sql
SELECT DISTINCT goal.player
FROM game
INNER JOIN goal
ON goal.matchid = game.id
WHERE goal.teamid <> 'GER'
  AND (game.team1 = 'GER' OR game.team2 = 'GER');
```

9. Show teamname and the total number of goals scored.


```sql
SELECT eteam.teamname, COUNT(goal.teamid)
FROM goal
INNER JOIN eteam
ON eteam.id = goal.teamid
GROUP BY eteam.teamname;
```

10. Show the stadium and the number of goals scored in each stadium.


```sql
SELECT game.stadium, COUNT(goal.matchid)
FROM game
INNER JOIN goal
ON game.id = goal.matchid
GROUP BY game.stadium;
```

11. For every match involving 'POL', show the matchid, date and the number of goals scored.


```sql
SELECT goal.matchid, game.mdate, COUNT(goal.matchid)
FROM game
INNER JOIN goal
ON goal.matchid = game.id
WHERE game.team1 = 'POL' OR game.team2 = 'POL'
GROUP BY goal.matchid;
```

12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'


```sql
SELECT goal.matchid, game.mdate, COUNT(goal.matchid) AS german_goals
FROM game
INNER JOIN goal
ON game.id = goal.matchid
WHERE goal.teamid = 'GER'
GROUP BY goal.matchid;
```

13. List every match involving the ENG team, show the number goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises.


```sql
SELECT
  game.mdate,
  game.team1,
  SUM(CASE WHEN goal.teamid = game.team1 THEN 1 ELSE 0 END) AS score1,
  game.team2,
  SUM(CASE WHEN goal.teamid = game.team2 THEN 1 ELSE 0 END) AS score2
FROM game
LEFT JOIN goal
ON game.id = goal.matchid
GROUP BY game.id, game.mdate
ORDER BY game.mdate, goal.matchid, game.team1, game.team2
```

## JOIN Quiz

1.

```sql
game  JOIN goal ON (id=matchid)
```

2.

matchid, teamid, player, gtime, id, teamname, coach

3.

```sql
SELECT player, teamid, COUNT(*)
  FROM game JOIN goal ON matchid = id
 WHERE (team1 = "GRE" OR team2 = "GRE")
   AND teamid != 'GRE'
 GROUP BY player, teamid
```

4.

DEN | 9 June 2012<br>
GER | 9 June 2012

5.

```sql
  SELECT DISTINCT player, teamid
   FROM game JOIN goal ON matchid = id
  WHERE stadium = 'National Stadium, Warsaw'
 AND (team1 = 'POL' OR team2 = 'POL')
   AND teamid != 'POL'
```

6.

```sql
SELECT DISTINCT player, teamid, gtime
  FROM game JOIN goal ON matchid = id
 WHERE stadium = 'Stadion Miejski (Wroclaw)'
   AND (( teamid = team2 AND team1 != 'ITA') OR ( teamid = team1 AND team2 != 'ITA'))
```

7.

Netherlands | 2<br>
Poland | 2<br>
Republic of Ireland | 1<br>
Ukraine | 2

## Old JOIN Tutorial

1.

```sql
SELECT who, country.name
FROM ttms JOIN country
ON (ttms.country=country.id)
WHERE games = 2000
```

2.

```sql
SELECT ttms.who, ttms.color
FROM ttms
INNER JOIN country
ON ttms.country = country.id
WHERE country.name = 'Sweden';
```

3.

```sql
SELECT ttms.games
FROM ttms
INNER JOIN country
ON ttms.country = country.id
WHERE country.name = 'China' AND ttms.color = 'gold';
```

4.

```sql
SELECT ttws.who AS 'barcelona_winners'
FROM ttws
INNER JOIN games
ON ttws.games = games.yr
WHERE games.city = 'Barcelona';
```

5.

```sql
SELECT games.city, ttws.color
FROM ttws
INNER JOIN games
ON ttws.games = games.yr
WHERE ttws.who = 'Jing Chen';
```

6.

```sql
SELECT ttws.who, games.city
FROM ttws
INNER JOIN games
ON ttws.games = games.yr
WHERE ttws.color = 'gold';
```

7.

```sql
SELECT ttmd.games, ttmd.color
FROM ttmd
INNER JOIN team
ON ttmd.team = team.id
WHERE team.name LIKE '%Yan Sen%';
```

8.

```sql
SELECT team.name
FROM ttmd
INNER JOIN team
ON ttmd.team = team.id
WHERE ttmd.color = 'gold' AND ttmd.games = 2004;
```

9.

```sql
SELECT team.name
FROM ttmd
INNER JOIN team
ON ttmd.team = team.id
WHERE ttmd.country = 'FRA';
```

## More JOIN operations

1. List the films where the yr is 1962 and the budget is over 2000000 [Show id, title]



```sql
SELECT id, title
FROM movie
WHERE yr = 1962;
```

2. Give year of 'Citizen Kane'.



```sql
SELECT yr
FROM movie
WHERE title = 'Citizen Kane';
```

3. List all of the Star Trek movies, include the id, title and yr (all of these movies start with the words Star Trek in the title). Order results by year.



```sql
SELECT id, title, yr
FROM movie
WHERE title LIKE '%Star Trek%'
ORDER BY yr;
```

4. What id number does the actor 'Glenn Close' have?



```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close';
```

5. What is the id of the 1942 film 'Casablanca'



```sql
SELECT id
FROM movie
WHERE title = 'Casablanca';
```

6. Use movieid=11768, (or whatever value you got from the previous question)



```sql
SELECT actor.name AS casablanca_cast_list
FROM movie
INNER JOIN casting
ON movie.id = casting.movieid
INNER JOIN actor
ON casting.actorid = actor.id
WHERE casting.movieid = (
  SELECT id
  FROM movie
  WHERE title = 'Casablanca'
  );
```

7. Obtain the cast list for the film 'Alien'



```sql
SELECT actor.name AS alien_cast_list
FROM movie
INNER JOIN casting
ON movie.id = casting.movieid
INNER JOIN actor
ON casting.actorid = actor.id
WHERE casting.movieid = (
  SELECT id
  FROM movie
  WHERE title = 'Alien'
  );
```

8. List the films in which 'Harrison Ford' has appeared



```sql
SELECT movie.title
FROM movie
INNER JOIN casting
ON movie.id = casting.movieid
INNER JOIN actor
ON casting.actorid = actor.id
WHERE casting.actorid = (
  SELECT id
  FROM actor
  WHERE name = 'Harrison Ford'
  );
```

9. List the films where 'Harrison Ford' has appeared - but not in the starring role. [Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]



```sql
SELECT movie.title
FROM movie
INNER JOIN casting
ON movie.id = casting.movieid
INNER JOIN actor
ON casting.actorid = actor.id
WHERE casting.actorid = (
  SELECT id
  FROM actor
  WHERE name = 'Harrison Ford'
  )
  AND casting.ord <> 1;
```

10. List the films together with the leading star for all 1962 films.



```sql
SELECT
  movie.title,
  (CASE WHEN casting.ord = 1 THEN actor.name END) AS name
FROM movie
INNER JOIN casting
ON movie.id = casting.movieid
INNER JOIN actor
ON casting.actorid = actor.id
WHERE movie.yr = 1962
 AND (CASE WHEN casting.ord = 1 THEN actor.name END) IS NOT NULL;
```

11. Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.



```sql
SELECT yr, COUNT(movie.title)
FROM movie
INNER JOIN casting
ON movie.id = casting.movieid
INNER JOIN actor
ON casting.actorid = actor.id
WHERE actor.name = 'Rock Hudson'
GROUP BY movie.yr
HAVING COUNT(movie.title) > 2;
```

12. List the film title and the leading actor for all of the films 'Julie Andrews' played in.



```sql
SELECT
  movie.title,
  (CASE WHEN casting.ord = 1 THEN actor.name END) as leading_actor
FROM movie
INNER JOIN casting
ON movie.id = casting.movieid
INNER JOIN actor
ON casting.actorid = actor.id
WHERE (CASE WHEN casting.ord = 1 THEN actor.name END) IS NOT NULL
  AND casting.movieid IN (
    SELECT casting.movieid
    FROM casting
    INNER JOIN actor
    ON casting.actorid = actor.id
    WHERE actor.name = 'Julie Andrews'
  );
```

13. Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.



```sql
SELECT actor.name
FROM movie
INNER JOIN casting
ON movie.id = casting.movieid
INNER JOIN actor
ON casting.actorid = actor.id
GROUP BY actor.name
HAVING SUM(CASE WHEN casting.ord = 1 THEN 1 ELSE 0 END) >= 15;
```

14. List the films released in the year 1978 ordered by the number of actors in the cast, then by title.



```sql
SELECT movie.title, COUNT(actor.id) as actors
FROM movie
INNER JOIN casting
ON movie.id = casting.movieid
INNER JOIN actor
ON casting.actorid = actor.id
WHERE movie.yr = 1978
GROUP BY movie.title
ORDER BY actors DESC, movie.title;
```

15. List all the people who have worked with 'Art Garfunkel'.



```sql
SELECT DISTINCT actor.name
FROM movie
INNER JOIN casting
ON movie.id = casting.movieid
INNER JOIN actor
ON casting.actorid = actor.id
WHERE casting.movieid IN (
  SELECT casting.movieid
  FROM casting
  INNER JOIN actor
  ON casting.actorid = actor.id
  WHERE actor.name = 'Art Garfunkel'
)
  AND actor.name <> 'Art Garfunkel';
```

## JOIN Quiz 2

1.

```sql
SELECT name
  FROM actor INNER JOIN movie ON actor.id = director
 WHERE gross < budget
```

2.

```sql
SELECT *
  FROM actor JOIN casting ON actor.id = actorid
  JOIN movie ON movie.id = movieid
```

3.

```sql
SELECT name, COUNT(movieid)
  FROM casting JOIN actor ON actorid=actor.id
 WHERE name LIKE 'John %'
 GROUP BY name ORDER BY 2 DESC
```

4.

Table-B

5.

```sql
SELECT name
  FROM movie JOIN casting ON movie.id = movieid
  JOIN actor ON actor.id = actorid
WHERE ord = 1 AND director = 351
```

6.

link the director column in movies with the primary key in actor
connect the primary keys of movie and actor via the casting table

7.

Table-B

## Using Null

1. List the teachers who have NULL for their department.



```sql
SELECT name
FROM teacher
WHERE dept IS NULL;
```

2. Note the INNER JOIN misses the teachers with no department and the departments with no teacher.



```sql
SELECT teacher.name, dept.name
FROM teacher
INNER JOIN dept
ON teacher.dept = dept.id;
```

3. Use a different JOIN so that all teachers are listed.



```sql
SELECT teacher.name, dept.name
FROM teacher
LEFT JOIN dept
ON teacher.dept = dept.id;
```

4. Use a different JOIN so that all departments are listed.



```sql
SELECT teacher.name, dept.name
FROM teacher
RIGHT JOIN dept
ON teacher.dept = dept.id;
```

5. Use COALESCE to print the mobile number. Use the number '07986 444 2266' if there is no number given. Show teacher name and mobile number or '07986 444 2266'



```sql
SELECT
  name,
  COALESCE(mobile, '07986 444 2266') as mobile
FROM teacher;
```

6. Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department.



```sql
SELECT
  teacher.name,
  COALESCE(dept.name, 'None') as dept
FROM teacher
LEFT JOIN dept
ON teacher.dept = dept.id;
```

7. Use COUNT to show the number of teachers and the number of mobile phones.



```sql
SELECT Count(name), Count(mobile)
FROM teacher;
```

8. Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed.



```sql
SELECT dept.name, COUNT(teacher.name) as number_of_teacher
FROM teacher
RIGHT JOIN dept
ON teacher.dept = dept.id
GROUP BY dept.name;
```

9. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise.



```sql
SELECT
  name,
  (CASE WHEN dept IN (1, 2) THEN 'Sci' ELSE 'Art' END)
FROM teacher;
```

10. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise.



```sql
SELECT
  name,
  (CASE WHEN dept IN (1, 2) THEN 'Sci'
        WHEN dept = 3 THEN 'Art'
        ELSE 'None' END)
FROM teacher;
```

## Using Null Quiz

1.

```sql
 SELECT teacher.name, dept.name FROM teacher LEFT OUTER JOIN dept ON (teacher.dept = dept.id)
```

2.

```sql
 SELECT dept.name FROM teacher JOIN dept ON (dept.id = teacher.dept) WHERE teacher.name = 'Cutflower'
```

3.

```sql
 SELECT dept.name, COUNT(teacher.name) FROM teacher RIGHT JOIN dept ON dept.id = teacher.dept GROUP BY dept.name
```

4.

display 0 in result column for all teachers without department

5.

'four' for Throd

6.

Table-A

## Numeric Examples

1.  Show the the percentage who STRONGLY AGREE



```sql
SELECT A_STRONGLY_AGREE
FROM nss
WHERE question='Q01'
 AND institution = 'Edinburgh Napier University'
 AND subject = '(8) Computer Science'
```

2. Show the institution and subject where the score is at least 100 for question 15.



```sql
SELECT institution, subject
FROM nss
WHERE score >= 100 AND question = 'Q15';
```

3.Show the institution and score where the score for '(8) Computer Science' is less than 50 for question 'Q15'



```sql
SELECT institution, score
FROM nss
WHERE subject = '(8) Computer Science'
  AND score < 50
  AND question = 'Q15';
```

4. Show the subject and total number of students who responded to question 22 for each of the subjects '(8) Computer Science' and '(H) Creative Arts and Design'.



```sql
SELECT subject, SUM(response)
FROM nss
WHERE question = 'Q22'
  AND subject IN ('(8) Computer Science',
                  '(H) Creative Arts and Design')
GROUP BY subject;
```

5. Show the subject and total number of students who A_STRONGLY_AGREE to question 22 for each of the subjects '(8) Computer Science' and '(H) Creative Arts and Design'.



```sql
SELECT subject,
  SUM((A_STRONGLY_AGREE / 100) * response)
FROM nss
WHERE question = 'Q22'
  AND subject IN ('(8) Computer Science',
                  '(H) Creative Arts and Design')
GROUP BY subject;
```

6. Show the percentage of students who A_STRONGLY_AGREE to question 22 for the subject '(8) Computer Science' show the same figure for the subject '(H) Creative Arts and Design'.



```sql
SELECT subject,
  ROUND(SUM(A_STRONGLY_AGREE * response) / SUM(response))
FROM nss
WHERE question = 'Q22'
  AND subject IN ('(8) Computer Science',
                  '(H) Creative Arts and Design')
GROUP BY subject;
```

7. Show the average scores for question 'Q22' for each institution that include 'Manchester' in the name.



```sql
SELECT institution,
  ROUND(SUM((score * response)) / SUM(response))
FROM nss
WHERE question = 'Q22' AND institution LIKE '%Manchester%'
GROUP BY institution;
```

8. Show the institution, the total sample size and the number of computing students for institutions in Manchester for 'Q01'.



```sql
SELECT
  institution,
  SUM(sample) AS sample_size,
  SUM(CASE WHEN subject = '(8) Computer Science' THEN sample ELSE 0 END) AS comp
FROM nss
WHERE question = 'Q01' AND institution LIKE '%Manchester%'
GROUP BY institution;
```

## Window function

1. Show the lastName, party and votes for the constituency 'S14000024' in 2017.



```sql
SELECT lastName, party, votes
FROM ge
WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY votes DESC;
```

2. Show the party and RANK for constituency S14000024 in 2017. List the output by party


```sql
SELECT
  party,
  votes,
  RANK() OVER (ORDER BY votes DESC) as posn
FROM ge
WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY party;
```

3. Use PARTITION to show the ranking of each party in S14000021 in each year. Include yr, party, votes and ranking (the party with the most votes is 1).


```sql
SELECT
  yr,
  party,
  votes,
  RANK() OVER (PARTITION BY yr ORDER BY votes DESC) as posn
FROM ge
WHERE constituency = 'S14000021'
ORDER BY party, yr;
```

4. Use PARTITION BY constituency to show the ranking of each party in Edinburgh in 2017. Order your results so the winners are shown first, then ordered by constituency.


```sql
SELECT
  constituency,
  party,
  votes,
  RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn
FROM ge
WHERE yr = 2017
  AND constituency BETWEEN 'S14000021' AND 'S14000026'
ORDER BY posn, constituency;
```

5. Show the parties that won for each Edinburgh constituency in 2017.


```sql
SELECT
  constituency,
  party,
  votes,
  RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn
FROM ge
WHERE yr = 2017
  AND constituency BETWEEN 'S14000021' AND 'S14000026'
ORDER BY posn, constituency;
```

6. Show how many seats for each party in Scotland in 2017.


```sql
SELECT party, COUNT(party)
FROM (
  SELECT constituency,
    party,
    RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) as posn
  FROM ge
  WHERE yr = 2017 AND constituency LIKE 'S%'
) AS party_ranking
WHERE party_ranking.posn = 1
GROUP BY party;
```

## Self join

1.

```sql
SELECT COUNT(*)
FROM stops;
```

2.

```sql
SELECT id
FROM stops
WHERE name = 'Craiglockhart';
```

3.

```sql
SELECT stops.id, stops.name
FROM stops
INNER JOIN route
ON stops.id = route.stop
WHERE route.num = 4 AND route.company = 'LRT'
ORDER BY route.pos;
```

4.

```sql
SELECT company, num, COUNT(*)
FROM route
WHERE stop = 149 OR stop = 53
GROUP BY company, num
HAVING COUNT(*) = 2;
```

5.

```sql
SELECT a.company, a.num, a.stop, b.stop
FROM route a
INNER JOIN route b
ON (a.company = b.company AND a.num = b.num)
WHERE a.stop = 53
  AND b.stop = (
    SELECT id
    FROM stops
    WHERE name = 'London Road'
  );
```

6.

```sql
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a
INNER JOIN route b
ON (a.company = b.company AND a.num = b.num)
INNER JOIN stops stopa
  ON a.stop = stopa.id
INNER JOIN stops stopb
  ON b.stop = stopb.id
WHERE stopa.name = 'Craiglockhart' AND stopb.name = 'London Road';
```

7.

```sql
SELECT DISTINCT a.company, a.num
FROM route a
INNER JOIN route b
ON (a.company = b.company AND a.num = b.num)
WHERE a.stop = 115 AND b.stop = 137;
```

8.

```sql
SELECT a.company, a.num
FROM route a
INNER JOIN route b
  ON (a.company = b.company AND a.num = b.num)
INNER JOIN stops stopa
  ON (a.stop = stopa.id)
INNER JOIN stops stopb
  ON (b.stop = stopb.id)
WHERE stopa.name = 'Craiglockhart' AND stopb.name = 'Tollcross';
```

9.

```sql
SELECT stopb.name, a.company, a.num
FROM route a
INNER JOIN route b
  ON (a.company = b.company AND a.num = b.num)
INNER JOIN stops stopa
  ON (a.stop = stopa.id)
INNER JOIN stops stopb
  ON (b.stop = stopb.id)
WHERE stopa.name = 'Craiglockhart' AND a.company = 'LRT';
```

10.

```sql
SELECT DISTINCT a.num, a.company, stops.name, b.num, b.company
FROM (
  SELECT x.company, x.num, y.stop
  FROM route x
  INNER JOIN route y
    ON (x.company = y.company AND x.num = y.num)
  INNER JOIN stops stopx
    ON (x.stop = stopx.id)
  INNER JOIN stops stopy
    ON (y.stop = stopy.id)
  WHERE stopx.name = 'Craiglockhart'
) AS a
INNER JOIN (
  SELECT x.company, x.num, y.stop
  FROM route x
  INNER JOIN route y
    ON (x.company = y.company AND x.num = y.num)
  INNER JOIN stops stopx
    ON (x.stop = stopx.id)
  INNER JOIN stops stopy
    ON (y.stop = stopy.id)
  WHERE stopx.name = 'Lochend'
) AS b
ON (a.stop = b.stop)
INNER JOIN stops
  ON (a.stop = stops.id)
ORDER BY a.num, stops.name, b.num
```

## Self join Quiz

1.

```sql
SELECT DISTINCT a.name, b.name
  FROM stops a JOIN route z ON a.id=z.stop
  JOIN route y ON y.num = z.num
  JOIN stops b ON y.stop=b.id
 WHERE a.name='Craiglockhart' AND b.name ='Haymarket'
```

2.

```sql
SELECT S2.id, S2.name, R2.company, R2.num
  FROM stops S1, stops S2, route R1, route R2
 WHERE S1.name='Haymarket' AND S1.id=R1.stop
   AND R1.company=R2.company AND R1.num=R2.num
   AND R2.stop=S2.id AND R2.num='2A'
```

3.

```sql
SELECT a.company, a.num, stopa.name, stopb.name
  FROM route a JOIN route b ON (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
 WHERE stopa.name='Tollcross'
```
