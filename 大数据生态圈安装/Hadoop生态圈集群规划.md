## Hadoop生态圈集群规划

### 主机规划

|                           | master     | slave1         | slave2 |
| ------------------------- | ---------- | -------------- | ------ |
| (Hadoop)NameNode          | 是         | 否             | 否     |
| (Haoop)SecondaryNameNode  | 否         | 是             | 否     |
| (Hadoop)DataNode          | 是         | 是             | 是     |
| (Hadoop)ResourceManage    | 是         | 否             | 否     |
| (Hadoop)NodeManager       | 是         | 是             | 是     |
| (Hadoop)JobHistoryServer  | 是         | 否             | 否     |
| (Hadoop HA)NameNode       | 是(Active) | 是(Standby)    | 否     |
| (Hadoop HA)ResourceManage | 是         | 是             | 否     |
| (Zookeeper)QuorumPeerMain | 是         | 是             | 是     |
| (HBase)HMaster            | 是         | 是（备用节点） | 否     |
| (HBase)HRegionServer      | 是         | 是             | 是     |
| MySQL                     | 是         | 否             | 否     |
| (Hive)RunJar              | 是         | 否             | 否     |
| Sqoop                     | 是         | 否             | 否     |
| Tomcat                    | 是         | 否             | 否     |

### 软件规划

| 软件      | 版本                                 |
| --------- | ------------------------------------ |
| Centos    | 7                                    |
| JDK       | jdk1.8.0_162                         |
| IDEA      | ideaIU-2019.2.4                      |
| Maven     | maven-3.5.0                          |
| Hadoop    | hadoop-2.7.2                         |
| XM5       | Xmanager Enterprise 5                |
| Zookeeper | zookeeper-3.4.13                     |
| MySQL     | mysql-5.6.33-linux-glibc2.5-x86_64   |
| HBase     | hbase-1.2.1                          |
| Hive      | hive-1.2.1                           |
| Sqoop     | sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz |
| Tomcat    | apache-tomcat-8.5.83.tar.gz          |





