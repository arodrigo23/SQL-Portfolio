## Problem Statement
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
The STATION table is described as follows:

![image](https://user-images.githubusercontent.com/104938319/178064458-b35915eb-7030-4b16-98c5-15e34128ef36.png)

where LAT_N is the northern latitude and LONG_W is the western longitude.

## Solution
```sql
SELECT city, LENGTH(city) FROM station ORDER BY LENGTH(city), city LIMIT 1;
SELECT city, LENGTH(city) FROM station ORDER BY LENGTH(city) DESC, city LIMIT 1;
```
