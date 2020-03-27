# **阿里云ECS服务器环境搭建—ubuntu 16.04 图形界面的安装**

### 1. 购买阿里云ECS服务器 ,并创建实例

```bash
（操作系统：Ubuntu16.04-64-bit，具体步骤，略）
```

### 2. 安装Xshell或者Putty

```bash
（官网下载，略）
```

### 3. 安装步骤

#### 3.1 更新软件库

```bash
sudo apt-get update
```

#### 3.2 升级软件
```bash
sudo apt-get upgrade
```

#### 3.3 安装ubuntu桌面系统

```bash
sudo apt-get install ubuntu-desktop
```

- 运行过程需要手动确认两次，选择 Y。
- 安装完成之后，终端输入 **reboot**，重启服务器。
- 过程有点久，请耐心等待。

#### 3.4 配置root账号

- 重启之后，桌面环境就安装好了，但是远程连接进去，发现只能使用guest帐号，不能选择其他用户，而且不需要密码就能登录，登录进去还会有个警告信息！但是guest帐号地位太低了，几乎没什么权力。 
- **这个地方尤其需要注意**：因为远程进入阿里云服务器，只能使用guest帐号，但是guest帐号是没有权限修改这个文件的。所以，我们需要在windows端，**使用上面提到的putty或者Xshell工具，以root帐号（使用putty工具进入可以指定登录用户），远程登录进入**，这样就可以修改这个文件了。

```bash
cd /usr/share/lightdm/lightdm.conf.d 
vi 50-ubuntu.conf 
```

```bash
# 修改前
[Seat:*]
user-session=ubuntu

# 修改后
[Seat:*]
user-session=ubuntu
greeter-show-manual-login=true
allow-guest=false
```

- 按  **i、a、o** 		 编辑，在当前光标位置的左边添加文本
- 按 **esc**                      回到命令模式 
- 输入 **:wq**                 退出
- vi的具体操作可以参考这个文章：<https://www.cnblogs.com/doseoer/p/6241443.html>  

- 修改完文件之后，如上图执行**reboot**，重启服务器。重启之后就可以用root用户登录，但是登录后还是有警告，这个需要修改 **/root/.profile** 文件。  修改成如下所示： 

```bash
# 文件修改前
    # ~/.profile: executed by Bourne-compatible login shells.

    if [ "$BASH" ]; then
      if [ -f ~/.bashrc ]; then
        . ~/.bashrc
      fi
    fi
    mesg n || true

# 文件修改后
    # ~/.profile: executed by Bourne-compatible login shells.

    if [ "$BASH" ]; then
      if [ -f ~/.bashrc ]; then
        . ~/.bashrc
      fi
    fi
    tty -s && mesg n || true
```

- 再执行 **reboot** **命令**，重启服务器，重启之后，只有root用户，登录后也没有警告信息了。 

------

