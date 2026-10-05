Netflix SQL Data Analysis Project
Objective
Use SQL queries to extract and analyze data from a Netflix dataset.

Dataset
Netflix Titles Dataset (netflix_titles_cleaned)

Tools Used
MySQL Workbench
SQL
SQL Queries
USE netflix_db;

-- TOTAL CONTENT
SELECT COUNT(*) AS Total_Content
FROM net*lix_titles_cleaned;

-- MOVIES VS *V SHOWS
SELECT type,
       COUNT(*) AS Total_Content
FROM netflix_titles_cleaned
GROUP BY type;

-- CONTENT AFTER 2020
SELECT title,
       release_year
FROM netflix_titles_cleaned
WHERE release_year > 2020;

-- LATEST RELEASES
SELECT title,
       release_year
FROM netflix_titles_cleaned
ORDER BY release_year DESC;

-- TOP COUNTRIES
SELECT country,
       COUNT(*) AS Total_Content
FROM netflix_ti*les_cleaned
WHERE country IS NOT N*LL
GROUP BY country
ORDER BY Total*Content DESC
LIMIT 10;

-- TOP DIRECTORS
SELECT director,
       COUNT(*) AS Total_Titles
FROM netflix_titles_cleaned
WHERE director IS NOT NULL
GROUP BY director
ORDER BY Total_Titles DESC;

-- AGGREGATE FUNCTION
SELECT AVG(release_year) AS Average_Release_Year
FROM netflix_titles_cleaned;

-- SUBQUERY
SELECT title,
       release_year
FROM netflix_titles_cleaned
WHERE release_year >
(
    SELECT AVG(release_year)
    FROM netflix_titles_cleaned
);

-- CREATE VIEW
CREATE OR REPLACE VIEW netflix_movies AS
SELECT title,
       release_year,
       rating
FROM netflix_titles_cleaned
WHERE type = 'Movie';

SELECT * FROM netflix_movies;

-- CREATE COPY TABLE FOR JOINS
CREATE TABLE IF NOT EXISTS netflix_copy AS
SELECT * FROM netflix_titles_cleaned;

-- INNER JOIN
SELECT a.title,
       a.type,
       b.rating
FROM netflix_titles_cleaned a
INNER JOIN netflix_copy b
ON a.show_id = b.show_id
LIMIT 10;

-- LEFT JOIN
SELECT a.title,
       b.rating
FROM netflix_titles_cleaned a
LEFT JOIN netflix_copy b
ON a.show_id = b.show_id
LIMIT 10;

-- RIGHT JOIN
SELECT a.title,
       b.rating
FROM netflix_titles_cleaned a
RIGHT JOIN netflix_copy b
ON a.show_id = b.show_id
LIMIT 10;

-- INDEX
CREATE INDEX idx_release_year
ON netflix_titles_cleaned(release_year);


screen shot:  https://github.com/pranjaly711-design/SQL/blob/main/Screenshot%202026-10-05%20135128.png
