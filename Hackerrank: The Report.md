# Problem Statement:
You are given two tables: Students and Grades. Students contains three columns: ID, Name, and Marks. 
Grades contains the following data:

Grade | Min_Mark | Max_Mark
------|----------|----------
 1    |    0     |   9
 2    |   10     |  19
 3    |   20     |  29
 4    |   30     |  39
 5    |   40     |  49
 6    |   50     |  59
 7    |   60     |  69
 8    |   70     |  79  
 9    |   80     |  89
 10   |   90     |  99
 
 Ketty gives Eve a task to generate a report containing three columns: Name, Grade, and Mark. 
 Ketty doesn't want the names of those students who received a grade lower than 8. The report 
 must be in descending order by grade--i.e. higher grades are entered first. If there is more 
 than one student with the same grade (8-10) assigned to them, order those particular students 
 by their name alphabetically. Finally, if the grade is lower than 8, use 'NULL' as their name
 and list them by their grades in descending order. If there is more than one student with the
 same grade (1-7) assigned to them, order those particular students by their marks in ascending
 order.
 
 ```sql
 SELECT 
    IF (Grades.Grade < 8, 'NULL', Students.Name)
    Grades.Grade
    Students.Marks
  FROM Students
  JOIN Grades
  ON Students.Marks BETWEEN Grades.Min_Mark AND Grades.Max_Mark
  ORDER BY Grades.Grade DESC, Students.Name
  ;
```
