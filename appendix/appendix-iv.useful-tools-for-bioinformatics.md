# Appendix IV. Useful tools for bioinformatics

## Jupyter

安装方法：

```bash
pip install jupyter
```

特性：

* 基于浏览器的Python编程界面
* 支持画图，HTML可视化和运行JavaScript
* 支持Markdown, Latex公式嵌入
* 支持Python2, Python3, R, bash等多种[kernel](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels)
* 支持插件，例如导航栏
* 可导出为Python脚本、HTML等，以ipynb文件格式分享
* 可远程运行Terminal
* 安装JupyterHub之后可通过集群上的账户登录，多用户之间互不干扰

## snakemake

文档地址：[https://snakemake.readthedocs.io/en/stable/](https://snakemake.readthedocs.io/en/stable/)

安装方法：

```bash
pip install snakemake
```

特性：

* Snakefile类似Makefile。编程语言是Python语法的扩展，可充分利用Python语言
* 自动解析任务之间的依赖性，自动并行没有依赖的任务
* 通过生成文件的修改时间跳过已运行完的任务
* 中断时自动移除输出文件，避免下一步用到不完整的输入文件
* 可设置通过qsub, bsub等命令提交到集群
* 可将任务依赖关系图导出为图片

## RStudio

下载地址：[https://www.rstudio.com/products/rstudio/download/](https://www.rstudio.com/products/rstudio/download/)

特性：

* 图形化界面集成R编辑器，数据管理，画图，包管理等
* 可运行Terminal
* RStudio Server可运行在服务器上，通过浏览器访问
* 用户可通过服务器上的账户登录到RStudio Server

## rsync

rsync是Linux/Unix下最常用的同步工具，常用于备份。

最常试用的命令：

```bash
rsync -ravP ${source} ${dest}
```

注意：

* `-a`参数保留符号链接和所有文件访问权限
* `-P`实时显示传输进度
* `${dest}`和`${source}`可以是文件或目录
* `${dest}`和`${source}`可以是远程服务器上的目录（格式为`user@server:directory`\)，但不能同时是远程文件或目录。远程文件传输一般需要SSH账户。
* 源目录名后加"/": 把源目录下的所有文件和目录复制到目标目录。源目录名不加"/"：在目标目录创建新的与源目录相同的目录。
* `${source}`可指定多次，`${dest}`只能指定一次
* 如果加`--delete`参数，则目标目录下多余的文件或目录会被删除（谨慎使用！）

## Visual Studio Code

微软推出的图形编辑器。

下载地址：[https://code.visualstudio.com/](https://code.visualstudio.com/)

特性：

* 轻量级。相比于PyCharm编辑器启动更快，运行更加流畅
* 与Git, Docker深度集成（可查看文件修改状态和修改历史）
* 支持大量的插件，包括Python, R, bash, C/C++，HTML等绝大部分语言语法检查器和补全
* 自动保存和恢复工作区（打开的文件）
* 底部集成Terminal
* Remote Development \(SSH\)插件支持直接通过SSH直接编辑远程服务器上的文件
* Remote Development \(WSL\)插件支持Windows上直接编辑WSL \(Linux子系统）上的文件
* Remote Development \(Docker\)插件支持直接编辑Docker容器内的文件

## htop

终端下交互式任务管理器

下载地址：[https://hisham.hm/htop/](https://hisham.hm/htop/)

特性：

* 建议替代系统top。可同时可视化显示运行的任务信息，CPU负载，内存占用，硬盘占用等信息
* 支持鼠标点击操作，例如按CPU, 内存使用排序
* 支持进程树显示
* 可显示进程下的线程

## screen

Linux下后台任务管理，用于保持任务后台运行并实时监控任务运行状态。

CentOS下安装方法：

```bash
sudo yum install screen
```

**启动新窗口**（命名为`${task_name}`）：

```bash
screen -S ${task_name}
```

**暂时退出窗口\(detach\)**: 先同时按Ctrl-a，松开后按d键

**列出所有窗口**:

```bash
screen -ls
```

**恢复窗口\(attach\)**:

```bash
screen -r ${task_name}
```

**完全退出窗口\(kill\)**: Ctrl-d

## parallel/xargs

命令行下任务并行软件。其中parallel需要单独安装，但功能比xargs更强大。

最简单的使用方法是，把要运行的bash命令写到文件`commands.txt`里，每行一个命令，然后运行：

```bash
parallel -j 8 commands.txt
```

其中`-j`后的数字代表最大同时运行的命令数。

xargs默认会把多行输入合并为空格分隔的单行输出，如果后面加命令，则会把它们作为命令参数。

例如以下命令把ls输出的文件名作为参数传递给`wc -l`统计每个文件的行数：

```bash
ls | xargs wc -l
```

如果需要上述命令并行，可以用以下命令：

```bash
ls | xargs -L 1 -P 4 wc -l
```

其中`-L 1`代表每一行合并为一个参数传递给`wc -l`，`-P 4`参数代表4个线程并行。

## ack

比grep更强大的代码搜索工具。

下载地址：[https://beyondgrep.com/](https://beyondgrep.com/)

特性：

* 默认递归搜索（grep命令需用`fgrep -r`递归搜索）
* 可指定编程语言（例如加`--python`参数）
* 高亮显示所在文件和行

## pigz

下载地址：[https://zlib.net/pigz/](https://zlib.net/pigz/)

多线程版的gzip压缩工具，使用方式与gzip完全相同。线程数可用-p参数指定。 一般用3~4个线程可大大加速gzip的压缩和解压操作，过大没有加速效果，因为受限于硬盘读写速度。

## crontab

Linux下计划运行任务的程序。

在线crontab生成器：[https://crontab-generator.org/](https://crontab-generator.org/)

打开crontab编辑器：

```bash
crontab -e
```

加入以下crontab行：

```text
0 */6 * * * du -sh /tmp >>/tmp/du.txt 2>&1
```

将每隔6个小时运行后面的命令`du -sh /tmp`，并添加到文件`/tmp/du.txt`里

## killall

按条件批量删除任务。

例如，删除所有名为python的任务：

```bash
killall python
```

删除所有由用户`${user}`启动的任务：

```bash
killall -u ${user}
```

