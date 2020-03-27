# 在阿里云上创建CentOS 7.4实例并配置Windows远程桌面访问——xrdp

## 1、运行以下命令安装GNOME桌面

```
yum groupinstall GNOME Desktop Environment -y
```

安装需要较长时间。

## 2、默认库不包含xrdp，需要安装epel库。

```bash
yum install epel-release
```

## 3、安装xrdp

```bash
yum install xrdp
```

## 4、安装tigervnc-server

```bash
yum install tigervnc-server
```

## 5、如果需要客户端，可同时安装tigervnc（可选）

```bash
yum install tigervnc
```

## 6、启动xrdp服务，并设置为开机启动

```bash
# 启动xrdp服务
systemctl start xrdp

#设置为开机启动
systemctl enable xrdp
```

## 7、查看xrdp服务是否正常启动

```bash
# 如果看到Active则说明正常
systemctl status xrdp.service 

# 看xrdp和xrdp-sesman是否正常启动
netstat -antup|grep xrdp 
```

## 8、关闭防火墙,或者打开防火墙3389端口

```bash
systemctl stop firewalld.service
systemctl disable firewalld.servie

# 或者打开3389端口
firewall-cmd --permanent --zone=public --add-port=3389/tcp
firewall-cmd --reload
```

至此，可以使用windows的远程桌面连接Linux。