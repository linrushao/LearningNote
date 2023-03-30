## 项目三：Openstack调通外部网络

使用我们创建好的虚拟机linrushao-davy访问到外部的网络，能够连接到Internet。可以使用网桥的模式使得内部的虚拟机也能连接到外部的网络。

### Step1：使用命令查看以太网的网段

使用快捷键win+R，输入cmd打开终端。

![image-20221130120716395](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130120716395.png)



输入命令ipconfig查看你的以太网地址网段。网络给我分配的ip地址是10.150.195.102。102就是我这台电脑的网段。10.150.192.1就是我电脑的网关。这两个信息在下面创建网络会用的到。【我所有的网络是WiFi，因为我没有连接网线，建议使用以太网，就是连接网线的】

![image-20221202094949711](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221202094949711.png)

### Step2：在管理员下创建网络

在管理员下的网络点击创建网络，一定是管理员下创建，这里的网络才具备权限。

![image-20221130141736008](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130141736008.png)

按照下图所示创建网络。

![image-20221130141834433](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130141834433.png)

按照下图创建子网。这里的子网网段（查看你电脑的网段是多少）要与你本机的电脑保持一致。子网网络地址的填写为10.152.xx.0/24。xx就是你的网段。

![image-20221130194120752](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130194120752.png)

子网详情填写如图所示。不要激活DHCP，因为地址是随机分配的，激活会产生物理冲突。地址池范围填写10.152.xx.150,10.152.xx.160。DNS服务器填写114.114.114.114。完成后点击创建按钮就可以创建网络。

![image-20221130151449041](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130151449041.png)

创建完网络后如图所示。

![image-20221130151949829](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130151949829.png)

### Step3：在管理员下创建路由

![image-20221130142439913](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130142439913.png)

在管理员下的网络点击创建路由。完成信息填写后点击新建路由即可。

![image-20221130142509338](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130142509338.png)

创建后的路由如图所示。

![image-20221130142532294](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130142532294.png)

点击路由route。

![image-20221130195525819](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130195525819.png)

进入到这个界面。

![image-20221130195545236](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130195545236.png)

点击增加接口按钮。子网直接选择已有的DEMO。

![image-20221130142722217](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130142722217.png)

创建好的路由如图所示。

![image-20221130152106559](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130152106559.png)

点击route,可以看到路由的概览，路由的信息如图所示。

![image-20221130194400282](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130194400282.png)

点击查看路由接口

![image-20221130194235910](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130194235910.png)

可以看到上图有我们虚拟机control01的IP地址是10.152.193.160（这个ip的网段是你自己主机的网段，要对应上来）。这个时候可以去电脑ping一下改ip地址，这个时候是连接不通的。

![image-20221130194512575](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130194512575.png)

### Step4：更改VirtualBox上的配置

点击设置按钮

![image-20221130143022592](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130143022592.png)



点击网络设置的网卡2

![image-20221130143041479](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130143041479.png)

在网卡2的模式里，连接方式选择桥接网卡，网卡（界面名称）选择Controller。点击高级按钮，则可以看到混杂模式。混杂模式选择全部允许。点击ok保存。

![image-20221130143144126](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130143144126.png)

### Step5：重启你的网卡enp0s8。

打开你的CRT（xshell也可以）需要登录管理者权限。输入命令：ip link,查看你电脑的网卡运行情况。

![image-20221130143323503](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130143323503.png)



输入命令： ip link set enp0s8 down。关闭网络

再输入命令：ip link set enp0s8 up。开启网络

![image-20221130143405080](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130143405080.png)

### Step6：ping一下网络

ping一下虚拟机的ip，如果能连接，则你的虚拟机ip已经生效，可以正常通网。

![image-20221130194547517](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130194547517.png)

### Step7：在实例里添加浮动ip

在实例里，点击绑定浮动IP。

![image-20221130152604706](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130152604706.png)

点击看看是否有IP地址

![image-20221130152645524](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130152645524.png)

显示没有浮动ip

![image-20221130152709495](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130152709495.png)

则点击旁边的+号按钮，再点击分配IP,即可。

![image-20221130194853596](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130194853596.png)

最后，出现管理浮动IP的关联。点击关联按钮。

![image-20221130194925122](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130194925122.png)

完成关联后，可以看到这里是有两个ip的。则关联成功了。我这里关联的ip是10.152.193.158。可以去ping一下，看看这台机网络的这个ip是否能通网。

![image-20221130194946641](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130194946641.png)



可以看到这里是能连通的。

![image-20221130193234161](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130193234161.png)

### Step8：测试我们创建的虚拟机能不能连通外网。

输入命令：ssh cirros@10.152.193.158（在终端上使用这个命令，只有win10以上版本才可支持）。输入yes。注意这个ip是我们刚创建的ip。输入完命令后，输入密码:gocubsgo。如图所示，本机的终端能够连接到虚拟机。

![image-20221130200459851](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130200459851.png)

输入命令：ip a,能够查到虚拟机的ip信息。

![image-20221130200531255](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130200531255.png)

输入命令：ping 114.114.114.114。如图所示，可以看到能够连接外网了。按ctrl c，终止访问。

![1](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/1.png)

输入命令：ping baidu.com。如图所示，可以看到能够连接百度了.按ctrl c，终止访问。

![2](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/2.png)

到此，虚拟机能够完成外网的连接。

### 异常处理

- openstack 云主机可以ping外网但ping不通浮动IP

![image-20221130180642426](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130180642426.png)

①在云主机安全规则添加条目：

![image-20221130190822187](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130190822187.png)

②.创建安全组，如下图：

![image-20221130193758668](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130193758668.png)

③添加完成的安全组

![image-20221130193833477](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130193833477.png)

结果：可以正常ping通

![image-20221130193906018](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130193906018.png)

- ssh cirros@10.152.193.158失败

![image-20221130200139014](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130200139014.png)

原因：ssh被openstack中的安全组给限制掉了，所有实例的22号端口都不能够被链接。

![image-20221130200244318](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130200244318.png)

解决方法：添加安全组

![image-20221130200324236](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130200324236.png)

结果：登录成功

![image-20221130200509460](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130200509460.png)

- 登录成功但是ping不同网络![image-20221130200702871](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130200702871.png)

原因：还是openstack中的安全组限制问题，以太网问题，我两的是wifi但是ping不同

解决方法：

- 如果我们不创建安全组，系统默认给所有实例使用default规则，选择项目->网络->安全组：
- 第一条规则使VM实例的因特网控制消息协议（ICMP）（ping命令）。 第二规则允许通过端口22，其用于通过SSH TCP连接。

![image-20221130201953488](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130201953488.png)



- 点击添加规则，选择所有TCP协议，方向为入口，其它默认

![image-20221130202137426](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130202137426.png)

![image-20221130202226872](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130202226872.png)







- 点击添加规则，选择所有ICMP协议，方向为入口，其它默认：

![image-20221130202109035](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130202109035.png)

![image-20221130202121212](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130202121212.png)





添加结果：

![image-20221130202251704](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130202251704.png)



运行结果：



![image-20221130210701449](%E9%A1%B9%E7%9B%AE%E4%B8%89%EF%BC%9AOpenstack%E8%B0%83%E9%80%9A%E5%A4%96%E9%83%A8%E7%BD%91%E7%BB%9C.assets/image-20221130210701449.png)





















