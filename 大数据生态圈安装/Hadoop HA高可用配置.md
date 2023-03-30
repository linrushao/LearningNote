## Hadoop HA高可用配置

### 1 Hadoop环境的基础配置



1. 基础环境准备

（1）测试jdk环境

![image-20221213145437145](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221213145437145.png)

（2）关闭防火墙

![image-20221213145707801](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221213145707801.png)

（3）SSH免密登录

![image-20221213211732466](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221213211732466.png)

（4）时钟同步

![image-20221213145956617](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221213145956617.png)

（5）zookeeper集群测试

![image-20221117194224306](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117194224306.png)

2. Hadoop的上传与解压

![image-20221117194041876](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117194041876.png)

3. 配置Hadoop环境变量

```shell
vim /etc/profile.d/mycluster.sh 
```



![image-20221117194550558](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117194550558.png)

- 让配置文件立即生效

```shell
source /etc/profile.d/mycluster.sh
```

### 2 Hadoop配置文件

1. 配置core-site.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!--
  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License. See accompanying LICENSE file.
-->

<!-- Put site-specific property overrides in this file. -->

<configuration>
    <!--指定NameNode 的地址 指定hdfs的nameservices名称为mycluster，与hdfs-site.xml的HA配置相同-->
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://mycluster</value>
    </property>
    
    <!--指定hadoop数据的存储目录-->
    <property>
        <name>hadoop.data.dir</name>
        <value>/usr/local/app/ha/hadoop-2.7.2/data</value>
    </property>
    	
    <!--指定hadoop临时数据的存储目录-->
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/usr/local/app/ha/hadoop-2.7.2/data/tmp</value>
    </property>
   
    <!--设置缓存的大小-->
    <property>
        <name>io.file.buffer.size</name>
        <value>131702</value>
    </property>
    
    <!--指定zookeeper的地址,配置HA时需要-->
    <property>
        <name>ha.zookeeper.quorum</name>
        <value>master:2181,slave1:2181,slave2:2181</value>
    </property>
    
</configuration>
```

![image-20221118100447003](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118100447003.png)

2. 配置hdfs-site.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!--
  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License. See accompanying LICENSE file.
-->

<!-- Put site-specific property overrides in this file. -->

<configuration>
    
    <!--指定副本数-->
    <property>
        <name>dfs.replication</name>
        <value>3</value>
    </property>
    <!--指定NameNode数据的存储目录-->
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>/usr/local/app/ha/hadoop-2.7.2/data/name</value>
    </property>
    <!--指定Datanode数据的存储目录-->
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>/usr/local/app/ha/hadoop-2.7.2/data/data</value>
    </property>
    <!--开启web界面访问hdfs-->
    <property>
        <name>dfs.webhdfs.enabled</name>
        <value>true</value>
    </property>
    <!--权限校验,flase为不开启-->
    <property>
        <name>dfs.permissions.enabled</name>
        <value>false</value>
    </property>
    
    <!--HDFS HA配置-->
    
    <!--指定hdfs的nameservices名称为mycluster,将多个NN打包成一个名字-->
    <property>
        <name>dfs.nameservices</name>
        <value>mycluster</value>
    </property>
    <!--集群中Name Node节点都有哪些，指定mycluster的两个namenode的名称分别为nn1,nn2-->
    <property>
        <name>dfs.ha.namenodes.mycluster</name>
        <value>nn1,nn2</value>
    </property>
    
    <!--nn1，nn2的RPC通信地址-->
    <!--nn1的RPC通信地址-->
    <property>
        <name>dfs.namenode.rpc-address.mycluster.nn1</name>
        <value>master:9000</value>
    </property>
    <!--nn2的RPC通信地址-->
    <property>
        <name>dfs.namenode.rpc-address.mycluster.nn2</name>
        <value>slave1:9000</value>
    </property>
    
    <!--nn1,nn2的http通信地址-->
    <!--nn1的http通信地址-->
    <property>
        <name>dfs.namenode.http-address.mycluster.nn1</name>
        <value>master:50070</value>
    </property>
    <!--nn2的http通信地址-->
    <property>
        <name>dfs.namenode.http-address.mycluster.nn2</name>
        <value>slave1:50070</value>
    </property>
    
    <!--指定NameNode元数据在JournalNode上的存放位置-->
    <property>
        <name>dfs.namenode.shared.edits.dir</name>
        <value>qjournal://master:8485;slave1:8485;slave2:8485/mycluster</value>
    </property>
        <!--声明journalnode服务器日志文件的存储目录-->
    <property>
        <name>dfs.journalnode.edits.dir</name>
        <value>/usr/local/app/ha/hadoop-2.7.2/data/journal</value>
    </property>
    
    <!--访问代理：client用于确定那个Name Node为Active,指定HDFS客户端连接active namenode的Java类-->
    <property>
        <name>dfs.client.failover.proxy.provider.mycluster</name>
        <value>org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider</value>
    </property>
    
    <!--配置隔离机制为ssh，即同一时刻只能有一台服务器对外响应-->
    <property>
        <name>dfs.ha.fencing.methods</name>
        <value>sshfence</value>
    </property>
    <!--指定密钥的位置，使用隔离机制时需要ssh无秘钥登录-->
    <property>
        <name>dfs.ha.fencing.ssh.private-key-files</name>
        <value>/root/.ssh/id_rsa</value>
    </property>
    
    <!--开启自动故障转移-->
    <property>
        <name>dfs.ha.automatic-failover.enabled</name>
        <value>true</value>
    </property>

</configuration>
```

