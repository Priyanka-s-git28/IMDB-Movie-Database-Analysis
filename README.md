# IMDB-Movie-Database-Analysis
 End-to-end exploratory data analysis (EDA) of the IMDb movie database using MySQL. This project focuses on identifying trends in global cinema, genre performance, and director impact through advanced SQL techniques like window functions, CTEs, and complex joins
- use project_movie_database;
-- show tables;
-- a)	Can you get all data about movies? 
select  * from movies;
-- b)	How do you get all data about directors?
select * from directors;
-- c)	Check how many movies are present in IMDB.
select count(*) as total_movies from movies;
-- d)	Find these 3 directors: James Cameron ; Luc Besson ; John Woo
select * from directors where name in ("James Cameron","Luc Besson","John Woo");
-- e)	Find all directors with name starting with S.
select * from directors where name like "S%";
-- f)	Count female directors
 select count(*) as female_directors from directors where gender=1;
-- g)	Find the name of the 10th first women directors?
 select name from directors where gender=1 order by  name asc limit 9,1;
-- h)	What are the 3 most popular movies?
select original_title,popularity from movies order by popularity desc limit 3;
-- i)	What are the 3 most bankable movies?
 select original_title,revenue from movies order by revenue desc limit 3;
-- j)	What is the most awarded average vote since the January 1st, 2000?
select original_title,vote_average from movies where release_date >= '2000-01-01' order by vote_average desc limit 1;
-- k)	Which movie(s) were directed by Brenda Chapman?
use project_movie_database;
SELECT m.original_title
 FROM movies m
 JOIN directors d 
 ON m.director_id = d.id
WHERE d.name = 'Brenda Chapman';
-- l)	Which director made the most movies?
select directors.name,count(movies.id) AS movie_count
from directors
join movies on directors.id=movies.director_id
group by directors.name
order by movie_count DESC LIMIT 1;
-- m)	Which director is the most bankable?
select directors.name,sum(movies.revenue) AS total_revenue
FROM directors
join movies on directors.id=movies.director_id
 group by directors.name
 order by total_revenue DESC LIMIT 1;
