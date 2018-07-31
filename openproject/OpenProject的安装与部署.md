# OpenProject的安装与部署

OpenProject是一个开源的免费的项目管理系统，因此适合小型异地团队合作项目使用。

[官网](https://www.openproject.org/)



## 使用 docker 安装和部署

[官网教程](https://www.openproject.org/docker/)

docker 部署很简单，认准 `openproject/community` 镜像即可，该文编写时的镜像版本为：`openproject/community:7`

**快速部署启动：**

```shell
$docker run -d -p 8080:80 --name OpenProject -e SECRET_KEY_BASE=secret openproject/community:7
```

> + `-d` 运行挂起
>
> + `--name OpenProject` 容器命名 (可选)
>
> + `-p 8080:80` 将宿主机8080端口映射到容器80端口 **(必须)**
>
>   > openproject 是web服务，必须把容器的80端口暴露出来才能供外部访问，当然选用端口随意
>
> + `-e SECRET_KEY_BASE=secret` 设置容器内环境变量 **(必须)**
>
> 假如，我宿主机的`ip`为`172.21.1.11`，则按照上述配置部署启动后，OpenProject的访问地址为:`http://172.21.1.11:8080`

部署启动后，过段时间等 `OpenProject` 启动后就能通过浏览器访问了。



**其他配置**

如果说OpenProject的数据非常重要的话，那么配置挂载持久化目录，或者改变所使用的数据库服务也可以。

+ 挂载持久化目录

  `docker` 的 `openproject/community:7` 镜像中`OpenProject`的默认数据位置为：

  + `/var/lib/postgresql/9.6/main` **Postgresql** 数据目录
  + `/var/log/supervisor` 日志目录
  + `/var/db/openproject` 静态文件目录（比如用户配置的头像，上传的文件等）

  然后我建议专门使用一个 `openproject` 目录来存放这些贵重资料。

  下面拿 `/var/lib/openproject` 目录为示例:

  ```shell
  #创建目录
  $sudo mkdir -p /var/lib/openproject/{pgdata,logs,static}
  #-v 挂载目录
  $docker run -d -p 8080:80 --name openproject -e SECRET_KEY_BASE=secret \
    -v /var/lib/openproject/pgdata:/var/lib/postgresql/9.6/main \
    -v /var/lib/openproject/logs:/var/log/supervisor \
    -v /var/lib/openproject/static:/var/db/openproject \
    openproject/community:7
  ```

+ 修改使用的数据库

   `OpenProject` 默认采用了 `postgresql` 自建数据库外，同样也可以切换为 `mysql` 数据库，就是修改环境变量: `DATABASE_URL` ,格式为`mysql2://user:password@server:port/database` 

  ```shell
  $docker run -d -p 8080:80 -e SECRET_KEY_BASE=secret \
    -e DATABASE_URL=mysql2://user:password@server:port/dbname \
    openproject/community:7
  
  # postgresql 则是这个格式：
  # -e DATABASE_URL="postgres://user:password@host:5432/dbname?pool=10&encoding=unicode&timeout=5000&reconnect=true" \
  ```

  > PS: 不过我个人 Mysql8.0 配置倒是失败了，可能是数据库太新的缘故吧...

## OpenProject 部分配置

+ 第一次安装初始化的 `OpenProject` 的 **管理员** 的用户名和密码均为 `admin` 

+ 如果界面是英文，修改语言步骤：登陆后右上角用户头像 -> MyAccount -> Settings -> Language -> 简体中文

+ 推荐配置SMTP邮件服务（有一个能用的邮箱就行）。邮件推送服务是用来推送注册用户的邮箱验证连接，推送用户的项目信息使用的，是一个非常便利的功能。

  **市面上各类的邮箱服务提供商的配置均有不同，请查阅各类邮箱的SMTP配置说明。**

  下面以QQ邮箱(`123456678@qq.com`)为例：

  > 页面(Page): 管理员账户(admin) -> 右上角用户头像 -> (Administration) -> 系统设置 (System settings) ->  电子邮件通知 (Email Notifications) 
  >
  > + 发出的电子邮件地址 | Emission email address: `123456678@qq.com`
  >
  > + **配置您的电子邮件提供商** | **CONFIGURE YOUR EMAIL PROVIDER**
  >
  >   + 电子邮件发送方法 | Email delivery method: `smtp`
  >
  >   + SMTP 服务器 | SMTP server: `smtp.qq.com`
  >
  >   + SMTP 端口 | SMTP port: `587`
  >
  >   + SMTP HELLO 域 | SMTP HELLO domain:  ` `
  >
  >     > QQ邮箱可以不填，有的邮箱有可以填
  >
  >   + SMTP 身份验证 | SMTP authentication: `login`
  >
  >   + SMTP 用户名 | SMTP username: `123456678@qq.com`
  >
  >   + SMTP 密码 | SMTP password: `***********`
  >
  >     > 注意，这里SMTP 密码需要QQ邮箱配置页面里去手动开启第三方 `SMTP` 服务，然后获取**授权码**。最后得到的 **[授权码]** 才是 `SMTP password` 要填入的部分。
  >     >
  >     > ![](images/img1.png)
  >     >
  >     > ![](images/img2.png)
  >
  >   + Automatically use STARTTLS if available 
  >
  >     + [x] 如果可用，自动使用 STARTTLS

  