![image-20221118100859225](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118100859225.png)

![image-20221118100926439](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118100926439.png)

![image-20221118101032593](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118101032593.png)

![image-20221118101047751](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118101047751.png)

3. 配置mapred-site.xml

```xml
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!--
  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License. See accompanying LICENSE file.
-->

<!-- Put site-specific property overrides in this file. -->

<configuration>
    
    <!--指定MapReduce程序运行在Yarn上-->
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    
    <property>
        <name>dfs.permissions</name>
        <value>false</value>
    </property>
    
    <!--历史服务器端地址-->
    <property>
        <name>mapreduce.jobhistory.address</name>
        <value>master:10020</value>
    </property>
    
    <!--历史服务器端web端地址-->
    <property>
        <name>mapreduce.jobhistory.webapp.address</name>
        <value>master:19888</value>
    </property>
    
    <!--开启uber模式（针对小作业的优化）-->
    <property>
        <name>mapreduce.job.ubertask.enable</name>
        <value>true</value>
    </property>
    
    <!--配置启动uber模式的最大map数-->
    <property>
        <name>mapreduce.job.ubertask.maxmaps</name>
        <value>9</value>
    </property>
    
    <!--配置启动uber模式的最大reduce数-->
    <property>
        <name>mapreduce.job.ubertask.mapreduces</name>
        <value>1</value>
    </property>
</configuration>
```

![image-20221118101528395](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118101528395.png)

![image-20221118101544353](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118101544353.png)

4. 配置yarn-site.xml

```xml
<?xml version="1.0"?>
<!--
  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License. See accompanying LICENSE file.
-->
<configuration>
    
    <property>
         <name>yarn.nodemanager.aux-services</name>
         <value>mapreduce_shuffle</value>
    </property>
    
    <property>
        <name>yarn.nodemanager.auxservices.mapreduce.shuffle.class</name>
        <value>org.apache.hadoop.mapred.ShuffleHandler</value>
    </property>
    
    
    <!--YARN HA的配置-->
    <!--启用resourcemanager ha-->
    <property>
        <name>yarn.resourcemanager.ha.enabled</name>
        <value>true</value>
    </property>
    
    <!--启用自动故障转移-->
    <property>
        <name>yarn.resourcemanager.ha.automatic-failover.enabled</name>
        <value>true</value>
    </property>
    
    <!--指定yarn HA的名称，声明两台resourcemanager的地址-->
    <property>
        <name>yarn.resourcemanager.cluster-id</name>
        <value>yarncluster</value>
    </property>
    
    <!--指定两个resourcemanager的名称，指定RM的逻辑列表-->
    <property>
         <name>yarn.resourcemanager.ha.rm-ids</name>
         <value>rm1,rm2</value>
    </property>
    
    <!--指定rm1,rm2的主机名-->
    <property>
        <name>yarn.resourcemanager.hostname.rm1</name>
        <value>master</value>
    </property>
    <property>
        <name>yarn.resourcemanager.hostname.rm2</name>
        <value>slave1</value>
    </property>
    
    <!--指定rm1的web端地址,YARN的http端口-->
    <property>
        <name>yarn.resourcemanager.webapp.address.rm1</name>
        <value>master:8088</value>
    </property>
    <property>
        <name>yarn.resourcemanager.webapp.address.rm2</name>
        <value>slave1:8088</value>
    </property>	
    
    <!--指定zookeeper的地址-->
    <property>
        <name>yarn.resourcemanager.zk-address</name>
        <value>master:2181,slave1:2181,slave2:2181</value>
    </property>
    <!--配置zookeeper的储存位置-->
    <property>
        <name>yarn.resourcemanager.zk-state-store.parent-path</name>
        <value>/rmstore</value>
    </property>
    
    <!--开启resourcemanager自动恢复功能-->
    <property>
        <name>yarn.resourcemanager.recovery.enabled</name>
        <value>true</value>
    </property>
    
    <!--指定resource manager的状态信息存储在zookeeper集群-->
    <property>
        <name>yarn.resourcemanager.store.class</name>
        <value>org.apache.hadoop.yarn.server.resourcemanager.recovery.ZKRMStateStore</value>
    </property>
    
    <!--开启nodemanager自动恢复功能-->
    <property>
        <name>yarn.resourcemanager.recovery.enabled</name>
        <value>true</value>
    </property>	
    
    <!--配置nodemanager IPC的通信端口-->
    <property>
        <name>yarn.nodemanager.address</name>
        <value>0.0.0.0:45454</value>
    </property>	
    
</configuration>
```

