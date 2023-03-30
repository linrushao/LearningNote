## Openstack系统创建实例

### Step1 上传镜像文件

①输入账号、密码登录Openstack网页10.10.10.254,

![image-20221129200522405](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129200522405.png)

1 创建镜像

①点击计算→镜像

- 点击创建镜像按钮

![image-20221129200724752](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129200724752.png)

- 镜像名称自己命名，上传已下载好的镜像文件。

![image-20221129201022505](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129201022505.png)

- 选择已下载完成的镜像，因为宿主机环境比较吃配置，在电脑运行起来比较慢，是正常现象。下载镜像的网站可在官方下载（https://download.cirros-cloud.net/0.6.1/）。

![image-20221129201433324](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129201433324.png)

- 镜像格式选择QCOW2-QEMU模拟器

![image-20221129201512491](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129201512491.png)

- 其他都不用更改，直接点击创建即可。

![image-20221129201542737](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129201542737.png)

然后显示在运行中，则创建成功了。

![image-20221202091907599](%E4%BB%BB%E5%8A%A1%E4%BA%8C%EF%BC%9AOpenstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221202091907599.png)

### **Step2**：创建实例类型

① 点击计算→实例类型

![image-20221129201758411](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129201758411.png)

- 点击创建实例类型

![image-20221129201947011](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129201947011.png)

- 因为机器性能的问题，建议内存、CPU等都按最小的设定。设置如图所示。

![image-20221129202011136](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129202011136.png)

②创建网络

- 点击项目→网络→创建网络

![image-20221129202130167](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129202130167.png)

- 网络的设置如图所示。

![image-20221129202205327](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129202205327.png)

- 子网的设置如图：

![image-20221129202250490](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129202250490.png)

- 子网详见不用更改，直接点击创建，就可以网络的创建了。

![image-20221129202333414](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129202333414.png)

- 查看镜像是不是上传成功了，如图显示运行中，则表示镜像运行没有问题。

![image-20221129202423846](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129202423846.png)

那么到这里，创建虚拟机的准备工作就完成了。

### Step3：配置实例环境

那么接下来就可以开始创建实例。在创建实例之前，还需要做一些配置工作。要做配置工作，需要打开远程工具软件xshell。

①进入到系统后，输入sudo su 进入到管理用户权限。输入cd ~，进入到用户主目录。

```shell
sudo su
cd ~
```

![image-20221129202936447](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129202936447.png)

这里需要检查nova服务是否正常。输入命令：

```shell
source admin-openrc.sh
```

进入到Openstack环境。输入命令：

```shell
openstack
```

![image-20221129204505410](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129204505410.png)

可以看到nova的结构服务。并且这些服务如图所示是显示正常的。输入命令：

```shell
compute service list
```

![image-20221129204552994](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129204552994.png)

输入exit，则退出。

![image-20221129204612635](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129204612635.png)

②也可以使用docker ps查看服务是否正常使用。相对于传统的方式，我们这套安装更加简单。不用手动安装这些服务。输入命令:

```shell
docker ps
```

![image-20221129204714247](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129204714247.png)

③进入到容器的命令：看到nova-compute代表已经进入到容器内部了

```shell
docker exec -it nova_compute bash
```

![image-20221129204759403](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129204759403.png)

④进入到/var/log/nova目录下，再输入ls -l查看，输入命令：

```shell
cd /var/log/nova
```

![image-20221129204853182](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129204853182.png)

输入exit退出。因为配置文件收集到了kolla目录下，所以需要到kolla目录下才能查看文件。【相当于openstack中的文件和Linux系统的文件绑定在一起，在Linux中修改文件后会同步到openstack文件中】

![image-20221129204930872](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129204930872.png)

⑤进入到/var/log/kolla/目录中。如下图所示可以看到这里有Openstack的文件。输入命令：

```shell
cd /var/log/kolla/
```

![image-20221129205020589](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129205020589.png)

进入到/var/log/kolla/nova/目录下，输入命令：

```shell
cd /var/log/kolla/nova/
```

![image-20221129205109419](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129205109419.png)

在nova目录下可以查看/var/log/kolla/nova/nova-compute的日志文件。这里是记录你在Openstack系统上的操作。输入命令：

```shell
vi /var/log/kolla/nova/nova-compute.log
#或
cat /var/log/kolla/nova/nova-compute.log
```

![image-20221129205159503](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129205159503.png)

⑥进行到这里，我们还需要修改容器的配置文件。进入容器的配置文件命令是？

进入到容器的命令：docker exec -it nova_compute bash。看到nova-compute代表已经进入到容器内部了。

