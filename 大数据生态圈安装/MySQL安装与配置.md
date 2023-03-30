## MySQL安装与配置

### 1 查看Linux中自带的MySQL

1. 查看Linux是否安装了MySQL数据库

~~~shell
rpm -qa | grep mysql
rpm -qa | grep mariadb
~~~

![image-20221111161325743](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221111161325743.png)

2. 删除Linux中自带的数据库并查看

~~~shell
rpm -e mariadb-libs-5.5.56-2.el7.x86_64 --nodeps
rpm -qa | grep mysql
rpm -qa | grep mariadb
~~~

![image-20221111162033237](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221111162033237.png)

### 2 MySQL安装包的上传与解压

1. 上传已经下载好的MySQL压缩包

~~~shell
rz
~~~

![image-20221111162321305](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221111162321305.png)

2. 查看是否上传成功

```shell
ll
```

![image-20221111162414446](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221111162414446.png)

3. 解压

```shell
tar -zxvf mysql-5.6.33-linux-glibc2.5-x86_64.tar.gz 
```

![image-20221113142522921](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113142522921.png)

4. 添加MySQL软连接

```shell
ln -s mysql-5.6.33-linux-glibc2.5-x86_64 mysql
```

>ln是link的缩写,在Linux中 ln 命令的功能是为某一个文件在另外一个位置建立一个同步的链接，当我们需要在不同的目录，用到相同的文件时，我们不需要在每一个需要的目录下都放一个必须相同的文件，我们只要在某个固定的目录，放上该文件，然后在其它的目录下用ln命令链接它就可以，不必重复的占用磁盘空间

| 参数                                          | 含义                                                         |
| --------------------------------------------- | ------------------------------------------------------------ |
| -b或--backup                                  | 删除，覆盖目标文件之前的备份                                 |
| -d或-F或--directory                           | 建立目录的硬连接                                             |
| -f或--force                                   | 强行建立文件或目录的连接，不论文件或目录是否存在             |
| -i或--interactive                             | 覆盖既有文件之前先询问用户                                   |
| -n或--no-dereference                          | 把符号连接的目的目录视为一般文件                             |
| -s或--symbolic                                | 对源文件建立软链接(符号连接)，而非硬连接                     |
| -S<字尾备份字符串>或--suffix=<字尾备份字符串> | 用"-b"参数备份目标文件后，备份文件的字尾会被加上一个备份字符串，预设的字尾备份字符串是符号"~"，可通过"-S"参数来改变它 |
| -v或--verbose                                 | 显示指令执行过程                                             |
| -V<备份方式>或--version-control=<备份方式>    | 用"-b"参数备份目标文件后，备份文件的字尾会被加上一个备份字符串，这个字符串不仅可用"-S"参数变更，当使用"-V"参数<备份方式>指定不同备份方式时，也会产生不同字尾的备份字符串 |

![image-20221113142828467](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113142828467.png)

### 3 添加系统MySQL组和MySQL用户

1. 添加MySQL组

```shell
groupadd mysql
```

2. 添加MySQL用户

```shell
useradd -r -g mysql mysql
```

| 参数 | 含义                                         |
| ---- | -------------------------------------------- |
| －c  | 加上备注文字，备注文字保存在passwd的备注栏中 |
| －d  | 指定用户登入时的启始目录                     |
| －D  | 变更预设值                                   |
| －e  | 指定账号的有效期限，缺省表示永久有效         |
| －f  | 指定在密码过期后多少天即关闭该账号           |
| －g  | 指定用户所属的群组                           |
| －G  | 指定用户所属的附加群组                       |
| －m  | 自动建立用户的登入目录                       |
| －M  | 不要自动建立用户的登入目录                   |
| －n  | 取消建立以用户名称为名的群组                 |
| －r  | 建立系统账号                                 |
| －s  | 指定用户登入后所使用的shell                  |
| －u  | 指定用户ID号                                 |

![image-20221113144248741](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113144248741.png)

### 4 进入MySQL目录中操作与配置

1. 进入MySQL目录

```shell
cd mysql
```

2. 修改当前目录拥有者为mysql用户

```shell
chown -R mysql:mysql ./
```

![image-20221113144620224](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113144620224.png)

3. 安装数据库

```shell
scripts/mysql_install_db --user=mysql --basedir=/usr/local/app/mysql --datadir=/usr/local/app/mysql/data
```

![image-20221113145159119](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113145159119.png)

产生多了一个文件

![image-20221113145411243](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113145411243.png)

4. 修改当前目录拥有者为root用户

```shell
chown -R root:root ./
```

![image-20221113145645470](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113145645470.png)

5. 修改当前data目录拥有者为mysql用户

```shell
chown -R mysql:mysql data
```

![image-20221113145825575](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113145825575.png)

6. 添加开机启动

```shell
cp support-files/mysql.server /etc/init.d/mysql
```

把启动脚本放到开机初始化目录中

![image-20221113150130806](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113150130806.png)

### 5 启动MySQL服务

```shell
service mysql start
```

- 可能会报错，没有添加datadir和datadir

