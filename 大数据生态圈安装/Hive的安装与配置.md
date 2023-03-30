## Hive的安装与配置

### 1 Hive的上传与解压

1. Hive安装包的上传

![image-20221114191056128](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114191056128.png)

2. Hive安装包的解压

```shell
tar -zxvf apache-hive-1.2.1-bin.tar.gz
```

![image-20221114191317081](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114191317081.png)

### 2 在MySQL中添加Hive信息

1. 启动并查看MySQL服务

~~~shell
[root@master app]# systemctl start mysql
[root@master app]# systemctl status mysql
~~~

![image-20221114192442052](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114192442052.png)

2. 登录到MySQL数据库中

```shell
[root@master app]# /usr/local/app/mysql/bin/mysql -uroot -p
```

![image-20221114192604365](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114192604365.png)

3. 创建hive数据库，用来保存Hive元数据

```mysql
create database hive DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
```

![image-20221114192810238](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114192810238.png)

查看数据

```mysql
mysql> show databases;
```

![image-20221114192842493](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114192842493.png)

4. 创建访问Hive数据库的用户，并授予访问权限

```mysql
mysql> grant all on hive.* to 'hive'@'%'IDENTIFIED BY 'hive';
mysql> grant all on hive.* to 'hive'@'master'IDENTIFIED BY 'hive';
mysql> grant all on hive.* to 'hive'@'localhost'IDENTIFIED BY 'hive';
```

![image-20221114193155667](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114193155667.png)

### 3 配置Hive

1. 配置环境变量

```shell
vim /etc/profile.d/mycluster.sh
```

- 添加以下配置信息

```shell
export HIVE_HOME=/usr/local/app/hive-1.2.1
export PATH=$PATH:$HIVE_HOME/bin
```

![image-20221114193446814](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114193446814.png)

- 让配置文件立即生效

```shell
source /etc/profile.d/mycluster.sh
```

2. 修改hive的相关配置

- 进入hive/conf目录下根据模板hive-env.sh和hive-site.xml文件

```shell
cd /usr/local/app/hive-1.2.1/conf/
```

![image-20221114193941659](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114193941659.png)

- 将文件拷贝重命名即可

①hive-env.sh创建与配置

```shell
cp hive-env.sh.template hive-env.sh
```

![image-20221114194444282](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114194444282.png)

修改hive-env.sh配置文件

```shell
vim hive-env.sh
```

添加以下内容

```sh
export HADOOP_HOVE=/usr/local/app/hadoop-2.7.2
export HIVE_CONF_DIR=/usr/local/app/hive-1.2.1/conf
```

![image-20221115091047036](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115091047036.png)

②hive-site.xml创建与配置

默认情况下，该文件并不存在，此配置文件非常重要，若有一项配置错误，则hive将运行不了，直接创建后添加内容即可

```shell
vim hive-site.xml
```

![image-20221114195027854](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114195027854.png)

hive-site.xml的内容如下

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
  <property>
    <name>javax.jdo.option.ConnectionURL</name>
    <value>jdbc:mysql://master:3306/hive?createDatabaseIfNotExist=true</value>
    <description>Jdbc 方式连接数据库</description>
  </property>
  <property>
    <name>javax.jdo.option.ConnectionDriverName</name>
    <value>com.mysql.jdbc.Driver</value>
    <description>Driver class name for a JDBC metastore 指定jdo驱动相关类</description>
  </property>
  <property>
    <name>javax.jdo.option.ConnectionUserName</name>
    <value>root</value>
    <description>访问数据库的用户名</description>
  </property>
  <property>
    <name>javax.jdo.option.ConnectionPassword</name>
    <value>linrushao</value>
    <description>连接hive数据库对应用户的密码</description>
  </property>
  <!--配置缓存目录-->
  <property>
    <name>hive.exec.local.scratchdir</name>
    <value>/usr/local/app/hive-1.2.1/iotmp</value>
  </property>
  <property>
    <name>hive.downloaded.resources.dir</name>
    <value>/usr/local/app/hive-1.2.1/iotmp</value>
  </property>
