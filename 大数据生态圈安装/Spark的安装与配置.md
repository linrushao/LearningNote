## Spark的安装与配置

### 1 Spark的下载与解压

0. 环境准备

准备环境:准备两台以上Linux服务器，安装好JDK

![spark高可用集群部署](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221231205024206-1672751207428.png)

1. 下载Spark安装文件：[Spark官方下载地址](http://spark.apache.org/downloads.html)

![image-20230103211009056](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103211009056.png)

因为spark2.x比较稳定，所以本安装配置选择2.x，在官方中下载需要在本下载网页的最下面中选择全部的发行版本，选择需要安装Spark版本即可

![image-20230103211114492](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103211114492.png)

官方文档：http://spark.apache.org/docs/latest/

2. 上传与解压

上传spark安装包到Linux上

![image-20230103143306363](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103143306363.png)

解压软件

```shell
[root@master app]# tar -zxvf spark-2.4.0-bin-hadoop2.7.tgz -C /usr/local/app
```

注意：-C  是解压到什么位置

![image-20230103143433479](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103143433479.png)

删除原来的压缩包并重命名解压的

```shell
[root@master app]# mv spark-2.4.0-bin-hadoop2.7 spark-2.4.0
```

![image-20230103143647398](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103143647398.png)

### 2 配置环境变量

进入到/etc/profile目录下，在mycluster.sh环境变量文件中

```shell
[root@master app]# cd /etc/profile.d/
[root@master profile.d]# vim mycluster.sh 
```

在文件中添加以下环境变量信息

```sh
# spark
export SPARK_HOME=/usr/local/app/spark-2.4.0
export PATH=$PATH:$SPARK_HOME/bin
```

![image-20230103144142805](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103144142805.png)

使环境变量生效

```shell
[root@master profile.d]# source /etc/profile.d/mycluster.sh 
```

### 3 修改配置文件

- spark-env.sh配置

进入到Spark安装目录，进入conf目录查看里面的配置文件

```shell
[root@master conf]# cd /usr/local/app/spark-2.4.0/conf/
[root@master conf]# ll

```

![image-20230103144533582](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103144533582.png)

重命名并修改spark-env.sh.template文件

```shell
[root@master conf]# mv spark-env.sh.template spark-env.sh
[root@master conf]# vim spark-env.sh 
```

![image-20230103144702184](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103144702184.png)

在该配置文件中添加如下配置

```sh
#Java环境变量
export JAVA_HOME=/usr/local/app/jdk1.8.0_162
#驱动器节点IP，设置Master的主机名
export SPARK_MASTER_IP=master
# 提交Application的端口，默认就是这个【7077】，万一要改呢就改这里
export SPARK_MASTER_PORT=7077
#每一个worker节点上可用的最大内存，我的虚拟机就2g
#真实服务器如果有128G，你可以设置为100G
#所以这里设置为1024m或1g
export SPARK_WORKER_MEMORY=1g
# 每一个Worker最多可以使用的cpu core的个数，我虚拟机就4个
# 真实服务器如果有32个，你可以设置为32个
export SPARK_WORKER_CORES=4
#Hadoop路径
export HADOOP_HOME=/usr/local/app/hadoop-2.7.2
#Hadoop配置目录
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
```

保存退出

![image-20230103145955509](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103145955509.png)

- slaves配置

重命名并修改slaves.template文件

```sh
[root@master conf]# mv slaves.template slaves
[root@master conf]# ll
[root@master conf]# vim slaves
```

![image-20230103150048940](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103150048940.png)

在该文件中添加子节点所在的位置（Worker节点）

```sh
master
slave1
slave2
```

保存退出

![image-20230103150310591](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103150310591.png)

### 4 分发文件

1. 分发spark软件

- 第一种方式：将配置好的Spark拷贝到其他节点上

```shell
scp -r /usr/local/app/spark-2.4.0  master:/usr/local/app/
scp -r /usr/local/app/spark-2.4.0  slave1:/usr/local/app/
scp -r /usr/local/app/spark-2.4.0  slvae2:/usr/local/app/
```

- 第二种方式【脚本】：将配置好的spark安装程序拷贝给其他机器 

```shell
[root@master conf]# for i in master slave1 slave2; do scp -r /usr/local/app/spark-2.4.0 $i:/usr/local/app/; done
```

![image-20230103150712238](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103150712238.png)

![image-20230103150927376](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103150927376.png)

2. 分发环境变量

```shell
[root@master ~]# for i in slave1 slave2; do scp -r /etc/profile.d/mycluster.sh $i:/etc/profile.d/; done
```

![image-20230103151106095](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103151106095.png)

让环境变量立即生效

```shell
[root@master ~]# source /etc/profile.d/mycluster.sh
[root@slave1 app]# source /etc/profile.d/mycluster.sh
[root@slave2 app]# source /etc/profile.d/mycluster.sh
```

![image-20230103151242269](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103151242269.png)

### 5 启动spark集群

Spark集群配置完毕，目前是1个Master，3个Work，在master上启动Spark集群

```shell
[root@master spark-2.4.0]# cd /usr/local/app/spark-2.4.0
[root@master spark-2.4.0]# sbin/start-all.sh
```

![image-20230103151605235](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103151605235.png)

启动后执行jps命令，主节点上有Master进程，其他子节点上有Work进行

![image-20230103151725854](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103151725854.png)

通过web页面访问spark管理页面（master所在机器的地址+8080端口），登录Spark管理界面查看集群状态（主节点）：[http://master:8080//](http://master:8080/)

![image-20230103151816024](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103151816024.png)

进入spark-shell

```shell
[root@master spark-2.4.0]# spark-shell
```

![image-20230103152156603](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103152156603.png)

到此为止，Spark集群安装完毕

### 6 测试spark集群

#### 6.1 第一个Spark程序

计算pi，利用spark中默认的例子，在lib目录下，一个WordCount程序和pi程序，该算法是利用蒙特·卡罗算法求PI

```shell
[root@master spark-2.4.0]# /usr/local/app/spark-2.4.0/bin/spark-submit \
--class org.apache.spark.examples.SparkPi \
--master spark://master:7077 \
--executor-memory 1G \
--total-executor-cores 2 \
/usr/local/app/spark-2.4.0/examples/jars/spark-examples_2.11-2.4.0.jar \
1000
```

参数说明：

| 参数                                                         | 含义                             |
| ------------------------------------------------------------ | -------------------------------- |
| --class org.apache.spark.examples.SparkPi                    | 指定类名                         |
| --master spark://master:7077                                 | 指定Master的地址                 |
| --executor-memory 1g                                         | 指定每个worker可用内存为2G       |
| --total-executor-cores 2                                     | 指定整个集群使用的cup核数为2个   |
| /usr/local/app/spark-2.4.0/examples/jars/spark-examples_2.11-2.4.0.jar | jar包路径                        |
| 1000                                                         | 迭代次数【迭代次数越多，越精确】 |

![image-20230103153500058](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103153500058.png)

#### 6.2 Spark Shell测试

spark-shell是Spark自带的交互式Shell程序，方便用户进行交互式编程，用户可以在该命令行下用scala编写spark程序。

```shell
[root@master spark-2.4.0]# /usr/local/app/spark-2.4.0/bin/spark-shell \
--master spark://master:7077 \
--executor-memory 1g \
--total-executor-cores 2
```

注意：

如果启动spark shell时没有指定master地址，但是也可以正常启动spark shell和执行spark shell中的程序，其实是启动了spark的local模式，该模式仅在本机启动一个进程，没有与集群建立联系。Spark Shell中已经默认将SparkContext类初始化为对象sc。用户代码如果需要用到，则直接应用sc即可

![image-20230103153725403](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103153725403.png)

#### 6.3 Spark Shell中编写WordCount程序

1.首先启动hdfs

```shell
[root@master ~]# /usr/local/app/hadoop-2.7.2/sbin/start-dfs.sh
```

![image-20230103154634686](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103154634686.png)

jps查看HDFS的进程

```shell
[root@master ~]# jps
```

![image-20230103154718095](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103154718095.png)

2.向hdfs上传一个文件到hdfs://master:9000/words.txt

```shell
[root@master ~]# hdfs dfs -mkdir /wordcount
[root@master ~]# hdfs dfs -put /root/test/words.txt /wordcount
[root@master ~]# hdfs dfs -ls /wordcount
```

![image-20230103155203951](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103155203951.png)

3.在spark shell中用scala语言编写spark程序

启动Spark-shell

```scala
[root@master spark-2.4.0]# /usr/local/app/spark-2.4.0/bin/spark-shell \
--master spark://master:7077 \
--executor-memory 1g \
--total-executor-cores 2
```

编写spark-shell命令

```scala
scala> sc.textFile("hdfs://master:8020/wordcount/words.txt").flatMap(_.split(" ")).map((_,1)).reduceByKey(_+_).saveAsTextFile("hdfs://master:8020/wordcountout")
```

![image-20230103160022066](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103160022066.png)

参数说明：

| sc                                                 | SparkContext对象，该对象是提交spark程序的入口 |
| -------------------------------------------------- | --------------------------------------------- |
| textFile("hdfs://master:8020/wordcount/words.txt") | 是hdfs中读取数据                              |
| flatMap(_.split(" "))                              | 先map再压平                                   |
| map((_,1))                                         | 将单词和1构成元组                             |
| reduceByKey(_+_)                                   | 按照key进行reduce，并将value累加              |
| saveAsTextFile("hdfs://master:8020/wordcountout")  | 将结果写入到hdfs中                            |

注意：端口和hdfs中的core-site.xml中的Namenode的端口一样

![image-20230103155432561](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103155432561.png)

5. 使用hdfs命令查看结果

```shell
[root@master ~]# hdfs dfs -ls hdfs://master:8020/wordcountout/p*
[root@master ~]# hdfs dfs -ls /wordcountout
```

![image-20230103160139198](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103160139198.png)

```shell
[root@master ~]# hdfs dfs -cat /wordcountout/part-00000
```

![image-20230103160238238](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103160238238.png)

#### 6.4 IDEA中编写WordCount程序

spark shell仅在测试和验证我们的程序时使用的较多，在生产环境中，通常会在IDE中编制程序，然后打成jar包，然后提交到集群，最常用的是创建一个Maven项目，利用Maven来管理jar包的依赖。

1. 创建一个项目

![image-20230103200521637](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103200521637.png)

2. 选择Maven项目，然后点击next

![image-20230103200538744](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103200538744.png)

3. 填写maven的GAV，然后点击next

![image-20230103200819011](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103200819011.png)

4. 填写项目名称，然后点击finish 

![image-20230103200834404](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103200834404.png)

5. 创建好maven项目后，点击Project Structure，点击Global Libraries选择Scala版本，Spark2.4.0支持的Scala版本是2.11。

![image-20230103201211164](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103201211164.png)

6. 构建完成的Maven架构

![image-20230103201605602](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103201605602.png)

7. 配置Maven的pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.gzgs</groupId>
    <artifactId>48_Spark</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <scala.version>2.11.12</scala.version>
        <spark.version>2.4.0</spark.version>
        <hadoop.version>2.7.2</hadoop.version>
        <kotlin.version>1.4.10</kotlin.version>
        <encoding>UTF-8</encoding>
    </properties>

    <dependencies>
        <!-- 导入scala的依赖 -->
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-library</artifactId>
            <version>${scala.version}</version>
        </dependency>
        <!-- 导入spark的依赖 -->
        <dependency>
            <groupId>org.apache.spark</groupId>
            <artifactId>spark-core_2.11</artifactId>
            <version>${spark.version}</version>
        </dependency>
        <!-- 指定hadoop-client API的版本 -->
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>${hadoop.version}</version>
        </dependency>
    </dependencies>
    <build>
        <pluginManagement>
            <plugins>
                <!-- 编译scala的插件 -->
                <plugin>
                    <groupId>net.alchim31.maven</groupId>
                    <artifactId>scala-maven-plugin</artifactId>
                    <version>3.2.2</version>
                </plugin>
                <!-- 编译java的插件 -->
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.5.1</version>
                </plugin>
            </plugins>
        </pluginManagement>
        <plugins>
            <plugin>
                <groupId>net.alchim31.maven</groupId>
                <artifactId>scala-maven-plugin</artifactId>
                <executions>
                    <execution>
                        <id>scala-compile-first</id>
                        <phase>process-resources</phase>
                        <goals>
                            <goal>add-source</goal>
                            <goal>compile</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>scala-test-compile</id>
                        <phase>process-test-resources</phase>
                        <goals>
                            <goal>testCompile</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <executions>
                    <execution>
                        <phase>compile</phase>
                        <goals>
                            <goal>compile</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>


            <!-- 打jar插件 -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.4.3</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <filters>
                                <filter>
                                    <artifact>*:*</artifact>
                                    <excludes>
                                        <exclude>META-INF/*.SF</exclude>
                                        <exclude>META-INF/*.DSA</exclude>
                                        <exclude>META-INF/*.RSA</exclude>
                                    </excludes>
                                </filter>
                            </filters>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

8. 新建一个scala class，类型为Object

![image-20230103202326627](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103202326627.png)

9. 编写spark程序

```scala
package com.gzgs.linrushao

import org.apache.spark.rdd.RDD
import org.apache.spark.{SparkConf, SparkContext}

/**
 * @Author LinRuShao
 * @Date 2023/1/3 20:20
 */
object WordCount {
  def main(args: Array[String]): Unit = {
    //创建Spark配置，设置应用程序名称，如果是当地运行需要设置core核数
    val conf: SparkConf = new SparkConf().setAppName("WordCount") //.setMaster("local[2]")
    //创建Spark执行的入口
    val sc: SparkContext = new SparkContext(conf)
    //指定以后从哪里读取数据创建RDD【弹性分布式数据集】,第二个参数：设置分区数
    val lines: RDD[String] = sc.textFile("hdfs://master:8020/wordcount/words.txt", 1)
    //切分压平
    val words: RDD[String] = lines.flatMap(_.split(" "))
    //将单词和一组合
    val wordAndOne: RDD[(String, Int)] = words.map((_, 1))
    //按key进行聚合
    val reduce: RDD[(String, Int)] = wordAndOne.reduceByKey(_ + _)
    //将结果保存到HDFS中
    reduce.saveAsTextFile("hdfs://master:8020/wordcountout")
    //释放资源
    sc.stop()
  }
}
```

10. 使用Maven打包：首先修改pom.xml中的main class，点击idea右侧的Maven Project选项，点击Lifecycle,选择clean和package，然后点击Run Maven Build

![image-20230103210023575](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103210023575.png)

11. 选择编译成功的jar包，并将该jar上传到Spark集群中的某个节点上

![image-20230103204806781](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103204806781.png)

12. 首先启动hdfs和Spark集群

查看hdfs，spark是否启动成功

![image-20230103204958895](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103204958895.png)

HDFS，Spark启动命令

```shell
[root@master ~]# /usr/local/app/hadoop-2.7.2/sbin/start-dfs.sh
[root@master spark-2.4.0]# cd /usr/local/app/spark-2.4.0/sbin/start-all.sh
```

13. 使用spark-submit命令提交Spark应用（注意参数的顺序）

```shell
/usr/local/app/spark-2.4.0/bin/spark-submit \
--class com.gzgs.linrushao.WordCount \
--master spark://master:7077 \
--executor-memory 1G \
--total-executor-cores 2 \
/root/test/48_Spark-1.0-SNAPSHOT.jar
```

![image-20230103210207982](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103210207982.png)

14. 查看程序执行结果

```shell
[root@master test]# hdfs dfs -ls /wordcountout
```

![image-20230103210254850](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103210254850.png)

```shell
[root@master test]# hdfs dfs -cat /wordcountout/part-00000
```

![image-20230103210401459](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103210401459.png)

### 7 Spark高可用配置

上面的Spark集群配置完毕，但是有一个很大的问题，那就是Master节点存在单点故障，要解决此问题，就要借助zookeeper，并且启动至少两个Master节点来实现高可靠，配置方式比较简单：

Spark集群规划：master，slave1是Master；master，slave1，slave2是Worker

#### 7.1 拷贝集群

为了预防万一，首先创建一个ha目录，该目录专门用于配置高可用集群，例如Hadoop，Spark

```shell
[root@master spark-2.4.0]# mkdir /usr/local/app/ha
```

将spark拷贝到ha目录下

```shell
[root@master spark-2.4.0]# cp -r /usr/local/app/spark-2.4.0 /usr/local/app/ha/
```

![image-20230103212352546](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103212352546.png)

#### 7.2 在原有基础上修改配置文件

- 修改spark-env.sh

安装配置zk集群，并启动zk集群，停止spark所有服务，修改配置文件spark-env.sh，在该配置文件中删掉SPARK_MASTER_IP并添加如下配置

```shell
export SPARK_DAEMON_JAVA_OPTS="-Dspark.deploy.recoveryMode=ZOOKEEPER -Dspark.deploy.zookeeper.url=master:2181,slave1:2181,slave2:2181 -Dspark.deploy.zookeeper.dir=/spark"
```

![image-20230103212857988](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103212857988.png)

总的配置信息

```sh
#Java环境变量
export JAVA_HOME=/usr/local/app/jdk1.8.0_162
#驱动器节点IP，设置Master的主机名
#export SPARK_MASTER_IP=master
# 提交Application的端口，默认就是这个【7077】，万一要改呢就改这里
#export SPARK_MASTER_PORT=7077
#每一个worker节点上可用的最大内存，我的虚拟机就2g
#真实服务器如果有128G，你可以设置为100G
#所以这里设置为1024m或1g
export SPARK_WORKER_MEMORY=1g
# 每一个Worker最多可以使用的cpu core的个数，我虚拟机就4个
# 真实服务器如果有32个，你可以设置为32个
export SPARK_WORKER_CORES=4
#Hadoop路径
export HADOOP_HOME=/usr/local/app/hadoop-2.7.2
#Hadoop配置目录
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
#配置zookeeper集群
export SPARK_DAEMON_JAVA_OPTS="-Dspark.deploy.recoveryMode=ZOOKEEPER -Dspark.deploy.zookeeper.url=master:2181,slave1:2181,slave2:2181 -Dspark.deploy.zookeeper.dir=/spark"
```

#### 7.3 配置环境变量

【高可用一定要配置环境变量】

进入环境变量中配置【三个节点都要】

```shell
[root@slave2 ~]# vim /etc/profile.d/mycluster.sh 
```

添加以下内容

```shell
# spark
export SPARK_HOME=/usr/local/app/ha/spark-2.4.0
export PATH=$PATH:$SPARK_HOME/bin
```

#### 7.4 分发文件

```shell
for i in master slave1 slave2; do scp -r /usr/local/app/ha/spark-2.4.0 $i:/usr/local/app/ha/; done
```

![image-20230103213644587](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103213644587.png)

在三台节点的ha目录下查看

![image-20230103213756283](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103213756283.png)

- 分发环境变量文件

```shell
[root@master ~]# for i in slave1 slave2; do scp -r /etc/profile.d/mycluster.sh $i:/etc/profile.d/; done
```

#### 7.5 启动spark高可用

1. 先启动zookeeper集群

```shell
[root@master ~]# zookeepercluster.sh start #脚本启动
```

![image-20230103214109132](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103214109132.png)

查看zookeeper集群状态

![image-20230103214217967](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103214217967.png)

2. 再启动spark集群

- 在master上执行**sbin/start-all.sh**脚本

```shell
[root@master ~]# /usr/local/app/ha/spark-2.4.0/sbin/start-all.sh 
```

![image-20230103214349389](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103214349389.png)

查看spark集群

![image-20230103214437360](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103214437360.png)

- 然后在slave1上执行**sbin/start-master.sh**启动第二个Master

![image-20230103214535289](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103214535289.png)

再次查看spark集群状态

![image-20230103214619761](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103214619761.png)

- 在Web端查看Spark集群信息

master

![image-20230103214733099](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103214733099.png)

slave1

![image-20230103224213105](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103224213105.png)

测试高可用

- 断开master

```shell
[root@master spark-2.4.0]# kill -9 12105
```

![image-20230103224852964](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103224852964.png)

查看slave1的master状态【需要等一会，等zookeeper检测到，就是说等心跳检测】

![image-20230103224937762](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103224937762.png)

重新启动master中的spark的master

![image-20230103225056444](Spark%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230103225056444.png)