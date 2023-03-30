## Hadoop的安装与配置

### 1 Hadoop集群的规划

|                   | master | slave1 | slave2 |
| ----------------- | ------ | ------ | ------ |
| NameNode          | 是     | 否     | 否     |
| DataNode          | 是     | 是     | 是     |
| SecondaryNameNode | 否     | 是     | 否     |
| ResourceManager   | 是     | 否     | 否     |
| NodeManager       | 是     | 是     | 是     |
|                   |        |        |        |
|                   |        |        |        |

### 2 基础环境配置

#### (1)安装JDK

1. 查看是否有linux自带jdk

```shell
 rpm -qa | grep java*
```

![image-20221117171501870](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221117171501870.png)

2. 下载并上传jdk,配置环境变量

![image-20221117171528025](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221117171528025.png)

3. source 文件，让文件立即生效，查看jdk是否安装

![image-20221117171551191](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221117171551191.png)

4. 测试jdk环境

![image-20221117171608034](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221117171608034.png)

#### (2) SSH免密登录

1. 生成公私钥

![image-20221117171704719](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221117171704719.png)

2. 复制各节点公钥到其他节点并测试

![image-20221117171724803](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221117171724803.png)

![image-20221117171732245](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221117171732245.png)

#### (3)时钟同步

1. 安装并配置master中ntp.conf文件

![image-20221117171813503](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221117171813503.png)

2. 配置slave节点的ntp.conf文件![img](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/clip_image002.jpg)

3. 启动并查看ntp服务器启动状态![img](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/clip_image004.jpg)

4. 同步slave节点的时间并测试![img](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/clip_image006.jpg)

### 3 部署Hadoop集群

1. core-site.xml文件

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
	<!--指定Namenode的地址-->
	<property>
		<name>fs.defaultFS</name>
		<value>hdfs://master:8020</value>
	</property>

        <!--指定hadoop数据的存储目录-->
        <property>
                <name>hadoop.data.dir</name>
                <value>/usr/local/app/hadoop-2.7.2/data</value>
	</property>
	
        <!--指定hadoop临时文件的存储目录-->
        <property>
                <name>hadoop.tmp.dir</name>
                <value>/usr/local/app/hadoop-2.7.2/tmp</value>
        </property>
</configuration>
```

2. hdfs-site.xml

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
                <value>file://${hadoop.data.dir}/name</value>
        </property>
        <!--指定Datanode数据的存储目录-->
        <property>
                <name>dfs.datanode.data.dir</name>
                <value>file://${hadoop.data.dir}/data</value>
        </property>
        <!--2nn web端访问地址-->
        <property>
                <name>dfs.namenode.secondary.http-address</name>
                <value>slave1:50090</value>
        </property>
</configuration>
```

3. mapred-site.xml

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
</configuration>
```

4. yarn-site.xml

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

<!-- Site specific YARN configuration properties -->
	<!--指定ResourceManager的地址-->
        <property>
                <name>yarn.resourcemanager.hostname</name>
                <value>master</value>
        </property>
        <property>
                <name>yarn.resourcemanager.address</name>
                <value>${yarn.resourcemanager.hostname}:8032</value>
        </property>
	<property>
                <name>yarn.resourcemanager.scheduler.address</name>
                <value>${yarn.resourcemanager.hostname}:8030</value>
        </property>
	<property>
                <name>yarn.resourcemanager.webapp.address</name>
                <value>${yarn.resourcemanager.hostname}:8088</value>
        </property>
        <property>
                <name>yarn.resourcemanager.webapp.https.address</name>
                <value>${yarn.resourcemanager.hostname}:8090</value>
        </property>
        <property>
                <name>yarn.resourcemanager.resource-tracker.address</name>
                <value>${yarn.resourcemanager.hostname}:8031</value>
        </property>
        <property>
                <name>yarn.resourcemanager.admin.address</name>
                <value>${yarn.resourcemanager.hostname}:8033</value>
        </property>
        <property>
                <name>yarn.nodemanager.local-dirs</name>
                <value>/opt/software/hadoop-2.7.2/data/yarn</value>
        </property>
	<!--开启日志集聚功能-->
        <property>
                <name>yarn.log-aggregation-enable</name>
                <value>true</value>
        </property>
        <property>
                <name>yarn.nodemanager.remote-app-log-dir</name>
                <value>/opt/software/hadoop-2.7.2/tmp</value>
        </property>
	<!--查看日志的路径-->
        <property>
                <name>yarn.log.server.url</name>
                <value>http://master:19888/jobhistory/logs</value>
        </property>
	<!--取消虚拟内存的限制-->
        <property>
                <name>yarn.nodemanager.vmem-check-enabled</name>
                <value>false</value>
        </property>
        <property>
                <name>yarn.nodemanager.aux-services</name>
                <value>mapreduce_shuffle</value>
        </property>
        <property>
                <name>yarn.nodemanager.aux-services.mapreduce_shuffle.class</name>
                <value>org.apache.hadoop.mapred.ShuffleHandler</value>
        </property>
        <property>
                <name>yarn.nodemanager.resource.memory-mb</name>
                <value>2048</value>
        </property>
        <property>
                <name>yarn.scheduler.minimum-allocation-mb</name>
                <value>512</value>
        </property>
        <property>
                <name>yarn.scheduler.maximum-allocation-mb</name>
                <value>4096</value>
        </property>
        <property>
                <name>mapreduce.map.memory.mb</name>
                <value>2048</value>
        </property>
        <property>
                <name>mapreduce.reduce.memory.mb</name>
                <value>2048</value>
        </property>
        <property>
                <name>yarn.nodemanager.resource.cpu-vcores</name>
                <value>1</value>
        </property>
</configuration>
```

5. slaves

```sh
master
slave1
slave2
```

6. 分发文件

```shell
scp -r /usr/local/app/hadoop-2.7.2/  slave1:/usr/local/
```

7. 格式化HDFS

```shell
hdfs namenode -format
```

![image-20230102204124531](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230102204124531.png)

8. 启动集群

```shell
#启动HDFS集群
./start-dfs.sh
#启动yarn
./start-yarn.sh
```

Master节点

![image-20230102164016475](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230102164016475.png)

slave1节点

![image-20230102164027193](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230102164027193.png)

slave2节点

![image-20230102164038680](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230102164038680.png)

9. 在Web端查看页面

查看HDFS，在浏览器中输入

```shell
master:50070
```

![image-20230102164141780](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230102164141780.png)

查看yarn，在浏览器中输入

```shell
master:8088
```

![image-20230102164222458](Hadoop%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20230102164222458.png)