# 常用的部分linux命令

这里只展示部分常用命令，命令也只展示部分常用选项



##man 查看指令文档手册

`man [option] [name]`

E.g.

`man man`

`man ls`

`man git`





##ls 展示目录文件

`ls [option] [path]`

**option**

+ `-a` 显示隐藏文件
+ `-l` 显示详细信息

E.g.

`ls -l`

`ls -la /usr/local`



## pwd 查看当前工作目录

`pwd [option]`

**option**

+ `-L` 显示当前逻辑工作目录
+ `-P` 显示当前物理工作目录



##cd 跳转/切换工作目录

`cd`

E.g.

`cd ~/Desktop`  跳转到当前用户的Desktop文件夹



##cp 复制文件

`cp [sourceFile] [targetFile]`

E.g.

`cp t1.txt text/` 将当前目录的t1.txt文件复制到当前目录text文件夹内

`cp t1.txt text/t2.txt` 将当前目录的t1.txt文件复制到当前目录text文件夹内并改为t2.txt

`cp /home/me/t1.txt /usr/` 使用绝对目录，将/home/me/t1.txt文件移动到/usr/目录下



##mv 移动文件

`mv [sourceFile] [targetFile]`

E.g.

`mv t1.txt text/` 将当前目录的t1.txt文件移动到当前目录text文件夹内

`mv t1.txt text/t2.txt` 将当前目录的t1.txt文件移动到当前目录text文件夹内并改为t2.txt

`mv /home/me/t1.txt /usr/` 使用绝对目录，将/home/me/t1.txt文件移动到/usr/目录下



## mkdir 新建文件夹

`mkdir [directory]`

E.g.

`mkdir /home/myfolder` 在/home路径下创建myfolder文件夹

