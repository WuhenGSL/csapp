## 使用 docker 容器部署 linux

```shell
brew install docker --cask
```

## 下载csapp实验代码

```shell
wget csapp.cs.cmu.edu/3e/XXXX
tar -xvf xxxx
```



## 环境搭建

### 拉取 CentOS

```shell
docker pull centos
```

### 创建容器

```shell
docker run --cap-add=SYS_PTRACE --security-opt seccomp=unconfined -it --platform linux/amd64 -v "$PWD:/csapp" --name=csapp centos /bin/bash
```

### 安装工具链和库

创建容器后会直接进入 linux 镜像，此时在 linux shell 中进行操作

```shell
cd /etc/yum.repos.d/
sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
yum update -y
yum install sudo
yum install make automake gcc gdb kernel-devel
yum install glibc-devel.i686
yum install vim wget
```

## 启动和关闭

### 启动

```shell
docker ps -a #查看 container ID
```

```shell
docker start containerID
docker exec -it containerID
```

### 关闭

```shell
exit #linux shell
```




