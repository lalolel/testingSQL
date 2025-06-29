-- SQLite Basics Tutorial: Movies Database
-- This comprehensive tutorial covers fundamental SQL operations with detailed explanations

-- ================================
-- SECTION 1: DATABASE SETUP
-- ================================

-- First, let's create a movies table to work with
-- This table will store movie information including name, year, genre, and IMDB rating
CREATE TABLE movies (
    id INTEGER PRIMARY KEY,  -- Unique identifier for each movie
    name TEXT NOT NULL,      -- Movie title (cannot be empty)
    year INTEGER,           -- Release year
    genre TEXT,             -- Movie genre (action, comedy, etc.)
    imdb_rating REAL        -- IMDB rating as decimal number
);

-- Let's insert some sample data to work with
-- Using INSERT INTO to add multiple movies at once
INSERT INTO movies (name, year, genre, imdb_rating) VALUES
    ('The Shawshank Redemption', 1994, 'drama', 9.3),
    ('The Godfather', 1972, 'crime', 9.2),
    ('Pulp Fiction', 1994, 'crime', 8.9),
    ('The Dark Knight', 2008, 'action', 9.0),
    ('Forrest Gump', 1994, 'drama', 8.8),
    ('Inception', 2010, 'action', 8.8),
    ('The Matrix', 1999, 'action', 8.7),
    ('Se7en', 1995, 'thriller', 8.6),
    ('The Silence of the Lambs', 1991, 'thriller', 8.6),
    ('Saving Private Ryan', 1998, 'war', 8.6),
    ('Interstellar', 2014, 'sci-fi', 8.6),
    ('The Avengers', 2012, 'action', 8.0),
    ('Titanic', 1997, 'romance', 7.8),
    ('The Notebook', 2004, 'romance', 7.8),
    ('Superbad', 2007, 'comedy', 7.6),
    ('The Hangover', 2009, 'comedy', 7.7),
    ('Scary Movie', 2000, 'comedy', 6.2),
    ('Batman & Robin', 1997, 'action', 3.8),
    ('Catwoman', 2004, 'action', 3.4),
    ('The Room', 2003, 'drama', 3.7);

-- ================================
-- SECTION 2: BASIC SELECT QUERIES
-- ================================

-- Basic SELECT: Retrieve all columns from all rows
-- The asterisk (*) means "all columns"
SELECT * FROM movies;

-- SELECT specific columns: Only get movie names and years
-- This is more efficient when you don't need all data
SELECT name, year FROM movies;

-- COUNT: Get the total number of movies in our database
-- COUNT(*) counts all rows, including those with NULL values
SELECT COUNT(*) AS total_movies FROM movies;

-- ================================
-- SECTION 3: WHERE CLAUSE - FILTERING DATA
-- ================================

-- Checkpoint 1: Find movies with IMDB rating less than 5
-- WHERE clause filters rows based on specified conditions
-- This query finds poorly rated movies
SELECT * 
FROM movies 
WHERE imdb_rating < 5;

-- Checkpoint 2: Find movies released after 2014
-- Using comparison operator (>) to filter by year
SELECT *
FROM movies
WHERE year > 2014;

-- Additional WHERE examples with different operators:

-- Equal to: Find movies from exactly 1994
SELECT * FROM movies WHERE year = 1994;

-- Not equal to: Find movies that are NOT action movies
SELECT * FROM movies WHERE genre != 'action';

-- Greater than or equal to: Movies with rating 8.5 or higher
SELECT * FROM movies WHERE imdb_rating >= 8.5;

-- Less than or equal to: Movies released in 2000 or earlier
SELECT * FROM movies WHERE year <= 2000;

-- ================================
-- SECTION 4: PATTERN MATCHING WITH LIKE
-- ================================

-- LIKE with underscore (_): Matches exactly one character
-- This finds movies with "Se" + any single character + "en"
-- Example: "Se7en" matches this pattern
SELECT * 
FROM movies
WHERE name LIKE 'Se_en';

-- LIKE with percent (%): Matches zero or more characters
-- This finds movies starting with "The " followed by anything
SELECT * 
FROM movies
WHERE name LIKE 'The %';

-- More LIKE pattern examples:

-- Movies ending with "man" (like "Batman", "Superman")
SELECT * FROM movies WHERE name LIKE '%man';

-- Movies containing "the" anywhere in the title
SELECT * FROM movies WHERE name LIKE '%the%';

