## Задания на 3
## Task 1
```
SELECT * FROM students
```
![image](https://github.com/necessary22/db_practice/assets/93242683/80497ecb-7128-493b-9965-4302c1f4dd01)

## Task 2
```
SELECT firstname, lastname FROM students WHERE age > 21
```
![image](https://github.com/necessary22/db_practice/assets/93242683/e4281e14-d3a3-427f-a481-1d4b4006d03e)

## Task 3
```
SELECT coursename FROM courses
```
![image](https://github.com/necessary22/db_practice/assets/93242683/c32180d5-ddae-439e-9f56-e945b6e7b138)

## Task 4
```
SELECT firstname, lastname FROM students
WHERE studentid IN (SELECT studentid FROM studentcourses WHERE courseid = (SELECT courseid FROM courses WHERE coursename = 'Математика'))
```
![image](https://github.com/necessary22/db_practice/assets/93242683/a1a97dcc-9dfa-409c-8fdc-bd0492751cab)

## Task 5
```
SELECT firstname, lastname FROM students
WHERE studentid IN (SELECT studentid FROM studentcourses WHERE courseid = (SELECT courseid FROM courses WHERE coursename = 'История' AND  age = 20))
```
![image](https://github.com/necessary22/db_practice/assets/93242683/a0121078-f8af-4490-9a09-4df90eb3e17a)
## Task 6
