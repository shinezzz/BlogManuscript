# Docker

## 概念

`https://docs.docker.com/install` 安装 docker

但是原本的docker不支持GPU加速，所以需要安装Nvidia-docker，`https://github.com/NVIDIA/nvidia-docker`找到相应文档来安装。

## Docker 常用操作

`image`，镜像是一个配置好的环境。

`container`， 容器，是image的具体实例。

创建容器：docker run [-it] some-image

列出运行的容器：docker ps

列出所有容器：docker ps -a

删除容器：docker rm container-id

启动：docker start [-i] container-id(-i 进入交互模式)

## 在openSUSE上安装

参考链接[https://en.opensuse.org/Docker](https://en.opensuse.org/Docker)

To install the docker and docker-compose packages:
```bash
zypper install docker python3-docker-compose
```
To start the docker daemon during boot:
```bash
sudo systemctl enable docker
```
To join the docker group that is allowed to use the docker daemon:
```bash
sudo usermod -G docker -a $USER
```
Restart the docker daemon:
```bash
sudo systemctl restart docker
```
Verify docker is running:
```bash
docker version
```
This will pull down and run the, "Hello World" docker container from dockerhub:
```bash
docker run --rm hello-world
```
Clean up and remove docker image we pulled down:

```bash
docker images
docker rmi -f IMAGE_ID
```