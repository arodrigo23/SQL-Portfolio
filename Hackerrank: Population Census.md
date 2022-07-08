## Problem Statement
Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.
Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

The CITY and COUNTRY tables are described as follows:

![image](https://user-images.githubusercontent.com/104938319/178065513-4cf967db-f6ee-4516-a51c-5cad3291621d.png)

![image](https://user-images.githubusercontent.com/104938319/178065521-ed4ad620-9cdb-4aaf-b8c2-008517177b00.png)

## Solution
```sql
SELECT SUM(city.population) 
    FROM city
    JOIN country
    ON city.countrycode = country.code
    WHERE country.continent = 'Asia'
    ;
```
