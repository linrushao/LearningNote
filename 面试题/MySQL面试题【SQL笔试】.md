# MySQL面试题

## 1 SQL笔试

Student(SID, Sname, Sage, Ssex) 学生表

Course(CID, Cname, TID) 课程表 

SC(SID, CID, score) 成绩表 

Teacher(TID, Tname) 教师表

![image-20230225093653600](MySQL%E9%9D%A2%E8%AF%95%E9%A2%98%E3%80%90SQL%E7%AC%94%E8%AF%95%E3%80%91.assets/image-20230225093653600.png)

创建表注意：1.课程从001开始 

问题： 

1、查询“001”课程比“002”课程成绩高的所有学生的学号；

```mysql
select a.SID 
from (
    select Sid,score 
    from SC 
    where CID='001') a,
    (select Sid,score                                             
     from SC where CID='002') b 
where a.score>b.score and a.Sid=b.Sid; 
```

2、查询平均成绩大于60分的同学的学号和平均成绩；

```mysql
select SID,avg(score) 
from sc 
group by SID 
having avg(score) >60;
```

3、查询所有同学的学号、姓名、选课数、总成绩； 

```mysql
select Student.SID,Student.Sname,count(SC.CID),sum(score) 
from Student 
left Outer join SC 
on Student.SID=SC.SID 
group by Student.SID,Sname 
```

4、查询姓“李”的老师的个数；

```mysql
select count(distinct(Tname)) 
from Teacher 
where Tname 
like '李%'; 
```

5、查询没学过“叶平”老师课的同学的学号、姓名；

     ```mysql
select Student.SID,Student.Sname 
from Student 
where SID not in (select distinct(SC.SID) 
                  from SC,Course,Teacher 
                  where SC.CID=Course.CID 
                  and Teacher.TID=Course.TID 
                  and Teacher.Tname='叶平');
     ```

6、查询学过“001”并且也学过编号“002”课程的同学的学号、姓名；

```mysql
select Student.SID,Student.Sname 
from Student,SC 
where Student.SID=SC.SID 
and SC.CID='001'and exists( 
    Select * 
    from SC as SC_2 
    where SC_2.SID=SC.SID 
    and SC_2.CID='002'); 
```

7、查询学过“叶平”老师所教的所有课的同学的学号、姓名；

```mysql
select SID,Sname 
from Student 
where SID in (select SID 
              from SC ,Course ,Teacher 
              where SC.CID=Course.CID and Teacher.TID=Course.TID and Teacher.Tname='叶平'
              group by SID 
              having count(SC.CID)=(select count(CID) 
                                    from Course,Teacher  
                                    where Teacher.TID=Course.TID and Tname='叶平'));
```

8、查询课程编号“002”的成绩比课程编号“001”课程低的所有同学的学号、姓名；

```mysql
Select SID,Sname from (
    select Student.SID,Student.Sname,score ,(
        select score 
        from SC SC_2 
        where SC_2.SID=Student.SID and SC_2.CID='002') score2 
                       from Student,SC where Student.SID=SC.SID and CID='001') S_2 where score2 <score; 
```

9、查询所有课程成绩小于60分的同学的学号、姓名；

```mysql
select SID,Sname 
from Student 
where SID not in (select Student.SID from Student,SC where S.SID=SC.SID and score>60); 
```

10、查询没有学全所有课的同学的学号、姓名； 

```mysql
select Student.SID,Student.Sname 
from Student,SC 
where Student.SID=SC.SID group by Student.SID,Student.Sname having count(CID) <(select count(CID) from Course); 
```

11、查询至少有一门课与学号为“1001”的同学所学相同的同学的学号和姓名；

```mysql
select SID,Sname from Student,SC where Student.SID=SC.SID and CID in select CID from SC where SID='1001'; 
```

12、查询至少学过学号为“001”同学所有一门课的其他同学学号和姓名；

```mysql
select distinct SC.SID,Sname 
from Student,SC 
where Student.SID=SC.SID and CID in (select CID from SC where SID='001'); 
```

13、把“SC”表中“叶平”老师教的课的成绩都更改为此课程的平均成绩； 

```mysql
update SC set score=(select avg(SC_2.score) 
                     from SC SC_2 
                     where SC_2.CID=SC.CID )
from Course,Teacher where Course.CID=SC.CID and Course.TID=Teacher.TID and Teacher.Tname='叶平'); 
```

14、查询和“1002”号的同学学习的课程完全相同的其他同学学号和姓名； 

```mysql
select SID from SC where CID in (select CID from SC where SID='1002') 
group by SID having count()=(select count() from SC where SID='1002');
```

