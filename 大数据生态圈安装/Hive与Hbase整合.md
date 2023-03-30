### Hive与Hbase整合

#### 1 修改hive-site.xml配置文件

打开配置文件

```shell
vi hive-site.xml
```

添加以下配置内容

```xml
  <property>
    <name>hbase.master</name>
    <value>master:60000</value>
  </property>
  <property>
    <name>hbase.zookeeper.property.clientPort</name>
    <value>2181</value>
  </property>
  <property>
    <name>hive.zookeeper.quorum</name>
    <value>master,slave1,slave2</value>
  </property>
  <property>
    <name>hbase.zookeeper.quorum</name>
    <value>master,slave1,slave2</value>
  </property>

```

![image-20221213200525328](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213200525328.png)

#### 2 修改hive-env.sh配置文件

~~~shell
vi /usr/local/app/hive-1.2.1/conf/hive-env.sh
~~~

添加以下内容

```shell
export HADOOP_HOVE=/usr/local/app/hadoop-2.7.2
export HIVE_CONF_DIR=/usr/local/app/hive-1.2.1/conf
export HBASE_HOVE=/usr/local/app/hbase-1.2.1


```

![image-20221213200709826](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213200709826.png)

#### 3 拷贝hbase的五个依赖jar包到hive的lib目录下

将我们HBase的五个jar包拷贝到hive的lib目录下
hbase的jar包都在/export/servers/hbase-1.2.0-cdh5.14.0/lib
我们需要拷贝五个jar包名字如下
hbase-client-1.2.0-cdh5.14.0.jar
hbase-hadoop2-compat-1.2.0-cdh5.14.0.jar
hbase-hadoop-compat-1.2.0-cdh5.14.0.jar
hbase-it-1.2.0-cdh5.14.0.jar
hbase-server-1.2.0-cdh5.14.0.jar

~~~shell
[root@master lib]# cp /usr/local/app/hbase-1.2.1/lib/hbase-client-1.2.1.jar /usr/local/app/hive-1.2.1/lib/
[root@master lib]# cp /usr/local/app/hbase-1.2.1/lib/hbase-hadoop2-compat-1.2.1.jar /usr/local/app/hive-1.2.1/lib/
[root@master lib]# cp /usr/local/app/hbase-1.2.1/lib/hbase-hadoop-compat-1.2.1.jar /usr/local/app/hive-1.2.1/lib/
[root@master lib]# cp /usr/local/app/hbase-1.2.1/lib/hbase-it-1.2.1.jar /usr/local/app/hive-1.2.1/lib/
[root@master lib]# cp /usr/local/app/hbase-1.2.1/lib/hbase-server-1.2.1.jar /usr/local/app/hive-1.2.1/lib/

~~~



![image-20221213201520865](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213201520865.png)

#### 4 启动集群

启动zookeeper

![image-20221213201926264](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213201926264.png)

启动hadoop

![image-20221213210118983](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213210118983.png)

启动hbase

![image-20221213201943497](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213201943497.png)

![image-20221214104145456](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221214104145456.png)

启动hive

![image-20221213202827644](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213202827644.png)

#### 5 测试

1.HBase当中创建表并手动插入加载一些数据

进入HBase的shell客户端，手动创建一张表，并插入加载一些数据进去

```shell
create 'hbase_hive_score',{ NAME =>'cf'}

put 'hbase_hive_score','1','cf:name','zhangsan'
put 'hbase_hive_score','1','cf:score', '95'

put 'hbase_hive_score','2','cf:name','lisi'
put 'hbase_hive_score','2','cf:score', '96'

put 'hbase_hive_score','3','cf:name','wangwu'
put 'hbase_hive_score','3','cf:score', '97'


```

![image-20221213205711139](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213205711139.png)

2.建立hive的外部表，映射HBase当中的表以及字段

在hive当中建立外部表，
进入hive客户端，然后执行以下命令进行创建hive外部表，就可以实现映射HBase当中的表数据

```shell
CREATE external TABLE course.hbase2hive(id int, name string, score int) STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler' WITH SERDEPROPERTIES ("hbase.columns.mapping" = ":key,cf:name,cf:score") TBLPROPERTIES("hbase.table.name" ="hbase_hive_score");

```

![image-20221213205548907](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213205548907.png)

查看hive中数据

![image-20221213205945060](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213205945060.png)



























1.hive当中建表，进入hive客户端

创建hive数据库与hive对应的数据库表

~~~shell
create database course;
use course;
create external table if not exists course.score(id int,cname string,score int) row format delimited fields terminated by '\t' stored as textfile ;

~~~

![image-20221213203320942](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213203320942.png)

准备数据内容如下

```shell
cd /export/
vim hive-hbase.txt
```

加载数据格式如下

~~~shell
1	zhangsan	80
2	lisi	60
3	wangwu	30
4	zhaoliu	70
~~~

进行加载数据
进入hive客户端进行加载数据

~~~shell
hive (course)> load data local inpath '/export/hive-hbase.txt' into table score;
hive (course)> select * from score;

~~~

![image-20221213203505289](Hive%E4%B8%8EHbase%E6%95%B4%E5%90%88.assets/image-20221213203505289.png)

2.创建hive管理表与HBase进行映射

我们可以创建一个hive的管理表与hbase当中的表进行映射，hive管理表当中的数据，都会存储到hbase上面去
hive当中创建内部表

~~~shell
create table course.hbase_score(id int,cname string,score int) 
stored by 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'  
with serdeproperties("hbase.columns.mapping" = "cf:name,cf:score") 
tblproperties("hbase.table.name" = "hbase_score");

~~~

通过insert overwrite select 插入数据

~~~shell
insert overwrite table course.hbase_score select id,cname,score from course.score;

~~~

3.hbase当中查看表hbase_score

进入hbase的客户端查看表hbase_score，并查看当中的数据

~~~shell
hbase(main):023:0> list
TABLE                                                                                       
hbase_score                                                                                 
myuser                                                                                      
myuser2                                                                                     
student                                                                                     
user                                                                                        
5 row(s) in 0.0210 seconds

=> ["hbase_score", "myuser", "myuser2", "student", "user"]
hbase(main):024:0> scan 'hbase_score'
ROW                      COLUMN+CELL                                                        
 1                       column=cf:name, timestamp=1550628395266, value=zhangsan            
 1                       column=cf:score, timestamp=1550628395266, value=80                 
 2                       column=cf:name, timestamp=1550628395266, value=lisi                
 2                       column=cf:score, timestamp=1550628395266, value=60                 
 3                       column=cf:name, timestamp=1550628395266, value=wangwu              
 3                       column=cf:score, timestamp=1550628395266, value=30                 
 4                       column=cf:name, timestamp=1550628395266, value=zhaoliu             
 4                       column=cf:score, timestamp=1550628395266, value=70                 
4 row(s) in 0.0360 seconds


~~~

