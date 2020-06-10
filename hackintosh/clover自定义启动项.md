# 首先在mac下挂载efi分区
方法一：在终端中操作
```
# 查看
diskutil list

diskutil mount disk01s01
```

方法二：使用clover configuration软件
打开软件，选择挂载分区，找到efi分区，点击挂载分区即可。（这里要输入账户的密码）

# 自定义启动项
使用clover configuration软件打开/EFI/CLOVER/config.plist文件，左侧点击GUI，界面如下：

点击custom entries

然后在下方添加自定义的启动项

记得不要勾选legacy选项，不然可能会出现`Boot Windows from Lagacy HD3`类似的选项

参考：
YouTube视频：[custom entries in clover](https://www.youtube.com/watch?v=waJeLVZwXUA&t=193s)