```shell
docker exec -it nova_compute bash
```

![image-20221129205325050](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129205325050.png)

进入到/etc/nova目录，输入命令：

```shell
cd etc/nova
```

![image-20221129205354545](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129205354545.png)

进入到系统文件。找到libvirt下的virt_type。将kvm修改为qemu。退出并保存wq。

输入命令：

```shell
vi nova.conf
```

修改为以下内容

```shell
virt_type = qemu
```

![image-20221129205546764](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129205546764.png)

输入命令exit退出容器。

⑦重启容器，相当于把服务重启了。输入命令：

```shell
docker restart nova_compute
```

![image-20221129205735016](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129205735016.png)

以上方法是每次电脑重启了，相当于配置文件又会回到之前的配置。所以，需要修改宿主机的配置文件，才能保证每次系统重启后文件是你已经修改过的文件

⑧进入到/etc/kolla/目录下，可以看到kolla下的目录是比较详细的。每一个目录对应一个容器。输入命令：

```shell
cd /etc/kolla/
```

![image-20221129205838144](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129205838144.png)

进入到/etc/kolla/nova-compute/。可以看到这里有两个配置文件config和nova文件。

```shell
cd /etc/kolla/nova-compute/
```

![image-20221129205904210](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129205904210.png)

进入到系统文件。找到libvirt下的virt_type。将kvm修改为qemu。退出并保存wq。

输入命令：

```shell
vi nova.conf
```

修改以下内容：

```shell
[libvirt]
connection_uri = qemu+tcp://10.10.10.2/system
virt_type = qemu
```

![image-20221129210012797](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129210012797.png)

查看config.json文件，这里有显示原配置文件的路径信息以及kolla容器的路径等信息。输入命令：

```shell
vi config.json
```

![image-20221129210128176](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129210128176.png)

重启容器。输入命令：

```shell
docker restart nova_compute
```

![image-20221129210209465](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129210209465.png)

在重启完之后，要docker ps查看容器是否正常运行还是被中断。输入命令：

```shell
docker ps
```

![image-20221129210413211](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129210413211.png)

如果哪个容器没有启动成功。那么就使用命令docker restart name。name是你没有启动成功的容器。这一步很重要。大家务必多次docker ps。确保容器都正常运行。

配置文件就已经修改成功了，可以开始实例。

### step4 创建实例

①点击项目→计算→实例→创建实例

![image-20221129210800913](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129210800913.png)

填写如图所示信息

- 详情

![image-20221129210840134](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129210840134.png)



- 源：点击箭头。选择已创建好的

![image-20221129211028946](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129211028946.png)

发现转到了已分配处

![image-20221129210956409](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129210956409.png)

- 实例类型：点击箭头。选择已创建好的

![image-20221129211204572](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129211204572.png)

其他的与原来保持一样，完成好后。点击创建实例按钮完成创建。

![image-20221129211249713](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129211249713.png)

如果没有问题，则创建成功，如下图所示。

![image-20221130113403738](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221130113403738.png)

点击实例名称linrushao-davy。linrushao-davy就是我们创建的虚拟机。可以看到虚拟机的日志，控制台，日志文件等。

![image-20221130113633183](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221130113633183.png)

点击日志，查看日志信息。

![image-20221130113659490](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221130113659490.png)

点击接口，查看接口信息

![image-20221130113843239](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221130113843239.png)



打开控制台。输入账号和密码。系统有提示账号和密码信息。

![image-20221130113942849](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221130113942849.png)



到此呢，Openstack系统的虚拟机就已经完成了。

### 异常处理

- 创建实例失败

![image-20221129211346679](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221129211346679.png)

查看报错信息，直接在控制台查看报错信息

![image-20221202094329475](%E4%BB%BB%E5%8A%A1%E4%BA%8C%EF%BC%9AOpenstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221202094329475.png)

或者在/var/log/kolla/nova/目录下查看里面所有组件的日志信息，查看报错详情

![image-20221202094754857](%E4%BB%BB%E5%8A%A1%E4%BA%8C%EF%BC%9AOpenstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221202094754857.png)

比如查看nova-compute.log日志文件

![image-20221202094635160](%E4%BB%BB%E5%8A%A1%E4%BA%8C%EF%BC%9AOpenstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221202094635160.png)

原因：镜像有问题

解决方法：换一个img镜像

![image-20221130113440413](Openstack%E7%B3%BB%E7%BB%9F%E5%88%9B%E5%BB%BA%E5%AE%9E%E4%BE%8B.assets/image-20221130113440413.png)
