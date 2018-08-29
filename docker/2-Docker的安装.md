# docker 安装

Docker安装很简单，按照官方的指定的系统的版本直接下载安装即可



## Centos7

centos下安装直接使用yum命令即可

```shell
$yum install -y docker
```



# docker 服务启动与关闭

+ Centos7 

  > 使用`systemctl`命令
  >
  > ```bash
  > #启动
  > $systemctl start docker.service
  > 
  > #关闭
  > $systemctl stop docker.service
  > 
  > #重启
  > $systemctl restart docker.service
  > ```
  >



# docker 与宿主机的访问

MacOS系统下，Docker与Mac之间多了一层虚拟机，虚拟机成了Docker容器的宿主机，因此无法直接访问mac,所以官方给出的是`host.docker.internal` 该host作为访问mac的地址

[官方文档](https://docs.docker.com/docker-for-mac/networking/)

