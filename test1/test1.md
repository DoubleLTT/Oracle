![](https://github.com/DoubleLTT/Oracle/blob/master/img3.JPG)
![](https://github.com/DoubleLTT/Oracle/blob/master/img2.JPG)
从查询时间来看，查询1的时间比查询2时间少，所以查询1优于查询2.

自定义代码如下：
'''
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT'，'Sales');
'''
