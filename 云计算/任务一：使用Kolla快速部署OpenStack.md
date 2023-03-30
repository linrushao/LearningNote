## 使用Kolla快速部署OpenStack

### 1 安装

1. 双击打开已下载完成的VirtualBox-6.1.26-14.exe软件，点击下一步

![image-20221129162233444](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162233444.png)

2. 在这个界面选择要安装的功能组件，按顺序分别是主程序（必选），VirtualBox USB驱动支持（安装后可以支持外接USB），虚拟机的网络支持（包括桥接的跟主机模式的网络）最后一个就是VirtualBox的Python 2.X的支持。这里可以不用动直接默认就行了。安装路径默认在C盘，点击「 浏览 」选择其他的路径（比如D盘,如图所示），然后点击下一步

![image-20221129162409232](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162409232.png)

3. 此界面为选择快捷方式，分别是在开始菜单创建快捷方式，在桌面创建快捷方式，在快速启动栏创建，关联文件。这个可以根据自己的喜好来选择。然后点击下一步

![image-20221129162440685](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162440685.png)

4. 弹出警告界面，提示安装网络组件会重置当前网络，点击是

![image-20221129162515149](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162515149.png)

5. 准备安装，点击「安装」进行安装。

![image-20221129162541630](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162541630.png)

- 软件正在安装中。

![image-20221129162612036](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162612036.png)

![image-20221129162751710](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162751710.png)

- 提示是否信任软件，点安装

![image-20221129162732409](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162732409.png)

6. 弹出Windows安全提示框，勾选“始终信任来自Oracle Corporation的软件”，点击「 安装 」。安装完成界面，勾选表示安装完成后启动Oracle VM VirtualBox虚拟机，点击「 完成」

![image-20221129162824393](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162824393.png)

7. 打开Oracle VM VirtualBox管理器，你会发现界面已经自动转换为中文了。

- 提示更新，直接忽略

![image-20221129162919998](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162919998.png)

- 安装完成界面

![image-20221129162949099](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129162949099.png)

### 2 安装部署Openstack的虚拟机

> 环境：1台虚拟机，电脑配置要求4核8G内存40G存储2张主机模式网卡，第一张IP:10.10.10.0/24,第二张系统默认。第一张需要手动添加，vm可以开启VT虚拟化。

#### 1 主机网络配置

①工具栏：点击管理→主机网络管理器

![image-20221129163331618](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129163331618.png)

②进入主机网络管理器界面。这里有两个网络，一个是自动创建的，另外一个是需要手动去创建的网络。自动创建的网络ip是默认192.168.56.1

![image-20221129163639772](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129163639772.png)

③这里要特别注意的是第二个网络，也就是需要大家手动创建的网络，点击创建按钮，完成第二个网络的创建工作。

![image-20221129163529890](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129163529890.png)

④完成创建后，点击手动配置网卡。输入ip为10.10.10.1，网络掩码是255.255.255.0。这里务必要保持ip与如下图所示。后续的操作与这里是统一的。因为这里都是使用静态地址，所以在两个网络的DHCP服务器都显示不启用。完成后面点击应用就可以关闭主机网络管理器。

![image-20221129163848330](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129163848330.png)

- 点击应用后，手动IP地址发生改变

![image-20221129164129536](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129164129536.png)

#### 2 虚拟系统创建

①点击新建

- 虚拟机名称命名为node1。文件夹保存路径的硬盘需要至少20G。因为整个安装下来的文件是超过15G的（保存路径也可以保存在固态硬盘上）。虚拟机的类型选择linux。版本选择Red Hat(64-bit)。完成后点击下一步。

![image-20221129164404388](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129164404388.png)

②内存大小选择8192MB。内存大小不能小于8G，不然会安装失败。

![image-20221129164457033](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129164457033.png)

- 虚拟硬盘，选择【现在创建虚拟硬盘】

![image-20221129164540063](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129164540063.png)

- 虚拟硬盘文件类型选择默认即可

![image-20221129164616865](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129164616865.png)

- 存储在物理硬盘上，选择动态分配

![image-20221129164812313](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129164812313.png)

- 文件位置和大小，硬盘大小至少要40G大小，这里选择的是50G。

![image-20221129164850513](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129164850513.png)

- 点击创建按钮。创建完成后，还需要设置它的网络，启动光盘。

![image-20221129164950048](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129164950048.png)

③点击【设置】按钮

![image-20221129165105617](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129165105617.png)

- 网卡1设置仅主机模式，选择我们创建的网络，如下图所:

>在Oracle VM VirtualBox中设置网络需要至少两个网卡才能完成，一个是Oracle VM VirtualBox内部通信，一个用于外部网络和内部网络的通信

![image-20221129165207842](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129165207842.png)

- 网卡2设置，选择仅主机模式，选择系统自动创建的网络，【后期如果需要联网这需要修该网络连接方式为其它的连接方式，或者也可以添加其它的网卡】如下图所示：

![image-20221129165242021](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129165242021.png)

- 网络配置完成【部署测试只需要两个都设置为仅主机网络即可，后期如果需要连接外网，这直接修改网卡或者直接添加网络】

![image-20221129165332723](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129165332723.png)

④存储【插入光盘】

- 点击设置，点击存储

![image-20221129165631381](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129165631381.png)

- 选择一个虚拟光盘文件，找到存放iso文件的路径。

![image-20221129165849100](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129165849100.png)

- 选择已下载完成的虚拟盘

![image-20221129165944553](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129165944553.png)

- 插入光盘后界面【在启动虚拟机后，控制器：IDE中的光盘会直接添加到控制器：SATA中】

![image-20221129170031189](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129170031189.png)

⑤系统【配置虚拟机主要的虚拟硬件配置】

