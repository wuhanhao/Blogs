# 获取Ubuntu16.04的Docker CE——使用存储库安装

*预计阅读时间： 8分钟*

## 先决条件

### OS要求

要安装Docker CE，您需要这些Ubuntu版本之一的64位版本：

- 仿生18.04（LTS）
- 巧妙的17.10
- Xenial 16.04（LTS）
- Trusty 14.04（LTS）

### 卸载旧版本

较旧版本的Docker被称为`docker`或`docker-engine`。如果已安装，请卸载它们：

```bash
$ sudo apt-get remove docker docker-engine docker.io
```

如果`apt-get`报告没有安装这些软件包，则可以。

`/var/lib/docker/`保留包括图像，容器，卷和网络在内的内容。现在调用Docker CE包`docker-ce`。

### 支持的存储驱动（略）

## 安装Docker CE

您可以根据需要以不同方式安装Docker CE**（本文是使用存储库安装）**：

- 大多数用户 **设置Docker的存储库** 并从中进行安装，以便于安装和升级任务。这是推荐的方法。
- 有些用户下载DEB软件包并 **手动安装** 并完全手动管理升级。这在诸如在没有访问互联网的气隙系统上安装Docker的情况下非常有用。
- 在测试和开发环境中，一些用户选择使用自动 **便捷脚本 **来安装Docker。

### 使用存储库安装

在新主机上首次安装Docker CE之前，需要设置Docker存储库。之后，您可以从存储库安装和更新Docker。

#### 设置存储库

1. 更新`apt`包索引：

   ```bash
   sudo apt-get update
   ```

2. 安装包以允许`apt`通过HTTPS使用存储库：

   ```bash
   sudo apt-get install \
       apt-transport-https \
       ca-certificates \
       curl \
       software-properties-common
   ```

3. 添加Docker的官方GPG密钥：

   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```

   `9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88`通过搜索指纹的最后8个字符，验证您现在拥有带指纹的密钥 。

   ```bash
   sudo apt-key fingerprint 0EBFCD88
   
   终端显示的信息：
   pub   4096R/0EBFCD88 2017-02-22
         Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
   uid                  Docker Release (CE deb) <docker@docker.com>
   sub   4096R/F273FCD8 2017-02-22
   ```

4. 使用以下命令设置**稳定**存储库。即使您还想从**边缘**或**测试**存储库安装构建，您始终需要**稳定的**存储 库。要添加**边缘**或 **测试**存储库，请在下面的命令中的单词后添加单词或（或两者）。`edge test stable`

- 针对**x86_64 / amd64**（其他的略）

```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

> **注意**：从Docker 17.06开始，稳定版本也会被推送到**边缘**并**测试**存储库。

#### 安装DOCKER CE

1. 更新`apt`包索引。

   ```bash
   sudo apt-get update
   ```

2. 安装最新版本的Docker CE，或转到下一步安装特定版本：

   ```bash
   sudo apt-get install docker-ce
   ```

   > 有多个Docker存储库？
   >
   > 如果您启用了多个Docker存储库，则在未指定`apt-get install`或 `apt-get update`命令中的版本的情况下安装或更新始终会安装尽可能高的版本，这可能不适合您的稳定性需求。

3. 要安装*特定版本*的Docker CE，请列出repo中的可用版本，然后选择并安装：

   一个。列出您的仓库中可用的版本：

   ```bsh
   $ apt-cache madison docker-ce
   
   终端显示的信息：
   docker-ce | 18.03.0~ce-0~ubuntu | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
   ......
   ......
   ......
   ```

   按其完全限定的包名称安装特定版本，例如，包名称（`docker-ce`）“=”版本字符串（第2列） `docker-ce=18.03.0~ce-0~ubuntu`。

   ```bash
   sudo apt-get install docker-ce=<VERSION>
   
   例如：$ sudo apt-get install docker-ce=18.03.0~ce-0~ubuntu
   ```

   Docker守护程序自动启动。

