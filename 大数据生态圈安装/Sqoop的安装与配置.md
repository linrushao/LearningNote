## Sqoop的安装与配置

### 1 Sqoop的上传与解压

- Sqoop的上传

![image-20221119155452021](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119155452021.png)

- Sqoop的解压

```shell
tar -zxvf sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz
```

![image-20221119155559890](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119155559890.png)

- 重命名

```shell
mv sqoop-1.4.7.bin__hadoop-2.6.0/ sqoop-1.4.7
ll
```

![image-20221119160158495](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119160158495.png)

### 2 配置环境变量

- 打开etc/profile.d/目录

```shell
vim /etc/profile.d/mycluster.sh
```

- 在mycluster.sh中添加以下内容

```sh
# sqoop
export SQOOP_HOME=/usr/local/app/sqoop-1.4.7
export CLASSPATH=$CLASSPATH:$SQOOP_HOME/lib
export PATH=$PATH:${SQOOP_HOME}/bin
```

![image-20221119160500224](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119160500224.png)

- 使用环境变量生效

```shell
source /etc/profile.d/mycluster.sh
```

### 3 修改配置信息

- 切换到sqoop配置文件目录

```shell
cd /usr/local/app/sqoop-1.4.7/conf/
```

- 复制配置文件并重命名

```shell
[root@master conf]# cp sqoop-env-template.sh sqoop-env.sh
[root@master conf]# ll
```

![image-20221119161019346](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119161019346.png)

- 编辑配置文件

```shell
[root@master conf]# vim sqoop-env.sh
```

并加入以下内容

```sh
export HADOOP_COMMON_HOME=/usr/local/app/hadoop-2.7.2
export HADOOP_MAPRED_HOME=/usr/local/app/hadoop-2.7.2
export HBASE_HOME=/usr/local/app/hbase-1.2.1
export HIVE_HOME=/usr/local/app/hive-1.2.1
export HIVE_CONF_DIR=/usr/local/app/hive-1.2.1/conf
export ZOOCFGDIR=/usr/local/app/zookeeper-3.4.13
```

![image-20221119162447621](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119162447621.png)

### 4 整合Hive

- 加入mysql的jdbc驱动包

- 拷贝jdbc驱动到sqoop的lib目录下【从HIVE中复制MySQL连接驱动到$SQOOP_HOME/lib】

```shell
cp /usr/local/app/hive-1.2.1/lib/mysql-connector-java-5.1.36.jar /usr/local/app/sqoop-1.4.7/lib/
```

![image-20221119162903688](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119162903688.png)

- 创建hive配置文件的软连接【链接依赖】

```shell
ln -s /usr/local/app/hive-1.2.1/conf/hive-site.xml  /usr/local/app/sqoop-1.4.7/conf/hive-site.xml
```

![image-20221119163325990](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119163325990.png)

### 5 测试Sqoop

- 通过某一个command来验证sqoop配置是否正确

```shell
bin/sqoop help
```

![image-20221119163901783](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119163901783.png)

- 打印sqoop版本

```shell
sqoop version
```

![image-20221119163707264](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119163707264.png)

- 测试Sqoop是否能够成功连接数据库，执行下面令会列出所有mysql的所有数据库

```sql
sqoop list-databases  --connect jdbc:mysql://localhost:3306/  --username root --password linrushao
```

![image-20221119164156061](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119164156061.png)

### 6 数据的导入

- MySQL数据准备

