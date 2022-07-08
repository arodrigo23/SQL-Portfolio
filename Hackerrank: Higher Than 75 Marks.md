## Problem Statement
Query the Name of any student in STUDENTS who scored higher than 75 Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.
The Students table is described as follows:

![image](https://user-images.githubusercontent.com/104938319/178065081-1f857fca-ea6e-4638-b4ad-0d728c78a9be.png)

The Name column only contains uppercase (A-Z) and lowercase (a-z) letters.

## Solution
```sql
SELECT name FROM students WHERE marks > 75 ORDER BY RIGHT(name, 3), id;
```
