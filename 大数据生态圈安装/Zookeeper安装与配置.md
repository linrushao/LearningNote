## Zookeeper安装与配置

### 1 zookeeper单机安装模式

#### 1 上传zookeeper压缩包

```shell
rz 
```

| 选项 | 含义                                               |
| ---- | -------------------------------------------------- |
| -e   | 文件名                                             |
| -a   | –ascii                                             |
| -b   | –binary 用binary的方式上传下载，不解释字符为ascii  |
| -e   | –escape 强制escape 所有控制字符，比如Ctrl+x，DEL等 |

* rar,gif等文件文件采用 -b 用binary的方式上传。
* 文件比较大而上传出错的话，采用参数 -e
* 如果用不带参数的rz命令上传大文件时，常常上传一半就断掉了，很可能是rz以为上传的流中包含某些特殊控制字符，造成rz提前退出。

![](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104161308954.png)

```shell
ll  #查看上传文件
```

![image-20221104161504941](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104161504941.png)

#### 2 解压

```shell
tar -zxvf zookeeper-3.4.13.tar.gz -C /usr/local/app/
```

| 选项 | 含义                               |
| ---- | ---------------------------------- |
| -C   | 解压到指定目录                     |
| -z   | 通过gzip过滤归档，支持gzip解压文件 |
| -x   | 对 tar 包做解打包操作              |
| -v   | 显示解打包的具体过程               |
| -f   | 指定要解压的 tar 包的包名          |

**![image-20221104161901965](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104161901965.png)**

#### 3 配置环境变量

1. 查看zookeeper安装路径

```shell
pwd
```

![image-20221104173236244](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104173236244.png)

2. 在/etc下添加配置文件，编辑配置文件

```shell
vim /etc/profile.d/mycluster.sh 
```

mycluster可以是随便的名字，但是要在/etc/profile.d/目录下

在文件末尾添加以下环境变量配置:

```shell
export ZOOPEEKER_HOME=/usr/local/app/zookeeper-3.4.13
export PATH=$PATH:$ZOOPEEKER_HOME/bin
```

![image-20221104174148561](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104174148561.png)

运行以下命令使环境变量生效

```shell
source /etc/profile.d/mycluster.sh
```

#### 4 核心配置文件

![image-20221104174452973](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104174452973.png)

初次使用 ZooKeeper 时, 需要将 $ZOOKEEPER_HOME/conf 目录下的 zoo_sample.cfg 重命名为 zoo.cfg

使用以下命令

~~~shell
 mv zoo_sample.cfg zoo.cfg
~~~

![image-20221104174741651](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104174741651.png)

zoo.cfg默认配置文件内容

```shell
# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial 
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between 
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just 
# example sakes.
dataDir=/tmp/zookeeper
# the port at which the clients will connect
clientPort=2181
# the maximum number of client connections.
# increase this if you need to handle more clients
#maxClientCnxns=60
#
# Be sure to read the maintenance section of the 
# administrator guide before turning on autopurge.
#
# http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
#
# The number of snapshots to retain in dataDir
#autopurge.snapRetainCount=3
# Purge task interval in hours
# Set to "0" to disable auto purge feature
#autopurge.purgeInterval=1
```

配置项说明如下:

| 参数                      | 含义                                                         |
| ------------------------- | ------------------------------------------------------------ |
| tickTime                  | ZooKeeper 中使用的基本时间单元, 以毫秒为单位, 默认值是 2000。它用来调节心跳和超时。例如, 默认的会话超时时间是两倍的 tickTime |
| initLimit                 | 默认值是 10, 即 tickTime 属性值的 10 倍。它用于配置允许 followers 连接并同步到 leader 的最大时间。如果 ZooKeeper 管理的数据量很大的话可以增加这个值 |
| syncLimit                 | 默认值是 5, 即 tickTime 属性值的 5 倍。它用于配置leader 和 followers 间进行心跳检测的最大延迟时间。如果在设置的时间内 followers 无法与 leader 进行通信, 那么 followers 将会被丢弃 |
| dataDir                   | ZooKeeper 用来存储内存数据库快照的目录, 并且除非指定其它目录, 否则数据库更新的事务日志也将会存储在该目录下。建议配置 dataLogDir 参数来指定 ZooKeeper 事务日志的存储目录 |
| clientPort                | 服务器监听客户端连接的端口, 也即客户端尝试连接的端口, 默认值是 2181 |
| maxClientCnxns            | 在 socket 级别限制单个客户端与单台服务器之前的并发连接数量, 可以通过 IP 地址来区分不同的客户端。它用来防止某种类型的 DoS 攻击, 包括文件描述符耗尽。默认值是 60。将其设置为 0 将完全移除并发连接数的限制 |
| autopurge.snapRetainCount | 配置 ZooKeeper 在自动清理的时候需要保留的数据文件快照的数量和对应的事务日志文件, 默认值是 3 |
| autopurge.purgeInterval   | 和参数 autopurge.snapRetainCount 配套使用, 用于配置 ZooKeeper 自动清理文件的频率, 默认值是 1, 即默认开启自动清理功能, 设置为 0 则表示禁用自动清理功能 |

