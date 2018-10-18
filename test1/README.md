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
![执行结果图片](./1_1.png)<br>
执行计划：<br><br>
![执行结果图片](./1_2.png)
![执行结果图片](./1_3.png)

分析执行计划：<br>
  计划有EXPLAIN PLAN，Predicate Information等。其中EXPLAIN PLAN（执行计划）的输出是一个表，属性有ID、Operation、Name、Rows、Bytes、Cost(%CPU)和Time。当前的Cost值为5。<br>

得到的优化指导结果：<br><br>
![执行结果图片](./3_1.png)
![执行结果图片](./3_2.png)
系统所给建议：<br>
![执行结果图片](./3_3.png)

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

![执行结果图片](./2_1.png)<br>
执行计划：<br><br>
![执行结果图片](./2_2.png)
![执行结果图片](./2_3.png)

分析执行计划：<br>
  计划同查询1一样。当前的Cost值为7。<br>
  
得到的优化指导结果：<br><br>
![执行结果图片](./4_1.png)
第二个查询系统没有给出建议。

结论：<br>
  就目前而言，第一个查询consistent gets值为10，第二个为9，第二个优于第一个；第一个cost值为5，第二个为7，第一个优于第二个。不知道physical reads。<br>
  无法用公式确切判断哪个更优化。但是第一个系统给出了优化建议，所以综合判断查询2更优化。<br>
 （尽量避免语句做全盘扫描。对于全盘扫描的语句，应增加相关的索引，优化SQL语句来解决。）