![image-20221113152018916](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113152018916.png)

### 6 登录MySQL

1. 第一次登录MySQL没有密码

```shell
/usr/local/app/mysql/bin/mysql
```

![image-20221113153319312](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113153319312.png)

2. 设置root用户的密码

- 使用MySQL数据库

```shell
 use mysql;
```

![image-20221113153506955](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113153506955.png)

- 执行设置密码的命令

```shell
update user set password=password("root") where user="root";
```

![image-20221113153629136](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113153629136.png)

- 刷新权限

```shell
flush privileges;
```

![image-20221113153814421](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113153814421.png)

- 退出数据库

```shell
exit;
```

![image-20221113153748190](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113153748190.png)

- 总的命令组成

![image-20221113153904765](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113153904765.png)

3. 用新密码重新进入MySQL

```shell
 /usr/local/app/mysql/bin/mysql -u root -p
```

![image-20221113154141586](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113154141586.png)

- 退出MySQL数据库

```shell
quit;
```

### 7 MySQL数据库测试

1. 查看数据库

```mysql
show databases;
```

![image-20221113155345113](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113155345113.png)

2. 使用数据库

```mysql
use test;
```

![image-20221113155418723](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113155418723.png)

3. 创建表

```mysql
create table emp(
id int comment '编号',
name varchar(10) comment '姓名',
age tinyint unsigned comment '年龄'
)comment '员工表';
```

![image-20221113155622136](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113155622136.png)

4. 查看表

```mysql
show tables;
```

![image-20221113155652021](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113155652021.png)

5. 在emp表中插入数据

```mysql
INSERT INTO emp (id, name, age) VALUES (1, '张三', 20);
INSERT INTO emp (id, name,  age) VALUES (2, '张无忌',18);
```

- 第一次插入中文数据时可能会报编码错误

```mysql
ERROR 1366 (HY000): Incorrect string value: '\xE5\xBC\xA0\xE4\xB8\x89' for column 'name' at row 1
```

解决方法查看异常处理

6. 查看表中数据

```mysql
select * from emp;
```

![image-20221113162401883](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113162401883.png)

### 8 异常处理

- 卸载Linux中自带的数据库时出现依赖错误

![image-20221111161627568](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221111161627568.png)

解决方法

~~~shell
rpm -e mariadb-libs-5.5.56-2.el7.x86_64 --nodeps
~~~

| 参数     | 含义                             |
| -------- | -------------------------------- |
| --nodeps | --nodeps就是安装时不检查依赖关系 |

- 第一次启动时报错

![image-20221113150452417](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113150452417.png)

问题：没有datadir和basedir目录和路径或配置错误

```shell
[root@master mysql]# service mysql start
/etc/init.d/mysql: line 256: my_print_defaults: command not found
/etc/init.d/mysql: line 276: cd: /usr/local/mysql: No such file or directory
Starting MySQL ERROR! Couldn't find MySQL server (/usr/local/mysql/bin/mysqld_safe)
```

由/usr/local/mysql可以看到是我们的目录错误，我们配置的目录是/usr/local/app/mysql

所以需要修改support-files/mysql.server配置文件里面的datadir和basedir目录路径

![image-20221113152131817](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113152131817.png)

5. 重新把启动脚本放到开机初始化目录中，覆盖原来的文件

```shell
cp support-files/mysql.server /etc/init.d/mysql
```

![image-20221113151222714](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113151222714.png)

6. 启动MySQL服务,成功启动

```shell
service mysql start
```

![image-20221113152018916](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113152018916.png)

- 插入中文数据时报错

![image-20221113155955555](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113155955555.png)

很明显是编码问题，查看表的编码

```mysql
show create table  emp;
```

![image-20221113160305292](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113160305292.png)

可以看出，emp表的编码为拉丁格式(Latin1)

解决方法

- 第一种方法，修改此表的编码格式，只对此表有用 

1.修改此表的编码格式

```mysql
alter table emp convert to charset utf8;
```

![image-20221113160628883](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113160628883.png)

2. 再次查看此表的编码

```mysql
show create table  emp;
```

![image-20221113160718457](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113160718457.png)

3. 再次插入数据测试

![image-20221113160753264](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113160753264.png)

- 第二方法，修改MySQL默认的编码格式

1. 先查看数据库默认的编码格式

```mysql
 show  variables  like '%char%';
```

![image-20221113160957072](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113160957072.png)

可以看到默认是拉丁格式(latin1)

2. 修改MySQL中的my.cnf配置文件

```shell
vi my.cnf
```

添加以下内容

```mysql
[client]
default-character-set = utf8

[mysqld]
default-storage-engine = INNODB
character-set-server = utf8
collation-server = utf8_general_ci
```

![image-20221113161353571](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113161353571.png)

3. 重新启动MySQL服务

```shell
service mysql restart
```

![image-20221113161746333](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113161746333.png)

4. 再次进入MySQL查看默认编码

```mysql
show  variables  like '%char%';
```

![image-20221113161906977](MySQL%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.assets/image-20221113161906977.png)

成功修改