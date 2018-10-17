### 代码截图如下：
1. 查询1![查询1](https://github.com/DoubleLTT/Oracle/blob/master/img3.JPG)
2. 查询2![查询2](https://github.com/DoubleLTT/Oracle/blob/master/img2.JPG)

**结论：从查询时间来看，查询1的时间比查询2时间少，所以查询1优于查询2.**

### 自定义代码如下：

~~~sql
SELECT department_name, count(job_id) as "部门总人数", 
avg(salary) as "平均工资"
FROM hr.employees e
JOIN
(SELECT d.department_id, d.department_name
FROM hr.departments d
WHERE d.department_name in ('IT', 'Sales'))
USING (department_id)
GROUP BY department_name;
~~~
