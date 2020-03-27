# Ubuntu16.04下通过Docker CE搭建Tensorflow环境

## **安装Docker CE——请查参考：**

<https://github.com/wuhanhao/Blogs/blob/master/AliCloud/%E8%8E%B7%E5%8F%96Ubuntu16.04%E7%9A%84Docker%20CE%E2%80%94%E2%80%94%E4%BD%BF%E7%94%A8%E5%AD%98%E5%82%A8%E5%BA%93%E5%AE%89%E8%A3%85.md>

## 下载TensorFlow images（镜像）

```bash
docker pull daocloud.io/daocloud/tensorflow:latest 

docker pull tensorflow/tensorflow:latest

注意：上面两条命令本质上没什么区别，第一条只是使用hub.docker.com的镜像，第二条使用默认镜像。
使用daocloud 的镜像，在国内用速度还是挺快的，如果docker.io的镜像慢，可以用daocloud的。
这个速度非常的快。一样用的。版本也挺新的。
```

过程可能有点久，具体看网速状况。

下载完毕后显示：

> ```bash
> Status: Downloaded newer image for tensorflow/tensorflow:latest
> ```

## 创建Tensorflow容器

```bash
docker run -it --rm --name myts -v ~/docker/tensorflow/notebooks:/notebooks -p 8888:8888 daocloud.io/daocloud/tensorflow:latest

docker run --rm --name my-tensorflow -it -p 8888:8888 -v ~/DockerCE/tensorflow/notebooks:/notebooks tensorflow/tensorflow

注意：上面两条命令本质上没什么区别，第一条只是使用hub.docker.com的镜像，第二条使用默认镜像。
使用daocloud 的镜像，在国内用速度还是挺快的，如果docker.io的镜像慢，可以用daocloud的。 
这个速度非常的快。一样用的。版本也挺新的。

--rm：在停止的时候删除镜像
--name：创建的容器名，即my-tensorflow
-it：保留命令行运行
-p 8888:8888：将本地的8888端口和http://localhost:8888/映射
-v ~/docker/tensorflow/notebooks:/notebooks：将本地的~/tensorflow挂载到容器内的/notebooks:/notebooks下
tensorflow/tensorflow ：默认是tensorflow/tensorflow:latest,指定使用的镜像

# 启动仅CPU容器
docker run -it -p 8888:8888 tensorflow/tensorflow
```

启动的时候并不是daemon 模式的，而是前台模式，同时显示了运行的日志。

```
root@whh:~/Desktop# docker run -it --rm --name myts -v ~/docker/tensorflow/notebooks:/notebooks -p 8888:8888 daocloud.io/daocloud/tensorflow:latest
[I 14:32:39.353 NotebookApp] Writing notebook server cookie secret to /root/.local/share/jupyter/runtime/notebook_cookie_secret
[W 14:32:39.366 NotebookApp] WARNING: The notebook server is listening on all IP addresses and not using encryption. This is not recommended.
[I 14:32:39.372 NotebookApp] Serving notebooks from local directory: /notebooks
[I 14:32:39.372 NotebookApp] The Jupyter Notebook is running at:
[I 14:32:39.372 NotebookApp] http://(71073396ed38 or 127.0.0.1):8888/?token=3f341534408d03ad9d0a2e317df58dd18eda2bc657453789
[I 14:32:39.372 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 14:32:39.373 NotebookApp] 
    
    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://(71073396ed38 or 127.0.0.1):8888/?token=3f341534408d03ad9d0a2e317df58dd18eda2bc657453789
```

> 注意：把http://(71073396ed38 or 127.0.0.1):8888/?token=3f341534408d03ad9d0a2e317df58dd18eda2bc657453789 改为http://**本机的IP地址**:8888/?token=3f341534408d03ad9d0a2e317df58dd18eda2bc657453789

之后复制上面的网址到浏览器上，就可以显示Jupyter Notebook，Jupyter Notebook（此前被称为 IPython notebook）是一个交互式笔记本。