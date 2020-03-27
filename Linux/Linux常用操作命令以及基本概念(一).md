# Linux常用操作命令以及基本概念(一)

## 1. 学习 Linux 终端命令的原因

- Linux 刚面世时并没有图形界面，所有的操作全靠命令完成，如磁盘操作、文件存取、目录操作、进程管理、文件权限设定等
- 在职场中，大量的**服务器维护工作**都是在**远程**通过 **SSH 客户端**来完成的，并没有图形界面，所有的维护工作都需要通过命令来完成
- 在职场中，作为后端程序员，必须要或多或少的掌握一些 Linux 常用的终端命令
- Linux 发行版本的命令大概有 200 多个，但是常用的命令只有 10 多个而已
- 不需要死记硬背，对于常用命令，用的多了，自然就记住了

## 2. 快捷键

- Tab：命令和文件名补全
- Ctrl+C：中断正在运行的程序
- Ctrl+D：结束键盘输入（End Of File，EOF）

## 3. 常用 Linux 命令的基本使用

| 序号 | 命令            | 对应英文                | 作用                     |
| ---- | --------------- | ----------------------- | ------------------------ |
| 01   | ls              | list                    | 查看当前文件夹下的内容   |
| 02   | pwd             | print work directory    | 查看当前所在文件夹       |
| 03   | cd [目录名]     | change directory        | 切换文件夹               |
| 04   | touch [文件名]  | touch                   | 如果文件不存在，新建文件 |
| 05   | mkdir [目录名]  | make directory          | 创建目录                 |
| 06   | rm [文件名]     | remove                  | 删除指定的文件名         |
| 07   | clear           | clear                   | 清屏                     |
| 08   | cp              | copy                    | 拷贝文件                 |
| 09   | mv              | move                    | 移动文件/修改文件名      |
| 10   | cat、more、grep | concatenate、more、more | 查看文件内容             |

> 小技巧
>
> - `ctrl + shift + =` **放大**终端窗口的字体显示
> - `ctrl + -` **缩小**终端窗口的字体显示

## 4. 求助

### --help

显示指令的基本用法与选项介绍。

### man

man是manual的缩写，是将指令的具体信息显示出来，是Linux提供的一个**手册**，包含了绝大部分的命令、函数的详细使用说明。

当执行`man date`时，有 DATE(1) 出现，其中的数字代表指令的类型，常用的数字及其类型如下：

| 代号 | 类型                                            |
| ---- | ----------------------------------------------- |
| 1    | 用户在 shell 环境中可以操作的指令或者可执行文件 |
| 5    | 配置文件                                        |
| 8    | 系统管理员可以使用的管理指令                    |

使用 `man` 时的操作键：

| 操作键   | 功能                 |
| -------- | -------------------- |
| 空格键   | 显示手册页的下一屏   |
| Enter 键 | 一次滚动手册页的一行 |
| b        | 回滚一屏             |
| f        | 前滚一屏             |
| q        | 退出                 |
| /word    | 搜索 **word** 字符串 |

### info

info 与 man 类似，但是 info 将文档分成一个个页面，每个页面可以进行跳转。

### doc

/usr/share/doc 存放着软件的一整套说明文件。

## 5. 关机

### who

在关机前需要先使用 who 命令查看有没有其它用户在线。

### sync

为了加快对磁盘文件的读写速度，位于内存中的文件数据不会立即同步到磁盘上，因此关机之前需要先进行 sync 同步操作。

### shutdown

> \# shutdown [-krhc] 时间 [信息]
> -k ： 不会关机，只是发送警告信息，通知所有在线的用户
> -r ： 将系统的服务停掉后就重新启动
> -h ： 将系统的服务停掉后就立即关机
> -c ： 取消已经在进行的 shutdown 指令内容

### PATH

可以在环境变量 PATH 中声明可执行文件的路径，路径之间用 : 分隔。

```bash
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/dmtsai/.local/bin:/home/dmtsai/bin
```

### sudo

sudo 允许一般用户使用 root 可执行的命令，不过只有在 /etc/sudoers 配置文件中添加的用户才能使用该指令。

## 6. 软件包管理工具

RPM 和 DPKG 为最常见的两类软件包管理工具：

- RPM 全称为 Redhat Package Manager，最早由 Red Hat 公司制定实施，随后被 GNU 开源操作系统接受并成为很多 Linux 系统 (RHEL) 的既定软件标准。
- 与 RPM 进行竞争的是基于 Debian 操作系统 (Ubuntu) 的 DEB 软件包管理工具 DPKG，全称为 Debian Package，功能方面与 RPM 相似。

YUM 基于 RPM，具有依赖管理功能，并具有软件升级的功能。

发行版：Linux 发行版是 Linux 内核及各种应用软件的集成版本。

| 基于的包管理工具 | 商业发行版 | 社区发行版      |
| ---------------- | ---------- | --------------- |
| RPM              | Red Hat    | Fedora / CentOS |
| DPKG             | Ubuntu     | Debian          |

