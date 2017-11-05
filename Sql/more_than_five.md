## 题目
There is a table courses with columns: student and class

Please list out all classes which have more than or equal to 5 students.

For example, the table:

<pre>
+---------+------------+
| student | class      |
+---------+------------+
| A       | Math       |
| B       | English    |
| C       | Math       |
| D       | Biology    |
| E       | Math       |
| F       | Computer   |
| G       | Math       |
| H       | Math       |
| I       | Math       |
+---------+------------+
</pre>
should output
<pre>
+---------+
| class   |
+---------+
| Math    |
+---------+
</pre>

## 分析
表中的统计要使用`group by`和`having`

## 代码实现
``` sql
SELECT class
FROM courses
GROUP BY class HAVING COUNT(DISTINCT student)>4
```
