# 随手笔记——配置Android-Studio的adb环境变量

*阅读时间大约2分钟*

**第一步，打开环境变量配置窗口**。右击我的电脑，属性-高级系统设置-环境变量。

**第二步，添加android系统环境变量**。在系统变量下点击新建按钮，输入环境变量名android（自己的习惯命名），将android开发工具的路径导入。

**第三步，在path中添加刚刚添加的环境**。选择系统变量中Path，点击编辑按钮，输入刚刚建好的环境，记住要加两个百分号。

**第四步，测试环境变量。重新**打开运行命令，直接按住win+R快捷键，打开运行。

**最后一步，在运行中输入cmd，调用命令操作窗口。进入后输入adb查看运行结果。**