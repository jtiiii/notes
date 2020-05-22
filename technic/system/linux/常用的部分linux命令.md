# 常用的部分linux命令

这里只展示部分常用命令，命令也只展示部分常用选项



## w 查看在线用户

`w`



## pkill 终止进程

也可以用来按照终端号踢出用户

E.g.

`pkill -t -9 pts/1`



## man 查看指令文档手册

`man [option] [name]`

E.g.

`man man`

`man ls`

`man git`

> 当要导出内容的时候，比如 `man tree > tree.txt` 时，查看内容混乱或者乱码。
>
> 解决方法: 再加入`col -b`操作
>
> E.g.  `tree man | col -b > tree.text`





## ls 展示目录文件

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



## cd 跳转/切换工作目录

`cd`

E.g.

`cd ~/Desktop`  跳转到当前用户的Desktop文件夹



## cp 复制文件

`cp [option] [sourceFile] [targetFile]`

**option**

+ `-r` 递归复制

E.g.

`cp t1.txt text/` 将当前目录的t1.txt文件复制到当前目录text文件夹内

`cp t1.txt text/t2.txt` 将当前目录的t1.txt文件复制到当前目录text文件夹内并改为t2.txt

`cp /home/me/t1.txt /usr/` 使用绝对目录，将/home/me/t1.txt文件移动到/usr/目录下



## mv 移动文件

`mv [sourceFile] [targetFile]`

E.g.

`mv t1.txt text/` 将当前目录的t1.txt文件移动到当前目录text文件夹内

`mv t1.txt text/t2.txt` 将当前目录的t1.txt文件移动到当前目录text文件夹内并改为t2.txt

`mv /home/me/t1.txt /usr/` 使用绝对目录，将/home/me/t1.txt文件移动到/usr/目录下



## mkdir 新建文件夹

`mkdir [directory]`

E.g.

`mkdir /home/myfolder` 在/home路径下创建myfolder文件夹



## col 过滤控制字符

在使用`>` 或者 `>>` 输出到内容文件时候，多余的控制字符会导致内容乱码，`col` 命令能过滤这些字符

`col [option]`

**option**

+ `-b` 过滤掉所有控制字符，包括RLF和HRLF
+ `-f` 过滤RLF字符
+ `-x` 过滤以多个空格表示跳格的字符
+ `-l<缓冲区列数>` 预设的内存缓冲区有128列，用户可以自行指定缓冲区的大小



## tar 解压缩

使用 `tar`指令可以解压缩/打包文件或者文件夹

`tar [option] <path>`

**option**

+ `-c` 创建一个`.tar`打包文件

+ `-x` 对一个`.tar`文件进行解压操作

+ `-t` 查看打包内容

+ `-z` 使用`gzip`进行解压缩

  > 若为 `-cz` 则为压缩，`-xz`则为解压，一般使用`.tar.gz`后缀

+ `-j` 使用`bzip2` 进行解压缩

  > 若为 `-cj` 则为压缩，`-xj` 则为解压，一般使用`.tar.bz2`后缀

+  `-f <filename>` 指定使用文件，若没有压缩操作，则以`.tar`为后缀

+ `-v` 详细显示正在处理的文件名

+ `-C` 指定解压目录

E.g.

```shell
#创建一个pack.tar.gz打包压缩文件，打包~/pack 目录
$tar -czvf pack.tar.gz ~/pack

#将pack.tar.gz的打包压缩文件解压到当前目录
$tar -xzvf pack.tar.gz
```



## find 查找

使用`find`命令查找文件或文件夹

`find <path> [option]`

**option**

+ `-name <text>` 按照名称匹配查找

  > E.g. `find ./ -name "config*"` 在当前目录下查找前缀名为`config`的文件

+ `-type <type>` 根据文件类型查找

  **type**

  + `f` 普通文件
  + `l` 符号链接
  + `d` 目录/文件夹
  + `b` 块设备
  + `s` 套接字
  + `p` Fifo

  > E.g. `find ./ -type d -name "member"` 在当前目录下查找名为member的目录/文件夹

+ `-size <size unit>` 根据文件大小查找

  **unit**

  + `b` 512bit
  + `c` 字节
  + `w` 2倍 c
  + `k` 1024倍 c
  + `M` 1024倍 K
  + `G` 1024倍 M

  > E.g.
  >
  > 在当前目录下例如查找文件大小为**603019898(bit)**
  >
  > ```shell
  > find ./ -size 603019898c
  > find ./ -size 301509949w
  > #-size 方法不接受小数点的，查找时会以向上方式取整
  > find ./ -size 588887k #588886.619140625
  > find ./ -size 575M #575.0845890045
  > ```

+ `-delete` 删除匹配的文件

+ `-empty` 匹配空文件