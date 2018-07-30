# Installing

关于mysql的安装，官方也有给出[安装文档](https://dev.mysql.com/downloads/mysql/)

此处则是我自己在Docker中的CentOS 7下安装Mysql8.0版本的笔记



## 配置docker容器

首先是配置docker容器,其实很简单

```shell
$docker run --privileged --name mysql -v /root/mysql:/mysql-data -p 3306:3306 centos /usr/sbin/init
```

> **option**
>
> + **`--privileged`** 解放docker容器内的root权限(没有该配置的话，容器内root用户还是部分权限被限制住)
>
> + **`--name <name>`** 定义容器别名（随意）
>
> + **`-v <host-path>:<container-path>`** 将宿主机目录挂载到容器内（相当于共享文件夹）
>
>   > 其实挂载容器的这个步骤主要是为了让容器内mysql数据持久化
>
> + **`-p <host-port>:<container-port>`** 将容器的端口映射到宿主机端口上（开放容器部分端口到外部）
>
>   > 该参数就是为了外部访问容器中的mysql服务
>
> + **`/usr/sbin/init`** 虽然一般最后CMD执行的命令都是 `/bin/bash` 进入操作命令界面，但是由于centos7特性的关系，启动容器的时候若没执行`/usr/sbin/init` 会导致常用的 `systemctl` 命令失效
>
> **顺便介绍docker其他常用命令：**
>
> + `docker exec -it <container> /bin/bash` 不知道为啥，使用`docker attach`容易假死连接不进去，还是得靠`docker exec`。
> + `docker start | stop | restart  <container>` 依次为启动，停止，重启容器



### 在线yum安装

[官网加持](https://dev.mysql.com/downloads/repo/yum/)

`yum `一键安装启动，指令一向舒适。简短的`yum install` 即可完成，非常方便。

按照你`linux`的内核版本和平台，选择合适的`yum`仓库安装文件

比如我这环境是`centos7`，则选择`mysql80-community-release-el7-1.noarch.rpm`

以下操作均在docker容器内以root用户操作:

> 下载mysql8.0的仓库文件
>
> ```shell
> $wget https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm
> ```
>
> 安装仓库文件
>
> ```shell
> $yum install -y mysql80-community-release-el7-1.noarch.rpm
> ```
>
> 查看mysql 可用yum仓库（主要用于测试仓库文件是否正常配置）
>
> ```shell
> $yum repolist all | grep mysql
> #以下是运行结果参考，如果正确显示mysql可用仓库，则说明yum仓库配置安装正常
> mysql-connectors-community/x86_64       MySQL Connectors Community          60
> mysql-tools-community/x86_64            MySQL Tools Community               69
> mysql80-community/x86_64                MySQL 8.0 Community Server          33
> ```
>
> 最后核心的一键安装步骤：
>
> ```shell
> $yum install -y mysql-community-server
> #因为yum是在线安装的，安装时间根据实际网络情况来
> ```
>
> 安装完毕后就可以启动了
>
> ```shell
> $systemctl start mysqld.service
> ```
>
> 不过第一次安装成功后，mysql会自动生成root用户临时密码
>
> 可以使用下面指令查看：
>
> ```shell
> $grep 'temporary password' /var/log/mysqld.log
> ```



## 后续配置

安装完mysql后，就是修改数据库数据文件目录了。比如移动到你挂载的目录下，也能作为数据持久化。

下面配置步骤请先关闭`mysql`服务：

```shell
$systemctl stop mysqld.service
```

> 编辑`/etc/my.cnf`文件，找到`datadir`配置，修改为你想要迁移的目录，我这里以`/mysql-data`目录为例
>
> **注意，在编辑文件前记得先备份**
>
> ```shell
> $vim /etc/my.cnf
> ~
> #datadir=/var/lib/mysql 
> #迁移目录为/mysql-data/data
> datadir=/mysql-data/data
> socket=/var/lib/mysql/mysql.sock
> 
> log-error=/var/log/mysqld.log
> pid-file=/var/run/mysqld/mysqld.pid
> ~                                      
> ```
>
> > 小知识：vim环境下，按 `I` (插入)或 `A` (追加)键进入编辑模式，按`ESC`退出编辑模式，按 `:` 键是进入指令模式，在指令模式下输入 `:wq` 回车后就是保存退出， `:q!` 则为不保存退出。
>
> 后面就是迁移目录的和保障`mysql`用户所有者权限
>
> ```shell
> #迁移目录
> $mv /var/lib/mysql /mysql-data/data
> #修改目录所有者
> $chown -R mysql:mysql /mysql-data
> $chmod 750 /mysql-data
> ```
>
> 最后重新启动mysql服务即可。
>
> ```shell
> $systemctl start mysqld.service
> ```
>
> 如果出现以下错误，多半是目录不存在，或者是权限和所属用户问题。多检查一下就好
>
> ```shell
> [ERROR] [MY-010273] [Server] Could not create unix socket lock file /var/lib/mysql/mysql.sock.lock.
> ```
>
> 

## 部分细节

+ **数据库连接插件修改**

  `mysql`8.0版本之后，连接插件和之前的`5.7`不一样，即时配置了密码，原先再使用的`navicat`，`datagrip`工具可能就无法连接。可能会出现以下错误：

  `Authentication plugin 'caching_sha2_password' cannot be loaded`

  这时候就重新修改密码加入`with mysql_native_password`内容

  E.g.

  ```mysql
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'root';
  ```

  