```sql
// 创建脚本
[root@master testsqoop]# vim company.sql
create database company;
use company;
create table staff(id int(4) primary key not null auto_increment, name varchar(255), sex varchar(255));
insert into staff(name, sex) values('Thomas', 'Male');
insert into staff(name, sex) values('Catalina', 'FeMale');
insert into staff(name, sex) values('Thomas', 'Male');
insert into staff(name, sex) values('Catalina', 'FeMale');
insert into staff(name, sex) values('Thomas', 'Male');
insert into staff(name, sex) values('Catalina', 'FeMale');
insert into staff(name, sex) values('Thomas', 'Male');
insert into staff(name, sex) values('Catalina', 'FeMale');
insert into staff(name, sex) values('Catalina', 'FeMale');
insert into staff(name, sex) values('Thomas', 'Male');
insert into staff(name, sex) values('Catalina', 'FeMale');
insert into staff(name, sex) values('Thomas', 'Male');
insert into staff(name, sex) values('Catalina', 'FeMale');
insert into staff(name, sex) values('Thomas', 'Male');
insert into staff(name, sex) values('Catalina', 'FeMale');
```

- 登录数据库执行脚本

```sql
[root@master mysql]# bin/mysql -uroot -p
Enter password: linrushao
mysql> source /root/testsqoop/company.sql
```

![image-20221119165641093](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119165641093.png)

```mysql
mysql> show databases;
mysql> use company;
mysql> select * from staff;
```

![image-20221119165815050](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119165815050.png)

1. 启动需要的组件

- 启动zookeeper、Hadoop、HBase

![image-20221119170134788](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119170134788.png)

2. 从MySQL导入HDFS

- 全表导入

```sql
bin/sqoop import \
--connect jdbc:mysql://master:3306/company \
--username root \
--password linrushao \
--table staff \
--target-dir company \
--delete-target-dir \
--num-mappers 2 \
--split-by id \
--fields-terminated-by "\t"
```

运行成功

![image-20221119171412215](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119171412215.png)

在HDFS的web端查看

![image-20221119171458932](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119171458932.png)

下载数据并查看

![image-20221119171549477](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119171549477.png)

- 查询导入sqoop_query

```sql
bin/sqoop import \
--connect jdbc:mysql://master:3306/company \
--username root \
--password linrushao \
--target-dir company \
--delete-target-dir \
--num-mappers 2 \
--split-by id \
--fields-terminated-by "\t" \
--query 'select id,name from staff where $CONDITIONS'
```

运行结果

![image-20221119173330547](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119173330547.png)



HDFS的Web端查询

![image-20221119173244391](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119173244391.png)

下载并查看文件

![image-20221119173222979](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119173222979.png)

- 部分导入【根据条件查询导入】

```sql
bin/sqoop import \
--connect jdbc:mysql://master:3306/company \
--username root \
--password linrushao \
--table staff \
--columns id,name \
--where 'id>=10 and id<=20' \
--target-dir company2 \
--delete-target-dir \
--num-mappers 2 \
--split-by id \
--fields-terminated-by "\t"
```

运行结果

![image-20221119180434497](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119180434497.png)

HDFS的Web端查看

![image-20221119180511523](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119180511523.png)

下载文件并查看

![image-20221119180545545](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119180545545.png)

2. 从MySQL导入到Hive

```sql
bin/sqoop import \
--connect jdbc:mysql://master:3306/company \
--username root \
--password linrushao \
--hive-import \
--hive-overwrite \
--hive-table staff_hive \
--target-dir company \
--delete-target-dir \
--num-mappers 2 \
--split-by id \
--fields-terminated-by "\t" \
--query 'select * from staff where $CONDITIONS'
```

**注意**：该过程分为两步，第一步将数据导入到HDFS，第二步将导入到HDFS的数据迁移到Hive仓库，第一步默认的临时目录是/user/bigdata/表名

如果运行成功结果如图：

![image-20221119191921126](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119191921126.png)

第一步：先从MySQL到HDFS

![image-20221119191844352](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119191844352.png)

第二步：再从HDFS到Hive

![image-20221119191948210](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119191948210.png)

启动hive并查看是否成功

```sql
[root@master sqoop-1.4.7]# cd ../hive-1.2.1/
[root@master hive-1.2.1]# bin/hive
hive> show tables;
hive> select * from staff_hive;
```

![image-20221119192227344](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119192227344.png)

3. 从MySQL导入到HBase

- 导入之前现在HBase中创建相应的表【避免报错】

