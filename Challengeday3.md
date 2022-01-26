Select the American directors ordered from oldest to youngest.
    SELECT date_of_birth,nationality
    FROM directors
    WHERE nationality ='American'
    ORDER BY date_of_birth ASC
Return the sistinct nationalities from the directors table.
    SELECT DISTINCT nationality
    FROM directors
Return the first names, last names and date of births of the 10 youngest female actors.
    SELECT first_name,last_name,date_of_birth, gender
    FROM actors
    WHERE gender ='F'
    ORDER BY date_of_birth DESC
    LIMIT 10
Return the top 3 movies with the highest international takings.
    SELECT MAX(international_takings)
FROM movie_revenues
GROUP BY international_takings/*not right*/

SELECT *
FROM movie_revenues
WHERE international_takings IS NOT NULL
ORDER BY international_takings DESC
LIMIT 3;
Concatenate the first and last names of the directors spearated by a space, and call this new column full_name.
    SELECT (first_name,last_name) AS full_name
    FROM directors

Return the actors with missing first_names or data_of_births.
    SELECT first_name, date_of_birth
    FROM actors
    WHERE first_name IS NULL
    OR date_of_birth IS NULL 
Count the number of actors born after the 1st January 1970.
    SELECT COUNT(date_of_birth)
    FROM actors
    WHERE date_of_birth > '1970-01-01'
What was the highest and lowest domestic takings for a movie.
    SELECT MAX(domestic_takings), MIN(domestic_takings) FROM movie_revenues;

What is the sum total movie length for movies rated 15.
            select sum (movie_length) as Total
        from movies
        where age_certificate = '15';

How many Japanese directors are in the directors table.
What is the average movie length for chinese movies.
    SELECT AVG(movie_length)
FROM movies
WHERE movie_lang = 'Chinese';

How many directors are there per nationality?
SELECT nationality, COUNT(nationality)
FROM directors
GROUP BY nationality;

What is the sum total movie_length for each age certificate and movie language combination?
    SELECT COUNT(*) FROM directors WHERE nationality='Japanese';
Return the movie languages which have a sum total movie length of over 500 minutes.
    FROM movies
GROUP BY movie_lang
HAVING SUM(movie_length) > 500;

Select the directors first and last names, the movie names, and release dates for all Chinese, Korean, and Japanese movies.
    SELECT first_name, last_name, movie_name, release_date
FROM movies
NATURAL JOIN directors
WHERE movie_lang IN ('Chinese', 'Korean', 'Japanese');

Select the movie names, release dates & international takings of all English language movies.
    SELECT movie_name,release_date,movie_revenues.international_takings FROM movies
    JOIN movie_revenues ON movies.movie_id=movie_revenues.movie_id
    WHERE movie_lang='English';

Select the movie names, domestic takings and international takings for all movies with either missing domestic takings or missing international takings and order the results by movie name.
    select movie_name, movie_revenues.domestic_takings, movie_revenues.international_takings
    FROM movies 
    JOIN movie_revenues ON movie_revenues.movie_id = movies.movie_id
    ORDER BY movie_name

 WHERE movie_revenues.domestic_takings IS NULL OR movie_revenues.international_takings IS   NULL;
Use left join to select the first and last names of all British directors and the names and age certificates of the movies that they directed.
    SELECT first_name,last_name,movie_name,age_certifiate
    FROM directors
    LEFT join movies on movies.director_id = directors.director_id
    WHERE nationality = 'British';
Count the number of movies that each director has directed.

Select the first names, last names and dates of birth from directors & actors table. Order the result by the date of birth.
    SELECT first_name, last_name
    FROM directors
    UNION
    SELECT first_name, last_name
    FROM actors    
    ORDER BY date_of_birth ASC;


Select the first and last names of all directprs and actors born in the 1960s. Order the result by last name.

    SELECT first_name, last_name
    FROM directors
    WHERE date_of_birth BETWEEN '1960-01-01' AND '1969-12-31'
    UNION
    SELECT first_name, last_name
    FROM actors
    WHERE date_of_birth BETWEEN '1960-01-01' AND '1969-12-31'
    ORDER BY last_name;

