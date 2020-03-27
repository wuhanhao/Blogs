## **解决在云服务器（操作系统：Ubuntu16.04）使用Anaconda启动jupyter-notebook可能出现的错误问题**

本人试过网上的其他办法，说是要创建配置文件，修改配置文件，但都不能解决。

以下是本人的解决办法：在云服务器（操作系统：Ubuntu16.04）使用Anaconda启动jupyter-notebook可能出现的错误提示：

> ```bash
> whh@ubuntu:~$ jupyter-notebook 
> [I 10:01:02.312 NotebookApp] Writing notebook server cookie secret to /run/user/1000/jupyter/notebook_cookie_secret
> Traceback (most recent call last):
>   File "/home/whh/anaconda3/bin/jupyter-notebook", line 11, in <module>
>     sys.exit(main())
>   File "/home/whh/anaconda3/lib/python3.6/site-packages/jupyter_core/application.py", line 266, in launch_instance
>     return super(JupyterApp, cls).launch_instance(argv=argv, **kwargs)
>   File "/home/whh/anaconda3/lib/python3.6/site-packages/traitlets/config/application.py", line 657, in launch_instance
>     app.initialize(argv)
>   File "<decorator-gen-7>", line 2, in initialize
>   File "/home/whh/anaconda3/lib/python3.6/site-packages/traitlets/config/application.py", line 87, in catch_config_error
>     return method(app, *args, **kwargs)
>   File "/home/whh/anaconda3/lib/python3.6/site-packages/notebook/notebookapp.py", line 1537, in initialize
>     self.init_webapp()
>   File "/home/whh/anaconda3/lib/python3.6/site-packages/notebook/notebookapp.py", line 1321, in init_webapp
>     self.http_server.listen(port, self.ip)
>   File "/home/whh/anaconda3/lib/python3.6/site-packages/tornado/tcpserver.py", line 144, in listen
>     sockets = bind_sockets(port, address=address)
>   File "/home/whh/anaconda3/lib/python3.6/site-packages/tornado/netutil.py", line 163, in bind_sockets
>     sock.bind(sockaddr)
> OSError: [Errno 99] Cannot assign requested address
> ```

**解决办法：jupyter-notebook --ip=0.0.0.0或者 jupyter notebook --ip=0.0.0.0或者jupyter-notebook --ip=0.0.0.0 --port=8080或者jupyter notebook --ip=0.0.0.0 -port=8080**

运行以上任一条命令之后，会出现如下信息：

```
whh@ubuntu:~$ jupyter-notebook --ip=0.0.0.0
[I 10:11:22.258 NotebookApp] JupyterLab beta preview extension loaded from /home/whh/anaconda3/lib/python3.6/site-packages/jupyterlab
[I 10:11:22.259 NotebookApp] JupyterLab application directory is /home/whh/anaconda3/share/jupyter/lab
[I 10:11:22.263 NotebookApp] Serving notebooks from local directory: /home/whh
[I 10:11:22.263 NotebookApp] 0 active kernels
[I 10:11:22.263 NotebookApp] The Jupyter Notebook is running at:
[I 10:11:22.263 NotebookApp] http://ubuntu:8888/?token=ef90e60c9dc2900f79fb68cbdad87dab2482c83c055fc649
[I 10:11:22.263 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[W 10:11:22.264 NotebookApp] No web browser found: could not locate runnable browser.
[C 10:11:22.264 NotebookApp] 
    
    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://ubuntu:8888/?token=ef90e60c9dc2900f79fb68cbdad87dab2482c83c055fc649&token=ef90e60c9dc2900f79fb68cbdad87dab2482c83c055fc649
```

大功告成，能正常启动，之后只要把

```bash
http://ubuntu:8888/?token=ef90e60c9dc2900f79fb68cbdad87dab2482c83c055fc649&token=ef90e60c9dc2900f79fb68cbdad87dab2482c83c055fc649
```

改为云服务器的IP地址即可：

```bash
http://云服务器IP:8888/?token=ef90e60c9dc2900f79fb68cbdad87dab2482c83c055fc649&token=ef90e60c9dc2900f79fb68cbdad87dab2482c83c055fc649
```

