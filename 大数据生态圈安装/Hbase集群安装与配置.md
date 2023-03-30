## Hbase集群安装与配置

### 1 HBase上传与解压

上传HBase文件压缩包并解压

```shell
tar -vzxf hbase-1.2.1-bin.tar.gz
```

![image-20221106104319664](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106104319664.png)

查看解压结果

~~~shell
ll
~~~

![image-20221106104359731](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106104359731.png)

### 2 修改配置文件

1. 修改hbase-env.sh文件

~~~shell
cd /usr/local/app/hbase-1.2.1/conf/
vi hbase-env.sh
~~~

export JAVA_HOME=/usr/local/java/jdk1.8.0_73，表示修改为自己的 jdk 目录

>Hbase其实自己带了zookeeper的jar包，它可以自己启动zookeeper
>这样的话就会跟我们自己单独部署的那个多种服务共用的zookeeper集群会产生冲突
>所以这里一般设置为false

export HBASE_MANAGES_ZK=false，表示不引用 hbase 自带的 zookeeper

显示行号

~~~shell
:set nu
~~~

修改27行左右的java环境变量

~~~shell
export JAVA_HOME=/usr/local/app/jdk1.8.0_162
~~~

![image-20221106105044202](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106105044202.png)

修改129行左右的是否引用hbase自带的zookeeper

~~~shell
export HBASE_MANAGES_ZK=false
~~~

![image-20221106105426783](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106105426783.png)

2. 修改hbase-site.xml文件

~~~shell
vi hbase-site.xml
~~~

配置内容

~~~xml
<configuration>
    <!--hbase存储在HADOOP HDFS上文件根目录路径-->
    <property>
        <name>hbase.rootdir</name>
        <value>hdfs://master:8020/hbase</value>        
    </property>
        <!--采用分布式模式-->
    <property>
        <name>hbase.cluster.distributed</name>
        <value>true</value>
    </property>
        <!--zookeeper地址，端口不指定的话就默认为2181-->
    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>master:2181,slave1:2181,slave2:2181</value>
    </property>  
</configuration>
~~~

![image-20221106110212492](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106110212492.png)

3. 修改 regionservers

> HRegionServer是HBase中最主要的组件，负责table数据的实际读写，管理Region。在分布式集群中,HRegionServer一般跟DataNode在同一个节点上，目的是实现数据的本地性，提高读写效率。

```shell
vi regionservers
```

![image-20221106120824411](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106120824411.png)

4. 修改 backup-masters（自行创建），指定备用的主节点 该文件是不存在的

```shell
 vi backup-masters
```

我们设置slave1作为备选Master节点

![image-20221106110457715](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106110457715.png)

5. 将hadoop的hdfs-site.xml与core-site.xml文件拷贝到hbase的conf目录下

~~~shell
cp -r /usr/local/app/hadoop-2.7.2/etc/hadoop/core-site.xml /usr/local/app/hbase-1.2.1/conf/
cp -r /usr/local/app/hadoop-2.7.2/etc/hadoop/hdfs-site.xml /usr/local/app/hbase-1.2.1/conf/
ls /usr/local/app/hbase-1.2.1/conf/
~~~

![image-20221106145908696](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106145908696.png)

### 3 配置环境变量

```shell
vim /etc/profile.d/mycluster.sh 
```

环境变量配置中添加以下内容

```sh
export HBASE_HOME=/usr/local/app/hbase-1.2.1
export PATH=$PATH:$HBASE_HOME/bin
```

让文件立即生效

```shell
source /etc/profile.d/mycluster.sh 
```

![image-20221106113900359](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106113900359.png)

### 4 分发文件

- 分发HBase文件

~~~shell
 scp -r /usr/local/app/hbase-1.2.1/ slave1:/usr/local/app/
 scp -r /usr/local/app/hbase-1.2.1/ slave2:/usr/local/app/
~~~

![image-20221106114731334](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106114731334.png)

- 分发环境变量

```shell
scp -r /etc/profile.d/mycluster.sh slave1:/usr/local/app/
scp -r /etc/profile.d/mycluster.sh slave2:/usr/local/app/
```

![image-20221106114941788](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106114941788.png)

- 在slave1、slave2中分别执行以下命令，让配置文件立即生效

```shell
 source /etc/profile.d/mycluster.sh
```



### 5 启动HBase服务

1. 启动HBase服务之前先要保证zookeeper和Hadoop启动完成

先启动zookeeper

~~~shell
zkServer.sh start
~~~

![image-20221106120120344](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106120120344.png)

2. 启动Hadoop集群

![image-20221106120227906](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106120227906.png)

3. 启动HBase服务

- 让master来做Hbase的Master节点，所以我们在master上执行启动Hbase的命令“bin/start-hbase.sh”，并使用jps来查看进程，可以看到HMaster进程和HRegionServer两个进程