- 点击系统

![image-20221129170057380](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129170057380.png)

- 启动顺序只勾选光盘和硬盘。处理器的内核选择4。如下图所示。

启动顺序只勾选光盘和硬盘。

![image-20221129170156062](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129170156062.png)

处理器的内核选择4【这个主要是看自己电脑的配置，这里设置为1也可以，但是可能会比较慢】

![image-20221129170315837](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129170315837.png)

⑥点击启动按钮，启动虚拟机【启动虚拟机后键盘和鼠标都是在虚拟机中使用的，如果需要在虚拟机中弹出光标，需要按住键盘中右边的Ctrl】

![image-20221129170503004](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129170503004.png)

- 启动后会看到页面如图所示，这里有两种安装模式。第一种是安装我们的部署节点（docker,registry,kolla-ansible）。第二种是安装普通节点(docker)。我们选择第一种安装模式。点击第一个，回车就可以安装啦。安装过程是全自动的，等待安装完成就可以。

![image-20221129170546431](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129170546431.png)

- 安装过程查看【在安装过程中，可以看到我们安装的操作系统为CentOS Linux7】

![image-20221129170635620](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129170635620.png)

⑦安装成功后，进入到登录的界面。

![image-20221129171955998](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129171955998.png)

- 输入账号和密码。账号是kolla,密码是kollapass

![image-20221129172207367](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129172207367.png)

#### 3 安装完成后操作

- 系统上是不能复制密码的，并且相对较麻烦。所以要借用远程软件工具xshell。主机名输入：10.10.10.2。用户名输入kolla。密码是kollapass。

![image-20221129173134700](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129173134700.png)

用户名【默认的用户名为：kolla】

![image-20221129173220081](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129173220081.png)

密码【默认密码是：kollapass】

![image-20221129173303735](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129173303735.png)

登录成功

![image-20221129173410020](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129173410020.png)

①进入到系统后，输入sudo su 进入到管理用户权限。输入cd ~，进入到用户主目录。

使用管理者操作权限和进入到用户主目录。输入命令：

```shell
sudo su
cd ~
```

![image-20221129202936447](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129202936447.png)

清理xshell屏幕命令：

```shell
clear
```

![image-20221129173500729](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129173500729.png)

#### 4 部署Openstack

- 进入到这里后，只要前面是跟着流程走的，特别是网络设置。那么就不需要配置其他内容，直接就可以部署Openstack了。在部署Openstack之前，需要检查下虚拟机能不能安装Openstack。

输入部署前检查命令：

```shell
kolla-ansible prechecks
```

![image-20221129173624948](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129173624948.png)

图里显示没有failed的，则证明检查完后是没有什么问题的。

![image-20221129173751725](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129173751725.png)

- 执行安装openstack命令：

```shell
kolla-ansible deploy
```

![image-20221129173815831](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129173815831.png)

安装的时间较长，这里大概需要15-20分钟。速度的快慢取决于你的电脑配置。

![image-20221129175312174](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129175312174.png)

这里显示failed为0。则显示Openstack系统部署安装成功了。

③输入命令：

```shell
docker ps
```

该命令主要是查看显示容器的数量，以及启动容器需要花费的时间。【STATUS为容器状态：启动多长时间或关闭多长时间】

![image-20221129175908505](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129175908505.png)

④请求令牌：

```shell
kolla-ansible post-deploy
```

我们系统，已经安装好了。这个命令是帮我们生成rc文件。有了rc文件，我们就可以去客户端调用Openstack的服务了。

![image-20221129180107610](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129180107610.png)

生成完成后，failed个数为0说明没有错误

![image-20221129180652887](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129180652887.png)

⑤拷贝令牌到当前目录：

```shell
cp /etc/kolla/admin-openrc.sh .
```

![image-20221129180723286](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129180723286.png)

⑥初始化环境：

```shell
source admin-openrc.sh 
```

![image-20221129180739465](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129180739465.png)

openstcak的客户端环境都已经包含在容器里面了。每一次进入容器都需要打开客户端。所以在这个版本里已经写好脚本。

⑦初始化环境之后，直接可以进入到open stack容器中，输入命令：

```shell
openstack
```

可以进入openstack环境。

![image-20221129180759030](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129180759030.png)

⑧进入到Openstack容器之后，查看服务列表输入命令：

```shell
service list
```

![image-20221129180824364](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129180824364.png)

输入ctrl d退出命令【或者是输入exit命令】。

```shell
ctrl d
```

![image-20221129180841544](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129180841544.png)

⑨查看Openstack账号的密码,,输入命令:

```shell
cat admin-openrc.sh
```

![image-20221129180911627](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129180911627.png)

- 利用浏览器登录

在浏览器中输入Openstack的网页ip地址：10.10.10.254

![image-20221129181126755](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129181126755.png)

输入账号：admin，密码是上图你复制的数据。登录网页

```shell
账号：admin
密码：0Ff8XXZLMKLWlHoiGieeWb6Lt7XsLI984f03QhnL
```

![image-20221129181236330](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129181236330.png)

成功登录页面【可以看到open stack内容的组件详情】

![image-20221129181326476](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129181326476.png)

### 3 异常处理

- 在输入docker ps命令报错

![image-20221129175534603](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129175534603.png)

原因:在普通用户下执行docker命令需要用sudo

临时解决方法：

```shell
sudo docker ps
```

- 输入openstack是报错

![image-20221129175534603](%E4%BD%BF%E7%94%A8Kolla%E5%BF%AB%E9%80%9F%E9%83%A8%E7%BD%B2OpenStack.assets/image-20221129175534603.png)

原因：权限问题

解决方法：直接切换为root用户

```shell
sudo su
```

