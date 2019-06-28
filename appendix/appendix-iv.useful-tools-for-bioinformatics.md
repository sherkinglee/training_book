# Useful tools for bioinformatics

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

文档地址：https://snakemake.readthedocs.io/en/stable/

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

下载地址：https://www.rstudio.com/products/rstudio/download/

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
* `${dest}`和`${source}`可以是远程服务器上的目录（格式为`user@server:directory`)，但不能同时是远程文件或目录。远程文件传输一般需要SSH账户。
* 源目录名后加"/": 把源目录下的所有文件和目录复制到目标目录。源目录名不加"/"：在目标目录创建新的与源目录相同的目录。
* `${source}`可指定多次，`${dest}`只能指定一次
* 如果加`--delete`参数，则目标目录下多余的文件或目录会被删除（谨慎使用！）

## Visual Studio Code

## htop

## screen

## singularity

## udocker

## parallel/xargs

## ack

## pigz


## crontab

## killall