```sql
hbase(main):001:0> create 'staff_hbase','info'
hbase(main):002:0> list
```

![image-20221119192855447](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119192855447.png)

- 执行导入命令

```mysql
bin/sqoop import \
--connect jdbc:mysql://master:3306/company \
--username root \
--password linrushao \
--hbase-table staff_hbase \
--hbase-row-key "id" \
--column-family "info" \
--target-dir company \
--delete-target-dir \
--num-mappers 2 \
--split-by id \
--fields-terminated-by "\t" \
--query 'select * from staff where $CONDITIONS'
```

运行结果

![image-20221119193151199](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119193151199.png)

在HBase中查看结果

```sql
scan 'staff_hbase'
```

![image-20221119193233052](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119193233052.png)

### 7 数据的导出

> 在Sqoop中，“导出”概念指：从大数据集群（HDFS，HIVE，HBASE）向非大数据集群（RDBMS）中传输数据，叫做：导出，即使用export关键字

1. HIVE/HDFS到MySQL

**注意**：Mysql中如果表不存在，不会自动创建

- 先清空MySQL的staff表中数据

```mysql
mysql> use company;
mysql> show tables;
mysql> truncate table staff;
mysql> select * from staff;
```

![image-20221119194030104](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119194030104.png)

- 运行sqoop脚本

```sql
bin/sqoop export \
--connect jdbc:mysql://master:3306/company \
--username root \
--password linrushao \
--table staff \
--num-mappers 2 \
--export-dir /user/hive/warehouse/staff_hive \
--input-fields-terminated-by "\t"
```

运行结果

![image-20221119194322375](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119194322375.png)

- 在MySQL中查看数据

```mysql
select * from staff;
```

![image-20221119194403238](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119194403238.png)

### 8 脚本打包

- 使用opt格式的文件打包sqoop命令，然后执行

1. 创建一个.opt文件

~~~shell
vim opt.txt
~~~

![image-20221119194721823](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119194721823.png)

2.  编写sqoop脚本

添加以下内容

```shell
--connect
jdbc:mysql://master:3306/company
--username
root
--password
linrushao
```

3. 执行该脚本

```shell
bin/sqoop list-databases --options-file /root/testsqoop/opt.txt
```

![image-20221119194930217](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119194930217.png)

### 9 异常处理

1. 查询导入

![image-20221119172011649](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119172011649.png)

解决方法：因为我查询的时候是根据id切分的，但是没有查询id字段，所以添加id字段查询即可

![image-20221119172310196](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119172310196.png)

2. 导入数据时异常

![image-20221119170722646](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119170722646.png)

异常原因：root用户权限问题

解决方法：登录语句用导出数据的mysql数据库,运行授权语句.()

```mysql
grant all privileges on *.* to root@'%' identified by 'linrushao';
grant all privileges on *.* to root@'slave1' identified by 'linrushao';
grant all privileges on *.* to root@'slave2' identified by 'linrushao';
flush privileges;
```

![image-20221119175901906](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119175901906.png)

3. 从MySQL中导入Hive中异常

![image-20221119181041388](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119181041388.png)

原因：环境变量设置错误

解决方法：在/etc/profile.d/mycluster.sh中添加环境变量

```shell
vim /etc/profile.d/mycluster.sh 
```

添加以下内容

```shell
# hadoop
export HADOOP_HOME=/usr/local/app/hadoop-2.7.2
export PATH=$PATH:$HADOOP_HOME/bin
export HADOOP_CLASSPATH=/usr/local/app/hadoop-2.7.2/lib
export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:/usr/local/app/hive-1.2.1/lib/*
```

![image-20221119191703084](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119191703084.png)

4. 从MySQL中导入数据到HBase中报错

![image-20221119192629529](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119192629529.png)

原因：sqoop1.4.7可能不支持Hbase自动创建HBase表的功能

解决方法：到HBase中创建一个表

![image-20221119192855447](Sqoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119192855447.png)



