# Ubuntu 16.04 基于阿里云服务器远程桌面连接

## 1、安装xrdp 

```bash
sudo apt-get install xrdp
```

## 2、安装vnc4server 

我这里是安装xrdp的时候自动安装的。我看网上很多说是需要单独安装的。

## 3、安装xfce4

```bash
sudo apt-get install xubuntu-desktop
```

这个软件比较大，其实就是安装xubuntu桌面

## 4、配置xfce4 

```bash
echo "xfce4-session" >~/.xsession
```

创建.xsession文件并写入内容。

## 5、继续配置xfce4，打开文件手动编辑

```bash
sudo gedit /etc/xrdp/startwm.sh
```

在. /etc/X11/Xsession前一行插入

```bash
#此步很重要，不可或缺
xfce4-session
```

## 6、重启xrdp

```bash
sudo service xrdp restart
```

## 7、开启桌面共享功能

进入系统->首选项->桌面共享，或者直接搜索桌面共享

将【允许其他人查看您的桌面】这一项勾上，其他默认就行

到这一步基本上已经完成了，接下来就是来测试是否能正常连接到Ubuntu桌面

## 8、使用启动Windows远程桌面工具(mstsc) 

连接之后类型选择默认模式(sesman-xvnc)就行，填写**用户名和密码**之后就好了(PS：就是系统的用户登录账户和密码)

这样就成功连接到上了Ubuntu图形界面

## 9、修改tab键自动补全功能 

至此为止，远程桌面登录可以正常使用了，但是在终端中无法使用tab的自动补全功能，使用起来甚是不便，使用如下方法修改：
此法不需要重启系统，可以直接在远程桌面中设置，打开菜单->设置->窗口管理器

选择键盘，可以看到窗口快捷键中动作一列有“切换同一应用程序的窗口”选项，将该选项的快捷键清除后关闭窗口即可。这样修改后马上可以使用了。

至此，xrdp连接Ubuntu 16.04图形界面的所有步骤已完成。