4. 通过运行`hello-world` 映像验证是否正确安装了Docker CE 。

   ```bash
   sudo docker run hello-world
   ```

   此命令下载测试映像并在容器中运行它。当容器运行时，它会打印一条信息性消息并退出。

   ```bash
   终端显示的信息：
   
   Unable to find image 'hello-world:latest' locally
   latest: Pulling from library/hello-world
   9db2ca6ccae0: Pull complete 
   Digest: sha256:4b8ff392a12ed9ea17784bd3c9a8b1fa3299cac44aca35a85c90c5e3c7afacdc
   Status: Downloaded newer image for hello-world:latest
   
   Hello from Docker!
   This message shows that your installation appears to be working correctly.
   
   To generate this message, Docker took the following steps:
    1. The Docker client contacted the Docker daemon.
    2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
       (amd64)
    3. The Docker daemon created a new container from that image which runs the
       executable that produces the output you are currently reading.
    4. The Docker daemon streamed that output to the Docker client, which sent it
       to your terminal.
   
   To try something more ambitious, you can run an Ubuntu container with:
    $ docker run -it ubuntu bash
   
   Share images, automate workflows, and more with a free Docker ID:
    https://hub.docker.com/
   
   For more examples and ideas, visit:
    https://docs.docker.com/engine/userguide/
   ```

Docker CE已安装并正在运行。该`docker`组已创建，但未向其添加任何用户。您需要使用它`sudo`来运行Docker命令（请见下文）。

#### 升级DOCKER CE

要升级Docker CE，请先运行`sudo apt-get update`，然后按照 **以上步骤** 选择要安装的新版本。

------

## 以非root用户身份管理Docker

Docker守护程序绑定到Unix套接字而不是TCP端口。默认情况下，Unix套接字由用户拥有，`root`而其他用户只能使用它`sudo`。Docker守护程序始终以`root`用户身份运行。

如果您不想在`docker`命令前加上`sudo`，请创建一个名为的Unix组`docker`并向其添加用户。当Docker守护程序启动时，它会创建一个可由该`docker`组成员访问的Unix套接字。

**总的来说**，docker通常会使用Unix socket和Docker引擎通讯，通常只有root和docker用户组的用户才可以访问该socket，不然你就要一直sudo，所以，最好把你当前需要使用docker的用户添加到docker用户组中。

> 警告：该`docker`组授予与`root` 用户等效的权限。

要创建`docker`组并添加您的用户：

#### 创建`docker`组。

```bash
sudo groupadd docker
```

#### 将您的用户添加到该`docker`组。

```bash
sudo usermod -aG docker $USER

例如：sudo usermod -aG docker whh
```

#### 注销并重新登录，以便重新评估您的组成员身份。

如果在虚拟机上进行测试，则可能需要重新启动虚拟机才能使更改生效。

在桌面Linux环境（如X Windows）上，完全注销会话，然后重新登录。

#### **验证您是否可以运行`docker`命令`sudo`。**

```bash
docker run hello-world
```

此命令下载测试映像并在容器中运行它。当容器运行时，它会打印一条信息性消息并退出。

如果`sudo`在将用户添加到`docker`组之前最初使用Docker CLI命令，则可能会看到以下错误，表示`~/.docker/`由于`sudo`命令而创建的目录的权限不正确。

```bash
WARNING: Error loading config file: /home/user/.docker/config.json -
stat /home/user/.docker/config.json: permission denied
```

要解决此问题，请删除`~/.docker/`目录（它会自动重新创建，但任何自定义设置都将丢失），或使用以下命令更改其所有权和权限：

```bash
sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
sudo chmod g+rwx "/home/$USER/.docker" -R
```

------

## Docker命令（部分）

```bash
## List Docker CLI commands
docker
docker container --help

## Display Docker version and info
docker --version
docker version
docker info

## Execute Docker image
docker run hello-world

## List Docker images
docker image ls

## List Docker containers (running, all, all in quiet mode)
docker container ls
docker container ls --all
docker container ls -aq


docker build -t friendlyhello .  # Create image using this directory's Dockerfile
docker run -p 4000:80 friendlyhello  # Run "friendlyname" mapping port 4000 to 80
docker run -d -p 4000:80 friendlyhello         # Same thing, but in detached mode
docker container ls                                 # List all running containers
docker container ls -a              # List all containers, even those not running
docker ps -a                        # List all containers, even those not running
docker container stop <hash>            # Gracefully stop the specified container
docker container kill <hash>          # Force shutdown of the specified container
docker container rm <hash>         # Remove specified container from this machine
docker container rm $(docker container ls -a -q)          # Remove all containers
docker image ls -a                              # List all images on this machine
docker image rm <image id>             # Remove specified image from this machine
docker rm <image id>                   # Remove specified image from this machine
docker image rm $(docker image ls -a -q)    # Remove all images from this machine
docker login              # Log in this CLI session using your Docker credentials
docker tag <image> username/repository:tag   # Tag <image> for upload to registry
docker push username/repository:tag             # Upload tagged image to registry
docker run username/repository:tag                    # Run image from a registry
```