15、删除学习“叶平”老师课的SC表记录； 

```mysql
delete SC 
from course ,Teacher 
where Course.CID=SC.CID and Course.TID= Teacher.TID and Tname='叶平';
```

16、向SC表中插入一些记录，这些记录要求符合以下条件：没有上过编号“003”课程的同学学号、2、 

  号课的平均成绩；

```mysql
Insert SC select SID,'002',(Select avg(score) 
                            from SC where CID='002') from Student where SID not in (Select SID from SC where CID='002'); 
```

17、按平均成绩从高到低显示所有学生的“数据库”、“企业管理”、“英语”三门的课程成绩，按如下形式显示：学生ID,,数据库,企业管理,英语,有效课程数,有效平均分 

```mysql
SELECT SID as 学生ID
,(SELECT score FROM SC WHERE SC.SID=t.SID AND CID='004') AS 数据库
,(SELECT score FROM SC WHERE SC.SID=t.SID AND CID='001') AS 企业管理
,(SELECT score FROM SC WHERE SC.SID=t.SID AND CID='006') AS 英语
,COUNT() AS 有效课程数, AVG(t.score) AS 平均成绩 
FROM SC AS t 
GROUP BY SID 
ORDER BY avg(t.score) 
```

18、查询各科成绩最高和最低的分：以如下形式显示：课程ID，最高分，最低分

```mysql
SELECT L.CID As 课程ID,L.score AS 最高分,R.score AS 最低分
FROM SC L ,SC AS R 
WHERE L.CID = R.CID and 
L.score = (SELECT MAX(IL.score) 
           FROM SC AS IL,Student AS IM 
           WHERE L.CID = IL.CID and IM.SID=IL.SID 
           GROUP BY IL.CID) 
AND 
R.Score = (SELECT MIN(IR.score) 
           FROM SC AS IR 
           WHERE R.CID = IR.CID 
           GROUP BY IR.CID 
          );
```

19、按各科平均成绩从低到高和及格率的百分数从高到低顺序 

```mysql
SELECT t.CID AS 课程号,max(course.Cname)AS 课程名,isnull(AVG(score),0) AS 平均成绩
,100  SUM(CASE WHEN isnull(score,0)>=60 THEN 1 ELSE 0 END)/COUNT() AS 及格百分数 
FROM SC T,Course 
where t.CID=course.CID 
GROUP BY t.CID 
ORDER BY 100  SUM(CASE WHEN isnull(score,0)>=60 THEN 1 ELSE 0 END)/COUNT() DESC 
```

20、查询如下课程平均成绩和及格率的百分数(用"1行"显示): 企业管理（001），马克思（002），OO&UML （003），数据库（004） 

```mysql
SELECT SUM(CASE WHEN CID ='001' THEN score ELSE 0 END)/SUM(CASE CID WHEN '001' THEN 1 ELSE 0 END) AS 企业管理平均分
,100  SUM(CASE WHEN CID = '001' AND score >= 60 THEN 1 ELSE 0 END)/SUM(CASE WHEN CID = '001' THEN 1 ELSE 0 END) AS 企业管理及格百分数
,SUM(CASE WHEN CID = '002' THEN score ELSE 0 END)/SUM(CASE CID WHEN '002' THEN 1 ELSE 0 END) AS 马克思平均分
,100  SUM(CASE WHEN CID = '002' AND score >= 60 THEN 1 ELSE 0 END)/SUM(CASE WHEN CID = '002' THEN 1 ELSE 0 END) AS 马克思及格百分数
,SUM(CASE WHEN CID = '003' THEN score ELSE 0 END)/SUM(CASE CID WHEN '003' THEN 1 ELSE 0 END) AS UML平均分
,100  SUM(CASE WHEN CID = '003' AND score >= 60 THEN 1 ELSE 0 END)/SUM(CASE WHEN CID = '003' THEN 1 ELSE 0 END) AS UML及格百分数
,SUM(CASE WHEN CID = '004' THEN score ELSE 0 END)/SUM(CASE CID WHEN '004' THEN 1 ELSE 0 END) AS 数据库平均分
,100  SUM(CASE WHEN CID = '004' AND score >= 60 THEN 1 ELSE 0 END)/SUM(CASE WHEN CID = '004' THEN 1 ELSE 0 END) AS 数据库及格百分数
FROM SC
```

21、查询不同老师所教不同课程平均分从高到低显示 

​     SELECT max(Z.TID) AS 教师ID,MAX(Z.Tname) AS 教师姓名,C.CID AS 课程ＩＤ,MAX(C.Cname) AS 课程名称,AVG(Score) AS 平均成绩