-- Movies with exactly 5 characters
SELECT * FROM movies WHERE name LIKE '_____';

-- Case-insensitive search (SQLite is case-insensitive by default for LIKE)
SELECT * FROM movies WHERE name LIKE '%MATRIX%';

-- ================================
-- SECTION 5: LOGICAL OPERATORS - AND, OR, NOT
-- ================================

-- AND: Both conditions must be true
-- Find horror movies released before 1985
SELECT *
FROM movies
WHERE year < 1985
   AND genre = 'horror';

-- Since we don't have horror movies before 1985, let's try thriller movies before 2000
SELECT *
FROM movies
WHERE year < 2000
   AND genre = 'thriller';

-- Checkpoint 1: OR - Either condition can be true
-- Find movies after 2014 OR action movies (or both)
SELECT *
FROM movies
WHERE year > 2014
   OR genre = 'action';

-- Checkpoint 2: Multiple OR conditions
-- Find romance OR comedy movies
SELECT *
FROM movies
WHERE genre = 'romance'
   OR genre = 'comedy';

-- More logical operator examples:

-- AND with multiple conditions: High-rated recent movies
SELECT * FROM movies 
WHERE year > 2000 
   AND imdb_rating > 8.5 
   AND genre = 'action';

-- NOT operator: Movies that are NOT comedies
SELECT * FROM movies WHERE NOT genre = 'comedy';

-- Complex combinations with parentheses for clarity
SELECT * FROM movies 
WHERE (genre = 'action' OR genre = 'thriller') 
   AND year > 1990;

-- ================================
-- SECTION 6: SORTING WITH ORDER BY
-- ================================

-- ORDER BY: Sort results in ascending or descending order
-- Sort by IMDB rating from highest to lowest (DESC = descending)
SELECT name, year, imdb_rating
FROM movies
ORDER BY imdb_rating DESC;

-- Additional ORDER BY examples:

-- Sort by year (oldest first) - ASC is default
SELECT name, year FROM movies ORDER BY year;
SELECT name, year FROM movies ORDER BY year ASC;  -- Same as above

-- Sort by multiple columns: first by genre, then by rating within each genre
SELECT name, genre, imdb_rating 
FROM movies 
ORDER BY genre, imdb_rating DESC;

-- Sort by year descending (newest first)
SELECT name, year FROM movies ORDER BY year DESC;

-- ================================
-- SECTION 7: LIMITING RESULTS
-- ================================

-- LIMIT: Restrict the number of rows returned
-- Get the top 3 highest-rated movies
SELECT *
FROM movies
ORDER BY imdb_rating DESC
LIMIT 3;

-- More LIMIT examples:

-- Get the 5 most recent movies
SELECT name, year FROM movies ORDER BY year DESC LIMIT 5;

-- Get the worst-rated movie
SELECT name, imdb_rating FROM movies ORDER BY imdb_rating ASC LIMIT 1;

-- OFFSET with LIMIT: Skip first 3 results, then get next 5
-- Useful for pagination
SELECT name, imdb_rating 
FROM movies 
ORDER BY imdb_rating DESC 
LIMIT 5 OFFSET 3;

-- ================================
-- SECTION 8: CONDITIONAL LOGIC WITH CASE
-- ================================

-- CASE: Create conditional logic similar to if-else statements
-- Categorize movies by their genre into "mood" categories
SELECT name,
 CASE
  WHEN genre = 'romance' THEN 'Chill'
  WHEN genre = 'comedy'  THEN 'Chill'
  ELSE 'Intense'
 END AS 'Mood'
FROM movies;

-- More CASE examples:

-- Categorize movies by rating
SELECT name, imdb_rating,
 CASE
  WHEN imdb_rating >= 9.0 THEN 'Masterpiece'
  WHEN imdb_rating >= 8.0 THEN 'Excellent'
  WHEN imdb_rating >= 7.0 THEN 'Good'
  WHEN imdb_rating >= 6.0 THEN 'Average'
  ELSE 'Poor'
 END AS rating_category
FROM movies
ORDER BY imdb_rating DESC;

-- Categorize by decade
SELECT name, year,
 CASE
  WHEN year >= 2010 THEN '2010s+'
  WHEN year >= 2000 THEN '2000s'
  WHEN year >= 1990 THEN '1990s'
  ELSE 'Classic'
 END AS decade
