## NASA Astronauts Analysis
This project uses the Astronaut Yearbook dataset from Kaggle (kaggle.com/nasa/astronaut-yearbook) to answer questions about NASA astronauts.

```
CREATE TABLE astronauts(
   Name                TEXT PRIMARY KEY,
   Year                INTEGER,
   GroupNum            INTEGER,
   Status              TEXT,
   Birth_Date          TEXT,
   Birth_Place         TEXT,
   Gender              TEXT,
   Alma_Mater          TEXT,
   Undergraduate_Major TEXT,
   Graduate_Major      TEXT,
   Military_Rank       TEXT,
   Military_Branch     TEXT,
   Space_Flights       INTEGER,
   Space_Flight_hr     INTEGER,
   Space_Walks         INTEGER,
   Space_Walks_hr      REAL,
   Missions            TEXT,
   Death_Date          TEXT, 
   Death_Mission       TEXT
);

-- Add records to table. Here is an example of just adding one record:
INSERT INTO astronauts(Name,Year,GroupNum,Status,Birth_Date,Birth_Place,Gender,Alma_Mater,Undergraduate_Major,Graduate_Major,Military_Rank,Military_Branch,Space_Flights,Space_Flight_hr,Space_Walks,Space_Walks_hr,Missions,Death_Date,Death_Mission) VALUES ('Joseph M. Acaba',2004,19,'Active','5/17/1967','Inglewood, CA','Male','University of California-Santa Barbara; University of Arizona','Geology','Geology',NULL,NULL,2,3307,2,13,'STS-119 (Discovery), ISS-31/32 (Soyuz)',NULL,NULL);

-- View data
SELECT * FROM astronauts LIMIT 50;

-- Which astronaut has the most space flight hours?
SELECT Name, Space_Flight_hr 
FROM astronauts 
ORDER BY Space_Flight_hr DESC
LIMIT 1;

-- How many astronauts have engineering vs. non-engineering undergraduate degrees?
SELECT
    CASE
        WHEN Undergraduate_Major LIKE '%engineering%' THEN 'Engineering'
        ELSE 'Non-Engineering'
    END AS Undergrad_Major_Type,
    COUNT(*) AS COUNT
FROM astronauts
GROUP BY Undergrad_Major_Type;

-- How many male and female astronauts have engineering degrees vs. non-engineering degrees (undergraduate or graduate degree)?
SELECT
    CASE
        WHEN Undergraduate_Major LIKE '%engineering%' OR Graduate_Major LIKE '%engineering%' THEN 'Engineering'
        ELSE 'Non-Engineering'
    END AS Graduate_Major_Type,
    Gender,
    COUNT(*) AS COUNT
FROM astronauts
GROUP BY Graduate_Major_Type, Gender;

-- What is the average number of space flights for men and women?
SELECT 
    Gender,
    AVG(Space_Flights) AS avg_num_of_space_flights
FROM astronauts 
GROUP BY Gender;

-- How many astronauts come from each military branch?
SELECT 
    CASE 
        WHEN Military_Branch LIKE '%Army%' THEN 'Army'
        WHEN Military_Branch LIKE '%navy%' THEN 'Navy'
        WHEN Military_Branch LIKE '%air force%' THEN 'Air Force'
        WHEN Military_Branch LIKE '%marine%' THEN 'Marines'
        WHEN Military_Branch LIKE '%coast guard%' THEN 'Coast Guard'
        ELSE 'No Branch'
    END AS Branch,
    COUNT(*) AS Num_of_astronauts
FROM astronauts
GROUP BY Branch
LIMIT 5;

-- Which military branches gave rise to more than 50 astronauts?
SELECT 
    CASE 
        WHEN Military_Branch LIKE '%Army%' THEN 'Army'
        WHEN Military_Branch Like '%navy%' THEN 'Navy'
        WHEN Military_Branch Like '%air force%' THEN 'Air Force'
        WHEN Military_Branch Like '%marine%' THEN 'Marines'
        WHEN Military_Branch Like '%coast guard%' THEN 'Coast Guard'
        ELSE 'No Branch'
    END AS Branch,
    COUNT(*) AS Num_of_astronauts
FROM astronauts
GROUP BY Branch
HAVING Num_of_astronauts > 50;

-- How many female astronauts did more than 3 space walks?
SELECT COUNT(*)
FROM astronauts  
WHERE Space_Walks > 3 AND Gender = 'Female';
```