![image-20221118101303265](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118101303265.png)

![image-20221118101327517](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118101327517.png)

![image-20221118101345290](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118101345290.png)

![image-20221118101429316](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118101429316.png)

5. 修改slave文件

```shell
master
slave1
slave2
```

![image-20221117200904616](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117200904616.png)





### 3 配置JAVA_HOME变量

- 在hadoop-env.sh文件中加入JAVA_HOME环境变量

```shell
vim hadoop-env.sh
```

加入以下内容

```shell
export JAVA_HOME=/usr/local/app/jdk1.8.0_162
```

![image-20221117200426664](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117200426664.png)



- 在yarn-env.sh文件中加入JAVA_HOME环境变量

```shell
vim yarn-env.sh
```

加入以下内容

```xml
export JAVA_HOME=/usr/local/app/jdk1.8.0_162
```



![image-20221117200513004](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117200513004.png)



- 在mapred-env.sh文件中加入JAVA_HOME环境变量

```shell
vim mapred-env.sh
```

加入以下内容

```xml
export JAVA_HOME=/usr/local/app/jdk1.8.0_162
```

![image-20221117200744371](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117200744371.png)

### 4 分发文件

- 将配置好的Hadoop复制到其他对应位置上，通过scp命令发送

```shell
scp -r /usr/local/app/ha/hadoop-2.7.2 slave1:/usr/local/app/ha/
scp -r /usr/local/app/ha/hadoop-2.7.2 slave2:/usr/local/app/ha/

```

![image-20221117201253276](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117201253276.png)

### 5 启动Hadoop集群

1. 启动zookeeper【master、slave1、slave2】

```shell
zkServer.sh start
```

![image-20221117202030457](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117202030457.png)

- 查看zookeeper进程

```shell
jps
```

![image-20221117202051163](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117202051163.png)

- 格式化ZKFC【master】

```shell
 bin/hdfs zkfc -formatZK
```

![image-20221117205059489](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117205059489.png)

- 格式化后验证，在某个zookeeper上执行zkCli.sh

```shell
zkCli.sh
```

![image-20221117205237288](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117205237288.png)

- 查看zookeeper的节点

```shell
ls /
```

![image-20221117205332614](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117205332614.png)

- 查看hadoop-ha下的节点

```shell
ls /hadoop-ha
```



![image-20221117205507424](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117205507424.png)

2. 启动Journal集群【master、slave1、slave2】

```shell
sbin/hadoop-daemon.sh start journalnode
```

> 用于Active NameNode ， Standby NameNode 同步数据，本身由一组JounnalNode节点组成，该组节点奇数个。

![image-20221117205830846](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117205830846.png)

- 查看jouranlNode进程【master、slave1、slave2】

```shell
jps
```

![image-20221117205930194](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117205930194.png)

3. 格式化集群上的一个NameNode【master、slave1】任选一个

```shell
bin/hdfs namenode -format -clusterId mycluster
```

![image-20221117210208508](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117210208508.png)

4. 启动集群中master的NameNode

```shell
sbin/hadoop-daemon.sh start namenode

scp -r /usr/local/app/ha/hadoop-2.7.2/data slave1:/usr/local/app/ha/hadoop-2.7.2/
```

![image-20221117210555529](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117210555529.png)

5. 将master上的Name Node数据同步到slave1上的Name Node【在slave1上执行】

```shell
bin/hdfs namenode -bootstrapStandby
```

![image-20221117213039221](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117213039221.png)

- 还有另外一种同步方法

```shell
scp -r /usr/local/app/ha/hadoop-2.7.2/data slave1:/usr/local/app/ha/hadoop-2.7.2/
```

直接将数据copy到slave1上

6. 启动slave1上的Name Node节点

```shell
sbin/hadoop-daemon.sh start namenode
```

![image-20221117213346837](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117213346837.png)

- 查看slave1上Name Node进程

```shell
jps
```

![image-20221117213440444](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117213440444.png)

master和slave1的namenode进程

![image-20221214100950869](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221214100950869.png)

- 在web端查看master和slave1的NameNode

master

![image-20221118094950447](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118094950447.png)

slave1

![image-20221118094924082](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118094924082.png)

两个都是standby，因为还没有启动zkfc进行监控检测