~~~shell
/usr/local/app/hbase-1.2.1
bin/start-hbase.sh 
~~~

- 启动服务信息

![image-20221106120515760](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106120515760.png)

- 查看集群信息

```shell
jps
```

![image-20221106121305474](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106121305474.png)

slave1有HMaster是因为，我们把slave1作为我们Hbase集群的备用节点

### 6 Web端查看HBase集群服务

- 可以看到master作为Master节点：

```shell
http://master:16010
```

![image-20221106121651221](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106121651221.png)

* 可以看到slave1作为备用Master节点

```shell
http://slave1:16010
```



![image-20221106121831763](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106121831763.png)

- 可以看到slave2作为RegionServer节点

```shell
http://slave2:16030
```

![image-20221106121921366](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106121921366.png)

- 在hdfs中查看

~~~shell
http://master:50070/
~~~



![image-20221106142039713](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106142039713.png)



### 7 测试HBase集群

#### （1）HBase Shell基本操作

1. 打开shell脚本

```shell
 bin/hbase shell
```

![image-20221106141218249](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106141218249.png)

2. 查看帮助

~~~mysql
help
~~~

![image-20221119112424139](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119112424139.png)

3. 创建表

创建表必须带有一个列族。其中cf就代表一个列族。如下查看表详情得时候，给我们列出来的信息都是按照列族来的。

```sql
create 'student','info'
```

![image-20221119113343465](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119113343465.png)

4. 插入数据

```sql
put 'student','1001','info:sex','male'
put 'student','1001','info:age','18'
put 'student','1002','info:name','Janna'
put 'student','1002','info:sex','female'
put 'student','1002','info:age','20'
```

![image-20221119113816641](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119113816641.png)

5. 查看当前数据库中有哪些表

```sql
list
```

![image-20221119113840010](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119113840010.png)

6. 扫描查看表数据

```sql
 scan 'student'
```

![image-20221119113934647](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119113934647.png)

```sql
 scan 'student',{STARTROW => '1001', STOPROW => '1001'}
```

![image-20221119114014346](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119114014346.png)

```sql
scan 'student',{STARTROW => '1001'}
```

![image-20221119114121938](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119114121938.png)



- 查看表结构

```sql
 desc 'student'
```

- ![image-20221119114426633](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119114426633.png)

- 更新指定字段

```sql
 put 'student','1001','info:name','Nick'
 put 'student','1001','info:age','100'
```

![image-20221119114614654](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119114614654.png)

扫描表

```sql
scan 'student'
```

![image-20221119114712954](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119114712954.png)

- 查看“指定行”或“指定列族:列”的数据

```sql
get 'student','1001'
```

![image-20221119114803677](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119114803677.png)

```sql
get 'student','1001','info:name'
```

![image-20221119114823796](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119114823796.png)

- 统计表数据行数

```sql
 count 'student'
```

![image-20221119114910380](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119114910380.png)

#### （2）HBase Java API编程

- Maven中pom.xml依赖

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.example</groupId>
    <artifactId>35_Hbase</artifactId>
    <version>1.0-SNAPSHOT</version>
    <properties>
        <kotlin.version>1.4.10</kotlin.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.apache.hbase</groupId>
            <artifactId>hbase-client</artifactId>
            <version>1.2.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.hbase</groupId>
            <artifactId>hbase-server</artifactId>
            <version>1.2.1</version>
        </dependency>
        <dependency>
            <groupId>org.jetbrains.kotlin</groupId>
            <artifactId>kotlin-stdlib-jdk8</artifactId>
            <version>${kotlin.version}</version>
        </dependency>
        <dependency>
            <groupId>org.jetbrains.kotlin</groupId>
            <artifactId>kotlin-test</artifactId>
            <version>${kotlin.version}</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.jetbrains.kotlin</groupId>
                <artifactId>kotlin-maven-plugin</artifactId>
                <version>${kotlin.version}</version>
                <executions>
                    <execution>
                        <id>compile</id>
                        <phase>compile</phase>
                        <goals>
                            <goal>compile</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>test-compile</id>
                        <phase>test-compile</phase>
                        <goals>
                            <goal>test-compile</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <jvmTarget>1.8</jvmTarget>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <executions>
                    <execution>
                        <id>compile</id>
                        <phase>compile</phase>
                        <goals>
                            <goal>compile</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>testCompile</id>
                        <phase>test-compile</phase>
                        <goals>
                            <goal>testCompile</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

- 连接HBase与基本配置

```java
//声明Connection以及Admin
Connection connection;
Admin admin;
//1.创建一个配置文件，创建配置信息，并指定连接的集群
Configuration conf = HBaseConfiguration.create();
// 配置ZK的地址，通过ZK可以找到HBase
conf.set("hbase.zookeeper.quorum", "master,slave1,slave2");
// 2、创建连接
connection = ConnectionFactory.createConnection(conf);
//3.创建DDL操作对象，创建Admin对象
admin = connection.getAdmin();
```

