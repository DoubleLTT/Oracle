## 实验一报告文档

1. ###实验内容：
      对Oracle12c中的HR人力资源管理系统中的表进行查询与分析，
      查询两个部门('IT'和'Sales')的部门总人数和平均工资。
2. ###实验过程：
 - 查询1截图

![查询1](https://github.com/DoubleLTT/Oracle/blob/master/img3.JPG)

 - 查询2截图

![查询2](https://github.com/DoubleLTT/Oracle/blob/master/img2.JPG)

3. ###实验结论：
      从查询时间来看，查询1用时0.032s,查询2用时0.06s,
      查询1的时间比查询2时间少，所以查询1优于查询2。
      均未给出优化建议。

4. ### 自定义代码：

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

分析：从employees表中查询部门名称，统计工作ID总和