</configuration>
```

![image-20221114201909408](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114201909408.png)

![image-20221114201926472](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114201926472.png)

因为在hive-site.xml配置文件中设置了配置缓存目录iotmp，为防止找不到路径，故在配置的路径中创建此目录

```shell
mkdir /usr/local/app/hive-1.2.1/iotmp
```

![image-20221114202200137](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114202200137.png)

- 修改/usr/local/app/hive-1.2.1/bin/hive-config.sh文件

```shell
vim /usr/local/app/hive-1.2.1/bin/hive-config.sh
```

在此文件中添加以下内容

```sh
export JAVA_HOME=/usr/local/app/jdk1.8.0_162
export HIVE_HOME=/usr/local/app/hive-1.2.1
export HADOOP_HOME=/usr/local/app/hadoop-2.7.2
```

![image-20221114202558339](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114202558339.png)

### 4 添加MySQL的jar包依赖

- 因为Hive中使用了MySQL作为元数据存储方式，所以需要添加MySQL的驱动程序到Hive的lib目录下

- 下载mysql-connector-java-5.1.36-bin.jar文件，直接在[Maven Repository: mysql » mysql-connector-java » 5.1.36 (mvnrepository.com)](https://mvnrepository.com/artifact/mysql/mysql-connector-java/5.1.36)网址中下载即可

![image-20221114203310223](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114203310223.png)

- 将文件路径定位到/usr/local/app/hive-1.2.1/lib/中

```shell
cd /usr/local/app/hive-1.2.1/lib/
```

直接上传jar包即可

![image-20221114203537311](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114203537311.png)

### 5 启动Hive服务

1. 先启动Hadoop服务

使用脚本启动hadoop服务

```shell
hadoopcluster.sh start
jps
```

![image-20221114203954738](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114203954738.png)

2. 初次启动hive之前需要初始化数据库，以后就不需要了

初始化命令

```shell
schematool -dbType mysql -initSchema --verbose
```

| 参数      | 含义               |
| --------- | ------------------ |
| --verbose | 详细显示进行的步骤 |

![image-20221115085644107](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115085644107.png)

初始化成功

3. 启动元数据

```shell
hive --service metastore &
```

![image-20221115091228914](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115091228914.png)

查看hive进程

```shell
jps
```

![image-20221115091257814](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115091257814.png)

4. 连接hive数据库

```shell
/usr/local/app/hive-1.2.1/bin/hive
```

![image-20221115091433589](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115091433589.png)

### 6 测试Hive服务

1. 查看hive数据库

```mysql
hive> show databases;
```

![image-20221115091658993](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115091658993.png)

2. 创建数据库

```msyql
create database test;
```

![image-20221115091913350](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115091913350.png)

3. 使用数据库

```mysql
use test;
```

![image-20221115091922864](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115091922864.png)

4. 再次查看数据库

```mysql
show databases;
```

![image-20221115091939157](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115091939157.png)

5. 退出hive

```mysql
quit;
```

![image-20221115092038655](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115092038655.png)

6. 在HDFS中查看是否创建了相应的目录

- 利用命令行查看

```shell
hdfs dfs -ls -R /user
```

| 参数 | 含义                     |
| ---- | ------------------------ |
| -R   | 递归地显示子目录下的内容 |

![image-20221115092236116](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115092236116.png)

- 利用HDFS的web端查看

![image-20221115092526347](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115092526347.png)

可以看到在HDFS上的/user/hive/warehouse目录已经创建了hive中test表对应的test.db，说明Hadoop和Hive已经整合成功。

### 7 Hive的Shell基本操作

- 启动并连接hive数据库

~~~shell
bin/hive
~~~

![image-20221118175649394](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118175649394.png)

- 查看数据库

```mysql
show databases;
```

![image-20221118175816581](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118175816581.png)

- 打开test数据库

```mysql
use test;
```

![image-20221118175939805](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118175939805.png)





- 显示test数据库中的表

```mysql
show tables;
```

![image-20221118175953412](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118175953412.png)

- 创建一张表

```mysql
 create table student(id int,name string);
```

![image-20221118180352497](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118180352497.png)

- 查看表的结构

```mysql
desc student;
```

![image-20221118180416553](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118180416553.png)

- 向表中插入数据

```mysql
insert into student values(100,"zhangsan");
insert into student(id,name) values(1,"lisi");
```

![image-20221118180556735](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118180556735.png)

![image-20221118182014519](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118182014519.png)

- 查询表中的数据

```mysql
select * from student;
```

![image-20221118182032808](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118182032808.png)

- 把查询的结果插入到指定的本地下

```mysql
insert overwrite local directory '/home/student' row format delimited fields terminated by ' ' select * from student;
```

![image-20221118192136275](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118192136275.png)

![image-20221118192424316](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118192424316.png)

- 删除表

```mysql
drop table student;
```

![image-20221118192609089](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221118192609089.png)



### 8 异常处理

1. 初始化时报错

![image-20221114204251212](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114204251212.png)

原因：hive-site.xml配置文件有问题

在初始化的时候添加--verbose参数，显示详细的运行步骤，可以看到报错的原因

```shell
schematool -dbType mysql -initSchema --verbose
```

![image-20221114211133175](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221114211133175.png)

故障原因：hive配置文件hive-env.sh环境变量HIVE_CONF_DIR配置有误，没有指向正确的配置文件目录

故障处理：修改export HIVE_CONF_DIR=/usr/local/app/hive-1.2.1/conf，再次初始化成功

```sh
export HADOOP_HOVE=/usr/local/app/hadoop-2.7.2
export HIVE_CONF_DIR=/usr/local/app/hive-1.2.1/conf
```

![image-20221115085228305](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115085228305.png)

3. 因为hive原本只需要初始化一次就可以了，但是因为第一次初始化的时候报错生成了一个metastore_db文件

![image-20221115093438471](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115093438471.png)

所以在第二次初始化的时候，我们需要将这个metastore_db文件删除

```shell
rm -rf -r /usr/local/app/hive-1.2.1/metastore_db
```

在配置成功的前提下，再次初始化并成功后可以发现

![image-20221115093715973](Hive%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221115093715973.png)

并没有相应的metastore_db文件生成