## Problem Statement
Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.

![image](https://user-images.githubusercontent.com/104938319/178064819-3afd0d01-0f11-4f3a-a181-9ab2b57d3b4b.png)

where LAT_N is the northern latitude and LONG_W is the western longitude.

## Solution
```sql
SELECT DISTINCT city FROM station WHERE LEFT(city, 1) IN ('a', 'e', 'i', 'o', 'u') AND RIGHT(city, 1) IN ('a', 'e', 'i', 'o', 'u');
```
