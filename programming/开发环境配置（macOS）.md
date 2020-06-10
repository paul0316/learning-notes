# 开发环境配置（macOS）

## Homebrew

Homebrew 是 macOS 下的包管理软件。

Homebrew 官方网址：https://brew.sh/index_zh-cn

将以下命令复制到终端执行

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

## 配置 iterm2+zsh+oh-my-zsh
可以使用homebrew安装iterm2，也可以直接去官网上下载软件安装包。
```
brew search iterm2
brew install iterm2
```

切换shell为zsh
```
# 查看所有的shell
cat /etc/shells

# 查看当前的shell
echo $SHELL

# 切换shell为zsh
chsh -s $(which zsh)
```

安装oh-my-zsh
[oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh)，官方介绍了几种安装方法
通过 curl
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

通过wget
```
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

手动安装
```
curl -Lo install.sh https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh
sh install.sh
```


**注意：**因为安装 Homebrew 连接的是国外服务器，经常出现安装失败或者安装很慢的问题

我使用的是脚本安装的方法，代码参考自：https://www.mintimate.cn/2020/04/05/Homebrew/

脚本代码如下：

```
/bin/zsh -c "$(curl -fsSL http://101.133.237.130/Homebrew/HomebrewAutoInstall.sh)"
```







## JDK

JDK 是通过安装包直接安装的





## Tomcat

Tomcat 是一款服务器。我这里使用 Homebrew 安装的，如下：

```
# 查找需要安装的版本
brew search tomcat

# 我安装的是 Tomcat8
brew install tomcat@8
```



使用

```
# 查看安装地址
brew ls tomcat@8

# 查看帮助
catalina -h

# 运行服务，这种方式启动的话，关闭控制台后 Tomcat 服务器停止
catalina run

# 通过以下方式控制 Tomcat 服务器的启动和停止（推荐）
# 启动
catalina start

# 停止
catalina stop
```



使用 `homebrew service` 控制 Tomcat 的启动和停止

```
# 启动
brew service start tomcat@8
# 停止
brew service stop tomcat@8
```





## Maven

依赖管理

homebrew安装如下：

```
brew search maven

brew install maven@3.5
```



使用

```
# 查看安装信息
mvn -v

Apache Maven 3.5.4 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-18T02:33:14+08:00)
Maven home: /usr/local/Cellar/maven@3.5/3.5.4_1/libexec
Java version: 13.0.2, vendor: N/A, runtime: /usr/local/Cellar/openjdk/13.0.2+8_2/libexec/openjdk.jdk/Contents/Home
Default locale: zh_CN_#Hans, platform encoding: UTF-8
OS name: "mac os x", version: "10.14.5", arch: "x86_64", family: "mac"
```



配置 maven 的本地仓库以及镜像

`settings.xml` 配置文件在 `/usr/local/Cellar/maven@3.5/3.5.4_1/libexec/conf` 目录下。

本地仓库

![image-20200517140353487](https://tva1.sinaimg.cn/large/007S8ZIlgy1gevev01tvpj30n806e3zy.jpg)



设置阿里镜像

```xml
<mirror>
    <id>alimaven</id>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    <mirrorOf>central</mirrorOf>
</mirror>
```









## 数据库

### 关系型数据库

MySQL







Oracle





### 非关系型数据库（NoSQL）

Redis







MongoDB





## 安装Node
### 安装node版本管理（node version manager）
[nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
```
# curl方法（二者选一即可）
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash

# wget方法
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash

```

安装之后
```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm

source ./zshrc
```

### 安装node
```
command -v nvm

nvm ls-remote

nvm install v12.18.0

```