```mysql
FROM SC AS T,Course AS C ,Teacher AS Z 
where T.CID=C.CID and C.TID=Z.TID 
GROUP BY C.CID 
ORDER BY AVG(Score) DESC 
```

22、查询如下课程成绩第 3 名到第 6 名的学生成绩单：企业管理（001），马克思（002），UML （003），数据库（004） 

  [学生ID],[学生姓名],企业管理,马克思,UML,数据库,平均成绩

```mysql
SELECT DISTINCT top 3 
SC.SID As 学生学号, Student.Sname AS 学生姓名 , T1.score AS 企业管理,T2.score AS 马克思,T3.score AS UML, T4.score AS 数据库,
ISNULL(T1.score,0) + ISNULL(T2.score,0) + ISNULL(T3.score,0) + ISNULL(T4.score,0) as 总分
FROM Student,SC LEFT JOIN SC AS T1 
ON SC.SID = T1.SID AND T1.CID = '001' 
LEFT JOIN SC AS T2 
ON SC.SID = T2.SID AND T2.CID = '002' 
LEFT JOIN SC AS T3 
ON SC.SID = T3.SID AND T3.CID = '003' 
LEFT JOIN SC AS T4 
ON SC.SID = T4.SID AND T4.CID = '004' 
WHERE student.SID=SC.SID and 
ISNULL(T1.score,0) + ISNULL(T2.score,0) + ISNULL(T3.score,0) + ISNULL(T4.score,0) 
NOT IN 
(SELECT 
 DISTINCT 
 TOP 15 WITH TIES 
 ISNULL(T1.score,0) + ISNULL(T2.score,0) + ISNULL(T3.score,0) + ISNULL(T4.score,0) 
 FROM sc 
 LEFT JOIN sc AS T1 
 ON sc.SID = T1.SID AND T1.CID = 'k1' 
 LEFT JOIN sc AS T2 
 ON sc.SID = T2.SID AND T2.CID = 'k2' 
 LEFT JOIN sc AS T3 
 ON sc.SID = T3.SID AND T3.CID = 'k3' 
 LEFT JOIN sc AS T4 
 ON sc.SID = T4.SID AND T4.CID = 'k4' 
 ORDER BY ISNULL(T1.score,0) + ISNULL(T2.score,0) + ISNULL(T3.score,0) + ISNULL(T4.score,0) DESC);
```

23、统计列印各科成绩,各分数段人数:课程ID,课程名称,[100-85],[85-70],[70-60],[ <60] 

```mysql
SELECT SC.CID as 课程ID, Cname as 课程名称 
,SUM(CASE WHEN score BETWEEN 85 AND 100 THEN 1 ELSE 0 END) AS [100 - 85]
,SUM(CASE WHEN score BETWEEN 70 AND 85 THEN 1 ELSE 0 END) AS [85 - 70] 
,SUM(CASE WHEN score BETWEEN 60 AND 70 THEN 1 ELSE 0 END) AS [70 - 60] 
,SUM(CASE WHEN score < 60 THEN 1 ELSE 0 END) AS [60 -] 
FROM SC,Course 
where SC.CID=Course.CID 
GROUP BY SC.CID,Cname;
```

24、查询学生平均成绩及其名次 

```mysql
SELECT 1+(SELECT COUNT( distinct 平均成绩)
          FROM (SELECT SID,AVG(score) AS 平均成绩
                FROM SC 
                GROUP BY SID 
               ) AS T1 
          WHERE 平均成绩> T2.平均成绩) as 名次,
SID as 学生学号,平均成绩
FROM (SELECT SID,AVG(score) 平均成绩
      FROM SC 
      GROUP BY SID 
     ) AS T2 
ORDER BY 平均成绩desc; 
```

25、查询各科成绩前三名的记录:(不考虑成绩并列情况)

```mysql
SELECT t1.SID as 学生ID,t1.CID as 课程ID,Score as 分数
FROM SC t1 
WHERE score IN (SELECT TOP 3 score 
                FROM SC 
                WHERE t1.CID= CID 
                ORDER BY score DESC 
               ) 
ORDER BY t1.CID; 
```

26、查询每门课程被选修的学生数 

```mysql
 select Cid,count(SID) from sc group by CID; 
```

27、查询出只选修了一门课程的全部学生的学号和姓名 

```mysql
select SC.SID,Student.Sname,count(CID) AS 选课数
from SC ,Student 
where SC.SID=Student.SID group by SC.SID ,Student.Sname having count(CID)=1; 
```

