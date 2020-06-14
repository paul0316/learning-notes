# 简介

## Docker简介





## Docker组件









# 安装Docker

## 前提条件







## Ubuntu和Debian中安装Docker







## RedHat和RedHat系发行版中安装Docker









## 在macOS中安装Docker









## 在Windows中安装Docker









## Docker安装脚本

可以从 get.docker.com 网址获取安装脚本

目前这种方式只支持在Ubuntu、Fedora、Debian和Gentoo中安装Docker。

```
curl https://get.docker.com/ | sudo sh
```







## 二进制文件安装

直接下载软件安装包

不推荐



## Docker守护进程

用户可以使用 `docker daemon` 命令来控制Docker守护进程。





## 配置Docker守护进程

可以使用-H标志指定不同的网络接口和端口配置。

```
sudo docker daemon -H tcp://0.0.0.0:2375
```







## 检查Docker守护进程是否正在运行







## 升级Docker











# Docker入门







# 使用Docker镜像和仓库









# 在测试中使用Docker











# 使用Docker构建服务











# Docker编配和服务发现









