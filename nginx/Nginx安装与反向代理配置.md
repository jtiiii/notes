# Nginx 安装与反向代理配置

以下操作环境为`Centos7`

## yum 安装

yum 一件指令安装

```shell
$yum install -y nginx
```

 

## nginx 启动|关闭|重启

**使用 `systemctl` 指令**

```shell
$systemctl start | stop | restart nginx
```



**使用 `nginx` 指令**

```shell
#启动
$nginx
#停止
$nginx -s stop
#重载
$nginx -s reload
```



> **直接关闭进程**
>
> ```shell
> #查找nginx服务进程
> $ps -ef | grep nginx
> #杀死进程 - [pid] 为查找到的nginx进程号
> $kill -9 [pid]
> ```
>
> 



## 配置反向代理

Nginx最重要也是最常用的一个功能就是反向代理，而且使用方法很简单，只需要配置文件就行了，nginx是通过配置来启动服务的。

nginx的配置文件默认路径为：`/etc/nginx/conf.d`

下面是示例配置：

**/etc/nginx/conf.d/example.conf**

```conf
#服务配置
server {
	#监听访问端口
	listen 80;
	#监听访问域名
	server_name  example.com;
	#根目录配置
	location / {
		#反向代理地址
		proxy_pass  http://localhost:8080/example/;
	}
}
```

上述示例配置的效果是，访问`example.com:80`地址的时候，会自动代理到`http://localhost:8080/example/`地址上。比如：`example.com:80/login` -> `http://localhost:8080/example/login`

配置完毕后重启`nginx`服务会自动生效