- 关闭连接

```java
//关闭资源
admin.close();
connection.close();
```

1. 查看表是否存在

```java
package com.gzgs;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.TableName;
import org.apache.hadoop.hbase.client.Admin;
import org.apache.hadoop.hbase.client.Connection;
import org.apache.hadoop.hbase.client.ConnectionFactory;
import java.io.IOException;

/**
 * @Author LinRuShao
 * @Date 2022/11/19 12:00
 */
public class hbaseAPI_isTableExists {
    public static void main(String[] args) throws IOException {
        //声明Connection以及Admin
        Connection connection;
        Admin admin;
        //1.创建一个配置文件，创建配置信息，并指定连接的集群
        Configuration conf = HBaseConfiguration.create();
        // 配置ZK的地址，通过ZK可以找到HBase
        conf.set("hbase.zookeeper.quorum", "master,slave1,slave2");
        // 2、创建连接
        connection = ConnectionFactory.createConnection(conf);
        //3.创建DDL操作对象，创建Admin对象
        admin = connection.getAdmin();
        
        boolean student = admin.tableExists(TableName.valueOf("student"));
        System.out.println(student);

        //关闭资源
        admin.close();
        connection.close();
    }
}
```

![image-20221119141943660](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119141943660.png)

运行结果

![image-20221119142549928](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119142549928.png)

2. 创建表

```java
HTableDescriptor student2 = new HTableDescriptor(TableName.valueOf("student2"));
HColumnDescriptor info2 = new HColumnDescriptor("info2");
//info.setTimeToLive(100);// 对列簇进行配置
student2.addFamily(info2);
admin.createTable(student2);
```

![image-20221119142300378](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119142300378.png)

运行结果

![image-20221119142436739](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119142436739.png)

HBase中查看结果

![image-20221119142635900](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119142635900.png)

3. 列出所有的表

```java
TableName[] tableNames = admin.listTableNames();
for (TableName name : tableNames) {
     System.out.println(name.getNameAsString());
    }
```

![image-20221119142844490](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119142844490.png)

运行结果

![image-20221119142951847](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119142951847.png)

4. 插入数据

```java
//插入数据
Table testAPI = connection.getTable(TableName.valueOf("student2"));
Put put = new Put("0002".getBytes());
// 相当于插入一列（一个cell）数据
put.addColumn("info2".getBytes(), "name".getBytes(), "李四".getBytes());
put.addColumn("info2".getBytes(), "age".getBytes(), "23".getBytes());
put.addColumn("info2".getBytes(), "phone".getBytes(), "18888887".getBytes());
testAPI.put(put);
System.out.println("插入数据成功");
```

![image-20221119143501951](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119143501951.png)

运行结果

![image-20221119143327564](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119143327564.png)

HBase中查看数据

![image-20221119143546198](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119143546198.png)

5. 获取表中的数据

```java
Table testAPI = connection.getTable(TableName.valueOf("student"));
Get get = new Get("1001".getBytes());
Result rs = testAPI.get(get);
// 获取rk
byte[] rk = rs.getRow();
System.out.println(rk);
System.out.println(Bytes.toString(rk));
// 获取cell
byte[] name = rs.getValue("info".getBytes(), "name".getBytes());
System.out.println(name);
System.out.println(Bytes.toString(name));
```



![image-20221119144128736](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119144128736.png)·![image-20221119144204135](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119144204135.png)

运行结果

![image-20221119144037094](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119144037094.png)

6. 删除表

```java
//删除表
TableName test = TableName.valueOf("test");
System.out.println(admin.tableExists(test));
// 判断表是否存在
if (admin.tableExists(test)) {
admin.disableTable(test);
admin.deleteTable(test);
System.out.println("删除表成功！！！");
}
```

![image-20221119144606059](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119144606059.png)

运行结果

![image-20221119144536475](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119144536475.png)

hbase查看结果

![image-20221119144653182](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119144653182.png)

### 8 停止服务

```shell
 bin/stop-hbase.sh
```

![image-20221106142256953](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106142256953.png)



### 9 异常处理

创建表时出现错误

![image-20221106141529881](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106141529881.png)

少了cf，其中cf就代表一个列族

![image-20221106141625546](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221106141625546.png)

-  Java API报错

![image-20221119121512110](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119121512110.png)

问题：依赖错误，maven中的hbase版本是2.0.5，而我集群中的hbase版本是1.2.1

解决方法：修改pom.xml中的hbase依赖

![image-20221119121749559](Hbase%E9%9B%86%E7%BE%A4%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221119121749559.png)