FROM movies
ORDER BY year DESC;

-- Complex CASE with multiple conditions
SELECT name, genre, year,
 CASE
  WHEN genre = 'action' AND year > 2000 THEN 'Modern Action'
  WHEN genre = 'action' AND year <= 2000 THEN 'Classic Action'
  WHEN genre IN ('romance', 'comedy') THEN 'Feel Good'
  WHEN imdb_rating < 5.0 THEN 'Skip It'
  ELSE 'Worth Watching'
 END AS recommendation
FROM movies;

-- ================================
-- SECTION 9: AGGREGATE FUNCTIONS
-- ================================

-- MIN: Find the lowest IMDB rating
SELECT MIN(imdb_rating) AS lowest_rating FROM movies;

-- MAX: Find the highest IMDB rating
SELECT MAX(imdb_rating) AS highest_rating FROM movies;

-- AVG: Calculate average IMDB rating
SELECT AVG(imdb_rating) AS average_rating FROM movies;

-- SUM: Total of all ratings (not very meaningful, but demonstrates SUM)
SELECT SUM(imdb_rating) AS total_ratings FROM movies;

-- COUNT with conditions: How many movies have rating above 8?
SELECT COUNT(*) AS high_rated_movies 
FROM movies 
WHERE imdb_rating > 8.0;

-- ================================
-- SECTION 10: GROUP BY AND HAVING
-- ================================

-- GROUP BY: Group rows that have the same values
-- Count movies by genre
SELECT genre, COUNT(*) AS movie_count
FROM movies
GROUP BY genre
ORDER BY movie_count DESC;

-- Average rating by genre
SELECT genre, AVG(imdb_rating) AS avg_rating, COUNT(*) AS movie_count
FROM movies
GROUP BY genre
ORDER BY avg_rating DESC;

-- HAVING: Filter groups (like WHERE but for groups)
-- Only show genres with more than 1 movie
SELECT genre, COUNT(*) AS movie_count
FROM movies
GROUP BY genre
HAVING COUNT(*) > 1
ORDER BY movie_count DESC;

-- ================================
-- SECTION 11: ADVANCED EXAMPLES
-- ================================

-- Combine multiple concepts: Find top-rated movie from each decade
SELECT decade, name, year, imdb_rating
FROM (
  SELECT name, year, imdb_rating,
    CASE
      WHEN year >= 2010 THEN '2010s+'
      WHEN year >= 2000 THEN '2000s'
      WHEN year >= 1990 THEN '1990s'
      ELSE 'Earlier'
    END AS decade,
    ROW_NUMBER() OVER (
      PARTITION BY 
        CASE
          WHEN year >= 2010 THEN '2010s+'
          WHEN year >= 2000 THEN '2000s'
          WHEN year >= 1990 THEN '1990s'
          ELSE 'Earlier'
        END 
      ORDER BY imdb_rating DESC
    ) AS rank
  FROM movies
) ranked
WHERE rank = 1;

-- ================================
-- SECTION 12: PRACTICAL EXERCISES
-- ================================

-- Exercise 1: Find all action movies from the 2000s with rating above 8
SELECT name, year, imdb_rating
FROM movies
WHERE genre = 'action'
  AND year BETWEEN 2000 AND 2009
  AND imdb_rating > 8.0;

-- Exercise 2: Get movie statistics summary
SELECT 
  COUNT(*) AS total_movies,
  MIN(year) AS earliest_year,
  MAX(year) AS latest_year,
  MIN(imdb_rating) AS lowest_rating,
  MAX(imdb_rating) AS highest_rating,
  AVG(imdb_rating) AS average_rating
FROM movies;

-- Exercise 3: Find movies with titles containing numbers
SELECT name, year, imdb_rating
FROM movies
WHERE name LIKE '%1%' 
   OR name LIKE '%2%' 
   OR name LIKE '%3%' 
   OR name LIKE '%4%' 
   OR name LIKE '%5%' 
   OR name LIKE '%6%' 
   OR name LIKE '%7%' 
   OR name LIKE '%8%' 
   OR name LIKE '%9%' 
   OR name LIKE '%0%';

-- Final query: Show all data for reference
SELECT 'Total movies in database:' AS info, COUNT(*) AS count FROM movies
UNION ALL
SELECT 'This completes the SQLite tutorial!' AS info, 0 AS count;
