## 题目
Write a SQL query to get the second highest salary from the Employee table.

For example, given the above Employee table, the query should return 200 as the second highest salary. If there is no second highest salary, then the query should return null.

## 分析题目
排除第一大后，选取最大的sal

## 代码实现
``` SQL
# Write your MySQL query statement below
select max(Salary) as SecondHighestSalary from Employee where Salary < (select Max(Salary) from Employee)
```
