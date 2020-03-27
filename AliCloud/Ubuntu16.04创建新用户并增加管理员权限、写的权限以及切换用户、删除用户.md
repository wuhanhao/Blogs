# Ubuntu16.04创建新用户并增加管理员权限、写的权限以及切换用户/删除用户

*预计阅读时间： 5分钟*

**$是普通管理员（普通用户），#是系统管理员（超级用户，即root用户）**，在Ubuntu下，root用户默认是没有密码的，因此也就无法使用（据说是为了安全）。

#### 想用root的话，得给root用户设置一个密码：

```bash
 sudo passwd root 
```

#### 然后登录时用户名输入root，再输入密码就行了。

 ubuntu建用户最好用**adduser**，虽然**adduser**和**useradd**是一样的在别的linux糸统下，但是我在ubuntu下用useradd时，并没有创建同名的用户主目录。

例子：adduser user1 

这样他就会自动创建用户主目录，创建用户同名的组。

```bash
root@ubuntu:~# sudo adduser whh(所要创建的用户名)

[sudo] password for xx: 
输入xx用户的密码，出现如下信息 
正在添加用户"whh"… 
正在添加新组"whh" (1006)… 
正在添加新用户"whh" (1006) 到组"linuxidc"… 
创建主目录"/home/whh"… 
正在从"/etc/skel"复制文件… 
输入新的 UNIX 口令： 
重新输入新的 UNIX 口令： 
两次输入whh的初始密码，
出现的信息如下 passwd: 
password updated successfully 
Changing the user information for linuxidc
Enter the new value, or press ENTER for the default
Full Name []: 
Room Number []: 
Work Phone []: 
Home Phone []: 
Other []: 
Full Name []:

等信息一路回车 

这个信息是否正确？ [Y/n] y 
```

到此，用户添加成功。

#### 如果需要让此用户有**root**权限

执行命令： 

```bash
root@ubuntu:~# sudo vim /etc/sudoers
```

 修改文件如下： 

```bash
# User privilege specification 
root ALL=(ALL) ALL 
whh ALL=(ALL) ALL 
```

保存退出（命令为**：wq！**强制修改保存信息并退出），whh用户就拥有了**root**权限。

#### **查看所有用户信息**

```bash
awk -F':' '{ print $1}' /etc/passwd
```

#### 获取写权限

经本人测试，通过以上方法创建的新用户没有**写的权限**（也就是我们通常所说的文件/目录右下角有一个小锁），以下便是怎样赋予新用户**写的权限**的解决办法。

运行以下命令即可：

```bash
sudo chmod 777 -R 目录/文件
```

#### 切换用户

```bash
# 切换用户的命令
su username

# 从普通用户切换到root用户
sudo su
```

#### 彻底删除用户(帐户)

终端方法：以下用**newuser**代替想要删除的用户账户

```bash
# 在root用户下
userdel -r newuser
cd /home/
sudo rm -r newuser

# 在普通用户下
sudo userdel -r newuser
cd /home/
sudo rm -r newuser
```

因为需要彻底删除用户，所以加上-r的选项，在删除用户的同时一起把这个用户的宿主目录和邮件目录删除。

> 注意：可能会出现以下错误：
>
> userdel: user xxx is currently used by process 1923
>
> 意思是说：userdel：用户xxx当前由进程1923使用
>
> 只要重启电脑(reboot)，再运行以上命令即可。 