> Standby NameNode
>
> 同样会接到来自DataNode的Block report, block location updates和heartbeat，同时会从共享存储的Editlog上读取并执行这些log操作，保持自己NameNode中的元数据（Namespcae information + Block locations map）和Active NameNode中的元数据是同步的。所以说Standby模式的NameNode是一个热备（Hot Standby NameNode），一旦切换成Active模式，马上就可以提供NameNode服务

7. 启动所有的Data Node节点【master、slave1、slave2】

```shell
sbin/hadoop-daemon.sh start datanode
```

![image-20221118092849453](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118092849453.png)

8. 启动yarn【master】

```shell
sbin/start-yarn.sh
```

![image-20221118093122582](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118093122582.png)

-  查看yarn进程

```shell
jps
```

![image-20221118094545087](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118094545087.png)

- 单独启动slave1上的ResouceManager

```shell
sbin/yarn-daemon.sh start resourcemanager
```

![image-20221118094717373](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118094717373.png)

9. 启动ZKFC，分别在master、slave1上执行

```shell
sbin/hadoop-daemon.sh start zkfc
```

> （1）健康检测：zkfc会周期性的向它监控的namenode（只有namenode才有zkfc进程，并且每个namenode各一个）发生健康探测命令，从而鉴定某个namenode是否处于正常工作状态，如果机器宕机，心跳失败，那么zkfc就会标记它处于不健康的状态；
>
> （2）会话管理：如果namenode是健康的，zkfc机会保持在zookeeper中保持一个打开的会话，如果namenode是active状态的，那么zkfc还会在zookeeper中占有一个类型为短暂类型的znode，当这个namenode挂掉时，这个znode将会被删除，然后备用的namenode得到这把锁，升级为主的namenode，同时标记状态为active,当宕机的namenode,重新启动，他会再次注册zookeeper,发现已经有znode了，就自动变为standby状态，如此往复循环，保证高可靠性，但是目前仅支持最多配置两个namenode.
>
> (3)master选举：如上所述，通过在zookeeper中维持一个短暂类型的znode,来实现抢占式的锁机制，从而判断哪个namenode为active状态。

master

![image-20221118095152288](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118095152288.png)

slave1

![image-20221118095217199](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118095217199.png)

两个节点

![image-20221214095950176](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221214095950176.png)

10. 查看Hadoop高可用需要的所有进程

![image-20221118095321866](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118095321866.png)

 **第二种启动方式**

```shell
sbin/start-dfs.sh 
```

![image-20221118102109529](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118102109529.png)

```shell
sbin/start-yarn.sh
```

![image-20221118102138740](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118102138740.png)

查看进程

```shell
jps
```

![image-20221118102223807](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118102223807.png)

![image-20221214095255533](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221214095255533.png)

### 6 测试Hadoop高可用

1. 查看master的NameNode状态

![image-20221118095603795](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118095603795.png)

2. 查看slave1的NameNode状态

![image-20221118095655164](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118095655164.png)

3. 关闭master节点的NameNode

```shell
sbin/hadoop-daemon.sh stop namenode
```

![image-20221118095828480](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118095828480.png)

4. 查看slave1的NameNode状态

![image-20221118095926043](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118095926043.png)

发现自动转换为active

5. 再次启动master的NameNode

```shell
sbin/hadoop-daemon.sh start namenode
```

![image-20221118100654923](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118100654923.png)

![image-20221118100621971](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118100621971.png)

发现master变为了standby状态

6.查看yarn的HA

master【active】

![image-20221214095516769](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221214095516769.png)

slave1【standby】

![image-20221214095539831](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221214095539831.png)



### 7 关闭Hadoop集群

1. 先关闭yarn

```shell
sbin/stop-yarn.sh 
```

![image-20221118102339353](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118102339353.png)

2. 关闭hdfs

```shell
sbin/stop-dfs.sh
```

![image-20221118102442815](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118102442815.png)

3. 关闭zookeeper

```shell
zkServer.sh stop
```

![image-20221118102628387](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221118102628387.png)

### 异常

1. 格式化的异常

![image-20221117202435481](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117202435481.png)

经过检查hdfs_site.xml文件，发现配置错误，因为后面配置的都是nn1，nn2,而红框处，应该也是nn1,nn2，此处要保持前后一致（名字只要是唯一的就行）

![image-20221117202707475](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117202707475.png)

将master和slave1分别修改为nn1,nn2

![image-20221117203016882](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117203016882.png)

格式化成功

![image-20221117205059489](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117205059489.png)

2. 同步数据时异常

![image-20221117210725027](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117210725027.png)

hdfs-site.xml文件配置错误

![image-20221117212738105](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117212738105.png)

正确应该是

![image-20221117212846691](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117212846691.png)

再次同步数据

![image-20221117213030080](Hadoop%20HA%E9%AB%98%E5%8F%AF%E7%94%A8%E9%85%8D%E7%BD%AE.assets/image-20221117213030080.png)

