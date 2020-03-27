# 在阿里云上创建CentOS 7.4实例并配置远程图形化桌面访问——VNC Server

您可以使用本文提供的脚本在Linux实例上自动安装并运行VNC Server，实现远程图形化管理Linux服务器。目前，该脚本仅适用于CentOS实例，会在CentOS实例中安装GNOME桌面环境。

## 使用说明

这部分内容以CentOS 7.4 64位操作系统为例，说明如何在Linux实例里自动安装并运行VNC Server，使您可以从Windows系统通过VNC Viewer远程连接到Linux实例。

## 前提条件

您的实例处于 **运行中** 状态。如果实例未启动，先启动实例。

您已经在Windows系统里下载并安装了 [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)。

## 操作步骤

### 1、远程连接Linux实例（方法略）

### 2、运行命令下载脚本install_vnc_server.sh

```bash
wget http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/41181/cn_zh/1504062842088/install_vnc_server.sh
```

### 3、以root身份运行脚本，安装VNC Server

```bash
bash install_vnc_server.sh
```

安装需要较长的时间。当屏幕上出现以下信息时，表示VNC Server安装完成。您需要记录显示的随机密码（下文将介绍怎样设置密码）。

> **说明**：如果脚本执行报错可以多尝试几次。

![](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AliCloud/VNC%20Server.png?raw=true)

### 4、运行以下命令，在返回结果中查看Xvnc服务正在使用的端口

```bash
netstat -tulnp
```

![](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AliCloud/%E6%9F%A5%E7%9C%8BXvnc%E6%9C%8D%E5%8A%A1%E6%AD%A3%E5%9C%A8%E4%BD%BF%E7%94%A8%E7%9A%84%E7%AB%AF%E5%8F%A3.png?raw=true)

> 上图表示VNC Server正在使用的端口为TCP 5901和6001，其中：
>
> **TCP 5901**：允许VNC客户端通过RFB协议连接VNC Server。使用VNC Viewer连接实例时选择这个端口。
>
> TCP 6001：允许Windows X连接VNC Server。

### 5、在实例所在安全组中，添加安全组规则，放行Xnvc服务需要的端口。具体添加方法略。

在本示例中需要添加2条安全组规则，分别放行TCP 5901和TCP 6001端口。具体规则如下图所示。

![](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AliCloud/%E6%B7%BB%E5%8A%A0%E5%AE%89%E5%85%A8%E7%BB%84%E8%A7%84%E5%88%99.png?raw=true)

### 6、如果实例已经启用防火墙，需要添加规则放行端口。具体操作，以您实例里安装的防火墙软件为准（可选）。

在本示例中，以iptables为例，您可以依次执行以下命令添加规则放行TCP 5901和6001端口：

```bash
iptables -A INPUT -p tcp --dport 5901 -j ACCEPT
iptables -A INPUT -p tcp --dport 6001 -j ACCEPT
service iptables save
```

> 提示：记得**重启**CentOS7.4

### 7、运行以下命令，并按界面提示设置VNC Server连接密码

```bash
vnspasswd

[root@CentOS ~]# vncpasswd
Password:
Verify:
Would you like to enter a view-only password (y/n)? y
Password:
Verify:
[root@CentOS ~]# 

# 可以根据自己情况选择y/n
```

### 8、运行以下命令设置开机启动VNC Server。

```bash
systemctl enable vncserver@:1.service
```

### 9、运行以下命令启动VNC Server。

```bash
systemctl start vncserver@:1.service
```

### 10、 运行以下命令确认服务是否已经启动。

```bash
 ps -ef | grep vnc
```

![](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AliCloud/%E7%A1%AE%E8%AE%A4vnc%E6%9C%8D%E5%8A%A1%E6%98%AF%E5%90%A6%E5%90%AF%E5%8A%A8.png?raw=true)

如果返回以下类似结果，说明服务已经启动。

### 11、按以下步骤在本地Windows系统里通过VNC Viewer连接Linux实例：

1. 在本地Windows系统里启动VNC Viewer。

2. 在工具栏里，选择 **File** > **New Connection**。

3. 在 **Properties** 对话框中，配置如下信息后单击 OK：

   	**VNC Server**：输入 Linux 实例的公网 IP 地址：5901

           **Name**：根据自己需要输入一个连接名称，方便后期管理。

![](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AliCloud/%E9%85%8D%E7%BD%AEIP%E5%9C%B0%E5%9D%80.png?raw=true)

4. 在VNC Viewer主窗口，右击新建连接的图标，并在弹出菜单中选择 **Connect**。

5. 在弹出的 **Authentication** 对话框中，输入VNC Server安装结束后显示的随机密码或者在第7步设置的连接密码，并单击 **OK**。

> **注意**： 这里使用的密码并不是实例的登录密码。

至此，您已经成功登录到Linux实例。

### 常见问题

第一次登录CentOS 7.4实例时，系统提示我登录身份为root super user（如下图所示），我该怎么处理？

![](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AliCloud/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98.png?raw=true)

这是一个正常的提示。您可以按以下步骤操作：：

1. 选择 **Do not show me this again**。
2. 单击 **Close** 关闭对话框。
