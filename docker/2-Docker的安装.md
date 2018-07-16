# docker 安装

Docker安装很简单，按照官方的指定的系统的版本直接下载安装即可

centos下安装直接使用yum命令即可

```shell
#yum install -y docker
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
  > 

