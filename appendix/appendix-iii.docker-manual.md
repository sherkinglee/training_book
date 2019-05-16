# Appendix III. Docker Manual

## 下载Docker软件

从\([https://www.docker.com/get-docker](https://www.docker.com/get-docker)\) 下载操作系统对应的Community Edition的docker软件。例如Mac系统可从\([https://store.docker.com/editions/community/docker-ce-desktop-mac](https://store.docker.com/editions/community/docker-ce-desktop-mac)\) 下载，之后安装并启动docker。

之后在命令行下输入以下命令：

```bash
docker ps
```

如果无错误信息，说明docker可以正常使用。

**注意：**在Linux系统下，需要使用以下命令将用户加入到docker用户组才能使用docker：

```bash
sudo usermod -aG dockr <user>
```

其中`<user>`是自己的用户ID。

## 构建Docker镜像

新建一个名为`Dockerfile`的文件，添加以下内容：

```text
FROM ubuntu:16.04

RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak \
&& echo "deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse" > /etc/apt/sources.list \
&& echo "deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse" >> /etc/apt/sources.list \
&& echo "deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse" >> /etc/apt/sources.list \
&& echo "deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse" >> /etc/apt/sources.list \
&& echo "deb http://mirrors.tuna.tsinghua.edu.cn/CRAN/bin/linux/ubuntu xenial/" >> /etc/apt/sources.list
RUN gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9 \
&& gpg -a --export E084DAB9 | apt-key add - \
&& apt-get update \
&& apt-get install -y vim r-base r-base-dev perl python \
&& apt-get clean

WORKDIR /work
CMD ["/bin/bash"]
```

然后运行：

```bash
docker build -t lulab/bioinfo-training .
```

之后会生成一个名为`lulab/bioinfo-training`的镜像，其中`-t`选项用于指定镜像的名称。

通过`docker images`命令可查看生成镜像的信息和大小.

## 使用Docker容器

### 启动一个新的docker容器 \(交互式\)

运行以下命令将会从镜像`lulab/bioinfo-training`启动新的容器：

```bash
docker run -it lulab/bioinfo-training --name=<container name>
```

默认会在容器中运行一个`/bin/bash`程序，进入交互式命令行状态。`<container name>`是容器的名称。

bash退出后，相应的容器也自动退出。这时用`docker ps -a`状态可看到容器处于停止状态。

### 启动一个新的docker容器（后台运行\)

另一种启动docker的方式是在启动时加上`-d`参数，让容器在后台运行：

```bash
docker run -dt lulab/bioinfo-training --name=<container name>
```

这时不会进入交互式界面，但是可用`docker ps`命令看到容器处于运行状态。

### 进入已有容器（交互式）

对于交互式运行，并且已停止的容器，需要先用以下命令重新启动容器：

```bash
docker start <container name>
```

然后用以下命令重新进入交互式界面：

```bash
docker attach <container name>
```

### 进入已有容器（后台运行）

对于已经启动的容器，运行以下命令可在容器中运行新的程序（`/bin/bash`）：

```bash
docker exec -it <container name> /bin/bash
```

### 停止容器

运行：

```bash
docker stop <container name>
```

可终止容器中所有的进程，但不删除数据。此时可用`docker ps -a`命令查看停止的容器。

### 删除容器

对于已经停止的容器，运行：

```bash
docker rm <container name>
```

可删除容器的数据。此时用`docker ps -a`命令不再能查看到。