修改zoo.cfg配置文件

```shell
ticketTime=2000
clientPort=2181
dataDir=/usr/local/app/zookeeper-3.4.13/data
dataLogDir=/usr/local/app/zookeeper-3.4.13/logs
```

![image-20221104175959866](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104175959866.png)

#### 5 启动zookeeper服务

~~~shell
zkServer.sh start
~~~

1. 启动服务信息如下

![image-20221104180439101](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104180439101.png)

2. 查看zookeeper服务进程

~~~shell
jps
~~~

![image-20221104180525262](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104180525262.png)

3. 查看ZooKeeper 节点模式

```shell
zkServer.sh status
```

![image-20221104191348999](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104191348999.png)

在单机模式中, Mode 的值是 "standalone"。

4. 停止 ZooKeeper 服务

想要停止 ZooKeeper 服务, 可以使用如下命令

```shell
zkServer.sh stop
```

![image-20221104191556866](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104191556866.png)

### **2 zookeeper集群安装模式**

#### 1 zoo.cfg配置

在 master 机器上, 在单机模式的配置文件下增加或修改下列配置（添加后3行配置）

```shell
ticketTime=2000
clientPort=2181
dataDir=/usr/local/app/zookeeper-3.4.13/data
dataLogDir=/usr/local/app/zookeeper-3.4.13/logs
syncLimit=5
initLimit=10
server.1=master:2888:3888
server.2=slave1:2888:3888
server.3=slave2:2888:3888
```

![image-20221104195716882](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104195716882.png)

相关配置说明:

- 集群模式中, 集群中的每台机器都需要感知其它机器, 在 zoo.cfg 配置文件中, 可以按照如下格式进行配置, 每一行代表一台服务器配置:

```shell
 server.id=host:port:port
```

- id 被称为 Server ID, 用来标识服务器在集群中的序号。同时每台 ZooKeeper 服务器上, 都需要在数据目录(即 dataDir 指定的目录) 下创建一个 myid 文件, 该文件只有一行内容, 即对应于每台服务器的Server ID

- ZooKeeper 集群中, 每台服务器上的 zoo.cfg 配置文件内容一致。
- server.1 的 myid 文件内容就是 "1"。每个服务器的 myid 内容都不同, 且需要保证和自己的 zoo.cfg 配置文件中 "server.id=host:port:port" 的 id 值一致。
- id 的范围是 1 ~ 255。

#### 2 创建myid文件

在 dataDir 指定的目录下 (即/usr/local/app/zookeeper-3.4.13/data目录) 创建名为 myid 的文件, 文件内容和 zoo.cfg 中当前机器的 id 一致。根据上述配置, master 的 myid 文件内容为 1

```shell
cd /usr/local/app/zookeeper-3.4.13/data
vim myid
```

![image-20221104192313573](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20221104192313573.png)

 #### 3 将文件分发到slave1节点和slave2节点

```shell
scp -r /usr/local/app/zookeeper-3.4.13/  slave1:/usr/local/app/
scp -r /usr/local/app/zookeeper-3.4.13/  slave2:/usr/local/app/
```

![image-20221104192906989](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104192906989.png)

#### 4 在子节点中查看分发文件

1. 在slave1节点中查看文件

![image-20221104193000406](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104193000406.png)

2. 在slave2节点中查看文件

![image-20221104193109597](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104193109597.png)

#### 5 slave配置

为 slave1 和 slave2 配置 zoo.cfg 和 myid 文件。zoo.cfg文件内容相同, slave1 的 myid 文件内容为 2, slave2 的 myid 文件内容为 3。

1. slave1节点配置myid

![image-20221104193338202](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104193338202.png)

2. slave2节点配置myid

![image-20221104193415252](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104193415252.png)

3.  将环境变量分发到slave子节点

```shell
scp -r /etc/profile.d/mycluster.sh slave1:/etc/profile.d/
scp -r /etc/profile.d/mycluster.sh slave2:/etc/profile.d/
```

![image-20221104193726115](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104193726115.png)

在slave1和slave2中分别执行命令

```shell
source /etc/profile.d/mycluster.sh 
```

让环境变量立即生效

#### 6 启动zookeeper集群服务

1. 分别在master、slave1、slave2中执行以下启动命令

```shell
zkServer.sh start
```

![image-20221104195954653](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104195954653.png)

2. 查看zookeeper集群服务器信息

```shell
zkServer.sh status
```

![image-20221104200037027](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104200037027.png)

master 和 slave1 两台服务器的 Mode 值均为 follower, 表明它们在集群中的角色为 Follower。

slaves2 服务器的 Mode 值为 leader, 表明它在集群中的角色为 Leader。

#### 7 zookeeper集群服务测试

进入客户端

```shell
zkCli.sh
```

![image-20221105111057438](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221105111057438.png)

查看节点

```shell
ls /
```

![image-20221105111254818](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221105111254818.png)

#### 8 异常处理

![image-20221104194422877](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104194422877.png)

此错误说明是配置文件中错误

![image-20221104195011777](zookeeper%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221104195011777.png)

我的节点名为slave1和slave2，所以配置错误