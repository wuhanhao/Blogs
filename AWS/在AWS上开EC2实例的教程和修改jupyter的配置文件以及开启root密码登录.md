# 在AWS上开EC2实例教程

## 1. 登录AWS账号，点击服务——>EC2——>实例

![控制台主页](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E6%8E%A7%E5%88%B6%E5%8F%B0%E4%B8%BB%E9%A1%B5.png?raw=true)

## 2. 点击实例——>启动实例

![实例](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E5%AE%9E%E4%BE%8B.png?raw=true)

## 3. 选择快速启动——>选择系统映像(AMI)，建议选择框框下面这个，并点击右边的选择按钮

![系统映像](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E7%B3%BB%E7%BB%9F%E6%98%A0%E5%83%8F.png?raw=true)

## 4. 选择实例类型，按需选择就行（注意：建议选择版本是：t2开头的）

### 4.1 并一路点击 下一步：... 直到点到 下一步：配置安全组

![实例类型](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E5%AE%9E%E4%BE%8B%E7%B1%BB%E5%9E%8B.png?raw=true)

### 4.2 选择一个现有安全组，并选择名称是default的安全组，最后点击 审核和启动

![配置安全组](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E9%85%8D%E7%BD%AE%E5%AE%89%E5%85%A8%E7%BB%84.png?raw=true)

## 5. 点击 启动 按钮

![实例启动](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E5%AE%9E%E4%BE%8B%E5%90%AF%E5%8A%A8.png?raw=true)

## 6. 选择刚刚您创建的 密钥对 。密钥对创建请看下面。

![密钥对](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E5%AF%86%E9%92%A5%E5%AF%B9.png?raw=true)

### 6.1 点击 密钥对，向下滚动才能找到

![创建密钥对](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E5%88%9B%E5%BB%BA%E5%AF%86%E9%92%A5%E5%AF%B9.png?raw=true)

### 6.2 输入密钥对名称，并点击创建，您的电脑将会自动下载一个.pem的文件，之后您需要使用puttygen来把它转成.ppk文件(教程略)

![密钥对名称](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E5%AF%86%E9%92%A5%E5%AF%B9%E5%90%8D%E7%A7%B0.png?raw=true)

## 7. 点击 查看实例或 i-0de...

![正在启动](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E6%AD%A3%E5%9C%A8%E5%90%AF%E5%8A%A8.png?raw=true)

## 8. 实例启动成功

![实例启动成功](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E5%AE%9E%E4%BE%8B%E5%90%AF%E5%8A%A8%E6%88%90%E5%8A%9F.png?raw=true)

## 9. 修改默认安全组的入站规则

![修改默认安全组的入站规则](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E4%BF%AE%E6%94%B9%E9%BB%98%E8%AE%A4%E5%AE%89%E5%85%A8%E7%BB%84%E7%9A%84%E5%85%A5%E7%AB%99%E8%A7%84%E5%88%99.png?raw=true)

### 9.1 编辑入站规则

![编辑入站规则](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E7%BC%96%E8%BE%91%E5%85%A5%E7%AB%99%E8%A7%84%E5%88%99.png?raw=true)

### 9.2 安全组的入站规则编辑成功

![安全组入站规则编辑成功](https://github.com/wuhanhao/Blogs/blob/master/Pictures/AWS/%E5%AE%89%E5%85%A8%E7%BB%84%E5%85%A5%E7%AB%99%E8%A7%84%E5%88%99%E7%BC%96%E8%BE%91%E6%88%90%E5%8A%9F.png?raw=true)

# 在AWS的EC2 上修改jupyter的配置文件

## 1. 登陆远程服务器

注意：使用普通用户登录，不要用root超级用户登录

## 2. 生成配置文件

```bash
jupyter notebook --generate-config
```

## 3. 生成密码

打开ipython/python，创建一个密文的密码

```bash
from notebook.auth import passwd
passwd()
Enter password: 
Verify password: 
Verify password: 
Out[2]: 'sha1:623cec53cd26:d13715cff65aa82cc0c60084c0e1a8603d8e2d43'
```

## 4. 修改默认配置文件

```
vim ~/.jupyter/jupyter_notebook_config.py 
```

进行如下修改：

```bash
c.NotebookApp.ip='*'                       # 代表所有iP都能访问，也可以指定ip
c.NotebookApp.password = u'sha1:628cc84dffd3:f253795ca0d4f0ba92b0133d6c9f6640cf61a232'      											   # 刚才复制的那个密文
c.NotebookApp.open_browser = False         # 禁止自动打开浏览器
c.NotebookApp.port =8888                   # 指定一个端口
c.NotebookApp.notebook_dir = '/home/ubuntu/jupyter'    # 指定属于自己的工作空间
c.PAMAuthenticator.encoding = 'utf8'       # 指定utf-8编码，解决读取中文路径
```

## 5. 启动jupyter notebook

```
jupyter-notebook
```

## 6. 远程访问

此时就可以直接从本地浏览器直接访问`http://服务器的IP:8888`就可以看到jupyter的登陆界面



# 在AWS的EC2 上开启root密码登录

##  1. 设置root用户密码登录

```bash
sudo passwd root
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

##  2. 修改配置文件，允许使用密码登录

```bash
vim /etc/ssh/sshd_config

# 将下面的 no 改为 yes 可使用/搜索
PasswordAuthentication no
```

### 3. 重启ssd
```
sudo /etc/init.d/ssh restart
```

