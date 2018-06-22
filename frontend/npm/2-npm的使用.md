# npm的使用

一般安装node会自带相应的npm版本。

但是npm版本更新比node快的多，最好经常执行更新操作来更新npm

##1. 安装 npm 和 node

直接去[node官网下载地址](https://nodejs.org/en/download/)下载对应系统的node安装包安装即可。

安装完毕后查看版本号来确认是否安装成功

示例:

```shell
#查看Node版本
$node -v
v8.9.4

#查看npm版本
$npm -v
5.6.0
```

## 2. 更新 npm 和 node

```shell
#更新npm
$npm install npm@latest -g 

#更新node
$npm install -g n 
$n latest
```



## 3. 查找 package

没有CLI的的时候可以通过[Website](https://www.npmjs.com/)去查询

有CLI的时候，可以使用下面命令：

```shell
$npm search [package-name]
```



## 4.查看安装的模块

```shell
$npm list [options]
```

**Options**

+ `-depth` 查看深度，比如`-depth=0` 表示只查看外面一级模块
+ `-global`查看安装的全局模块



## 5.初始化项目

```shell
$npm init [options]
```

**Options**

+ `-y` 快速默认初始化



