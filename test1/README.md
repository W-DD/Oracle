# 实验一
- 查询1
```sql
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
```
实验结果截图：<br><br>
![执行结果图片](./1_1.png)
通过sqldeveloper的优化指导工具进行优化指导得到：<br><br>
![执行结果图片](./1_3.png)
![执行结果图片](./1_4.png)
----------
- 查询2
```sql
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT'，'Sales');
```
实验结果截图：<br><br>
![执行结果图片](./1_2.png)
通过sqldeveloper的优化指导工具进行优化指导得到：<br><br>
![执行结果图片](./1_5.png)
![执行结果图片](./1_6.png)
