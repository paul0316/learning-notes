# 极客时间-玩转Git三件套

配置user信息
```
git config --global user.name "paul0316"
git config --global user.email "daaicp3@163.com"
```

config的三个作用域
缺省等于local
```
git config --local # 只对某个仓库有效
git config --global # 对当前用户所有仓库有效
git config --system # 对系统所有登录用户有效
```

显示config的配置，加上--list
```
git config --list --local # 只对某个仓库有效
git config --list --global # 对当前用户所有仓库有效
git config --list --system # 对系统所有登录用户有效
```

观看完第三个视频







## 创建第一个仓库并配置local用户信息

把已有的项目代码纳入Git仓库

```
cd 项目代码所在的文件夹
git init
```



新建一个项目直接用Git管理

```
cd 某个文件夹
git init your_project # 会在当前路径下创建和项目名同名的文件夹
cd your_project
```



配置仓库的local用户信息

```
cd your_project
git config --local user.name "username"
git config --local user.emial "email"
git config --local --list

cp ../0-material/readme .
git add readme
git status
git commit -m "Add readme"
```