### DEB 包的安装 / 升级 / 查询 / 卸载 

一个 DEB 包包含了已压缩的软件文件集以及该软件的内容信息（在头文件中保存），通常表现为以 .deb 扩展名结尾的文件，例如 package.deb 。对其操作，需要使用 dpkg 命令。下面介绍 dpkg 工具的参数和使用方法。

### DPKG 命令常用参数

DPKG 的常规使用方法为 dpkg -? Package(.rpm), 其中 -? 为安装参数 ( 更多信息，请查阅帮助 $man rpm)：

- -l 在系统中查询软件内容信息
- --info 在系统中查询软件或查询指定 rpm 包的内容信息
- -i 在系统中安装 / 升级软件
- -r 在系统中卸载软件 , 不删除配置文件
- -P 在系统中卸载软件以及其配置文件

### DPKG 命令参数使用方法

安装 DEB 包命令

```bash
sudo dpkg -i package.deb
```

升级 DEB 包命令

```bash
# 和安装命令相同
sudo dpkg -i package.deb
```

```bash
# 不卸载配置文件
sudo dpkg -r package.deb 

# 卸载配置文件
sudo dpkg -P package.deb 
```

查询 DEB 包中包含的文件列表命令

```bash
sudo dpkg-deb -c package.deb
```

查询 DEB 包中包含的内容信息命令

```bash
dpkg --info package.deb
```

查询系统中所有已安装 DEB 包

```bash
dpkg -l package
```

### RPM 包的安装 / 升级 / 查询 / 卸载

一个 RPM 包包含了已压缩的软件文件集以及该软件的内容信息（在头文件中保存），通常表现为以 .rpm 扩展名结尾的文件，例如 package.rpm 。对其操作，需要使用 rpm 命令。下面介绍 rpm 工具的参数和使用方法。

### RPM 命令常用参数

RPM 的常规使用方法为 rpm -? package.rpm，其中 -? 为操作参数 ( 更多信息，请查阅帮助 $man rpm)：

- -q 在系统中查询软件或查询指定 rpm 包的内容信息
- -i 在系统中安装软件
- -U 在系统中升级软件
- -e 在系统中卸载软件
- -h 用 #(hash) 符显示 rpm 安装过程
- -v 详述安装过程
- -p 表明对 RPM 包进行查询，通常和其它参数同时使用，如：
- -qlp 查询某个 RPM 包中的所有文件列表
- -qip 查询某个 RPM 包的内容信息

### RPM 命令参数使用方法

以上参数有些需要组合使用，比如说 rpm -h package.rpm 是没有意义的，但 rpm -ih package.rpm 即表示安装 package 并用 # 符显示安装进度。

安装 RPM 包

```bash
rpm -ivh package.rpm
```

 升级 RPM 包命令

```
rpm -ev package
```

查询 RPM 包中包含的文件列表命令 

```
rpm -qlp package
```

查询 RPM 包中包含的文件列表命令

```bash
rpm -qlp package
```

查询 RPM 包中包含的内容信息命令

```bash
rpm -qip package
```

查询系统中所有已安装 RPM 包

```
rpm -qa
```

##  7. VIM 三个模式

- 一般指令模式（Command mode）：VIM 的默认模式，可以用于移动游标查看内容；
- 编辑模式（Insert mode）：按下 "i" 等按键之后进入，可以对文本进行编辑；
- 指令列模式（Bottom-line mode）：按下 ":" 按键之后进入，用于保存退出等操作。

注意：按下 esc 退出编辑模式

在指令列模式下，有以下命令用于离开或者保存文件。

| 命令 | 作用                                                         |
| ---- | ------------------------------------------------------------ |
| :w   | 写入磁盘                                                     |
| :w!  | 当文件为只读时，强制写入磁盘。到底能不能写入，与用户对该文件的权限有关 |
| :q   | 离开                                                         |
| :q!  | 强制离开不保存                                               |
| :wq  | 写入磁盘后离开                                               |
| :wq! | 强制写入磁盘后离开                                           |

## 8. 查看磁盘空间及目录容量

Df命令是linux系统以磁盘分区为单位查看文件系统，可以加上参数查看磁盘剩余空间：

```bash
df -hl
```

下面是相关命令的解释：

```bash
df -hl              # 查看磁盘剩余空间
df -h               # 查看每个根路径的分区大小
du -sh [目录名]      # 返回该目录的大小
du -sm [文件夹]      # 返回该文件夹总M数

# 更多功能可以输入一下命令查看：
df –help
du –help

sudo fdisk -l              # 查看硬盘的分区
sudo hdparm -i /dev/hda    # 查看IDE硬盘信息

# 查看STAT硬盘信息
sudo hdparm -I /dev/sda 或 
sudo apt-get install blktool 或
sudo blktool /dev/sda id

df -h              # 查看硬盘剩余空间 
du -hs 目录名       # 查看目录占用空间 
```