28、查询男生、女生人数 

```mysql
Select count(Ssex) as 男生人数 from Student group by Ssex having Ssex='男';
Select count(Ssex) as 女生人数 from Student group by Ssex having Ssex='女'；
```

29、查询姓“张”的学生名单

```mysql
SELECT Sname FROM Student WHERE Sname like '张%';
```

30、查询同名同性学生名单，并统计同名人数 

```mysql
select Sname,count() from Student group by Sname having count()>1;
```

31、1981年出生的学生名单(注：Student表中Sage列的类型是datetime) 

```mysql
select Sname, CONVERT(char (11),DATEPART(year,Sage)) as age 
from student 
where CONVERT(char(11),DATEPART(year,Sage))='1981'; 
```

32、查询每门课程的平均成绩，结果按平均成绩升序排列，平均成绩相同时，按课程号降序排列 

```mysql
Select CID,Avg(score) from SC group by CID order by Avg(score),CID DESC ; 
```

33、查询平均成绩大于85的所有学生的学号、姓名和平均成绩 

```mysql
select Sname,SC.SID ,avg(score) 
from Student,SC 
where Student.SID=SC.SID group by SC.SID,Sname having  avg(score)>85; 
```

34、查询课程名称为“数据库”，且分数低于60的学生姓名和分数

```mysql
Select Sname,isnull(score,0) 
from Student,SC,Course 
where SC.SID=Student.SID and SC.CID=Course.CID and Course.Cname='数据库'and score <60; 
```

35、查询所有学生的选课情况； 

```mysql
SELECT SC.SID,SC.CID,Sname,Cname 
FROM SC,Student,Course 
where SC.SID=Student.SID and SC.CID=Course.CID ; 
```

36、查询任何一门课程成绩在70分以上的姓名、课程名称和分数；

```mysql
SELECT distinct student.SID,student.Sname,SC.CID,SC.score 
FROM student,Sc 
WHERE SC.score>=70 AND SC.SID=student.SID; 
```

37、查询不及格的课程，并按课程号从大到小排列 

```mysql
select Cid from sc where scor e <60 order by CID ; 
```

38、查询课程编号为003且课程成绩在80分以上的学生的学号和姓名；

```mysql
select SC.SID,Student.Sname from SC,Student where SC.SID=Student.SID and Score>80 and CID='003';
```

39、求选了课程的学生人数 

```mysql
select count() from sc; 
```

40、查询选修“叶平”老师所授课程的学生中，成绩最高的学生姓名及其成绩 

```mysql
select Student.Sname,score 
from Student,SC,CourseC,Teacher 
where Student.SID=SC.SID and SC.CID=C.CID and C.TID=Teacher.TID and Teacher.Tname='叶平' and SC.score=(select max(score)from SC where CID=C.CID );
```

41、查询各个课程及相应的选修人数 

```mysql
select count() from sc group by CID; 
```

42、查询不同课程成绩相同的学生的学号、课程号、学生成绩 

```mysql
 select distinct A.SID,B.score from SC A ,SC B where A.Score=B.Score and A.CID <>B.CID ;
```

43、查询每门功成绩最好的前两名 

```mysql
SELECT t1.SID as 学生ID,t1.CID as 课程ID,Score as 分数
FROM SC t1 
WHERE score IN (SELECT TOP 2 score 
                FROM SC 
                WHERE t1.CID= CID 
                ORDER BY score DESC 
               ) 
ORDER BY t1.CID; 
```

44、统计每门课程的学生选修人数（超过10人的课程才统计）。要求输出课程号和选修人数，查询结果按人数降序排列，查询结果按人数降序排列，若人数相同，按课程号升序排列 

```mysql
select CID as 课程号,count() as 人数 
from sc 
group by CID 
order by count() desc,Cid 
```

45、检索至少选修两门课程的学生学号 

```mysql
select SID 
from sc 
group by Sid 
having count() > = 2 
```

46、查询全部学生都选修的课程的课程号和课程名 

```mysql
select CID,Cname 
from Course 
where CID in (select Cid from sc group by Cid)
```

47、查询没学过“叶平”老师讲授的任一门课程的学生姓名

```mysql
select Sname from Student where SID not in (select SID from Course,Teacher,SC where Course.TID=Teacher.TID and SC.CID=course.CID and Tname='叶平'); 
```

48、查询两门以上不及格课程的同学的学号及其平均成绩 

```mysql
select SID,avg(isnull(score,0)) 
from SC 
where SID 
in (select SID from SC where score <60 group by SID having count()>2)
group by SID; 
```
