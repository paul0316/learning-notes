# Git
配置用户信息
```
git config --global user.name "your.username"
git config --global user.email "your.email"
```
这些配置可以在 .gitconfig 文件中找到

将 ssh 添加到 GitHub 账户
```
# copy ssh
pbcopy < ~/.ssh/id_rsa.pub
```
在 GitHub 账户设置中添加 ssh。



很多人在GitHub仓库看到类似 .DS_Store 等文件，可以通过设置 .gitignore 文件解决。
.gitignore 文件模板
```
# Folder view configuration files
.DS_Store
Desktop.ini

# Thumbnail cache files
._*
Thumbs.db

# Files that might appear on external disks
.Spotlight-V100
.Trashes

# Compiled Python files
*.pyc

# Compiled C++ files
*.out

# Application specific files
venv
node_modules
.sass-cache
```
这是 Mac 下的 .gitignore 文件
如果是 Windows 用户，可以访问这个网站[gitignore.io](https://www.toptal.com/developers/gitignore?templates=macos)，自定义生成 .gitignore 文件。



由于 GitHub 的服务器在国外，国内访问 GitHub 速度很慢，如果你有代理的话，可以给 git 设置代理，在终端中输入以下内容：
临时设置代理
```
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7891
```

长期设置代理
```
# socks5
git config --global http.proxy "socks5:127.0.0.1:port"
git config --global http.proxy "socks5:127.0.0.1:port"

# unset proxy
git config --global --unset http.proxy
git config --global --unset https.proxy
```


还有一种加速的方式
国内用户可以使用码云（gitee）






# GitHub









# GitLab
