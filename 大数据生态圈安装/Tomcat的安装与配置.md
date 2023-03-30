## Tomcat的安装与配置

### 1 Tomcat的上传与解压

- 检查linux是否安装tomcat ，执行命令

```shell
rpm -qa|grep tomcat 
```

![image-20221120111119714](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120111119714.png)

- Tomcat的上传，下载地址：[Apache Tomcat® - Apache Tomcat 8 Software Downloads](https://tomcat.apache.org/download-80.cgi#8.5.83)

![image-20221120111359292](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120111359292.png)

- 解压

```shell
tar -zxvf apache-tomcat-8.5.83.tar.gz
```

![image-20221120111804356](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120111804356.png)

- 重命名

```shell
mv apache-tomcat-8.5.83/ tomcat-8.5.83
```

![image-20221120111918678](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120111918678.png)

### 2 配置环境变量

- 编辑/etc/profile.d/mycluster.sh文件

```shell
vim /etc/profile.d/mycluster.sh
```

添加以下内容

```sh
#tomcat
export TOMCAT_HOME=/usr/local/app/tomcat-8.5.83
export PATH=$PATH:$TOMCAT_HOME/bins
```

![image-20221120112739930](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120112739930.png)

-  执行以下命令让配置文件立即生效

```shell
source /etc/profile.d/mycluster.sh
```

### 3 Tomcat的启动与关闭

- 执行以下启动命令

```shell
/usr/local/app/tomcat-8.5.83/bin/startup.sh
```

![image-20221120113048266](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120113048266.png)

- 查看 tomcat 是否启动成功

```shell
ps -ef | grep java
```

![image-20221120113257318](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120113257318.png)

- 验证是否启动成功

在浏览器输入 http:\\ip地址：8080。如果出现 tomcat 的主页则启动成功

![image-20221120113350417](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120113350417.png)

**注意**：如果看不到界面有可能是防火墙没关

关闭防火墙命令：

```shell
systemctl stop firewalld
systemctl status firewalld
```

![image-20221120113542267](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120113542267.png)

- 关闭tomcat

```shell
/usr/local/app/tomcat-8.5.83/bin/shutdown.sh
```

![image-20221120113722618](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120113722618.png)

查看Java进程

```shell
ps -ef | grep java
```

![image-20221120113747884](Tomcat%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221120113747884.png)