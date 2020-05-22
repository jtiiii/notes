# npm的使用

一般安装node会自带相应的npm版本。

但是npm版本更新比node快的多，最好经常执行更新操作来更新npm

## 安装和更新

### 安装

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

### 更新

```shell
#更新npm
$npm install npm@latest -g 

#更新node
$npm install -g n 
$n latest
```



## package - 模块/项目

### 在线查找

没有CLI的的时候可以通过[Website](https://www.npmjs.com/)去查询

有CLI的时候，可以使用下面命令：

```shell
$npm search <package-name>
```



### 安装模块

```shell
$npm install [option] <package>
```

**option**

- `-g` 是否全局安装

  > npm 全局默认安装位置：
  >
  > + MacOS: `/usr/local/lib/node_modules `
  > + Windows: `C:\Users\{root}\AppData\Roaming\npm\node_modules`
  >
  > 实在找不到全局安装位置在哪的
  >
  > 也可以使用指令`npm config ls`，来查看里面的`; cwd`目录
  >
  > E.g.
  >
  > ```shell
  > $npm config ls      
  > ; cli configs
  > metrics-registry = "https://registry.npmjs.org/"
  > scope = ""
  > user-agent = "npm/6.1.0 node/v10.4.1 darwin x64"
  > 
  > ; node bin location = /usr/local/bin/node
  > ## cwd 目录就是全局安装模块
  > ; cwd = /usr/local/lib/node_modules
  > ; HOME = /Users/peizangpin
  > ; "npm config ls -l" to show all defaults.
  > ```
  >
  > 
  >
  > 



### 卸载模块

```shell
$npm uninstall [option] <package>
```

**option**

- `-g` 是否卸载全局模块



### 查看安装的模块

```shell
$npm list [options]
```

**Options**

- `-depth` 查看深度，比如`-depth=0` 表示只查看外面一级模块
- `-global`查看安装的全局模块



### 查看项目/模块信息

```shell
$npm info <package>
```



### 更新模块

```shell
$npm update [option]
```

**option**

- `-g` 全局模块

1. 先到远程仓库查询最新版本
2. 然后对比本地版本，如果本地版本不存在，或者远程版本较新
3. 查看 `package.json` 中对应的语义版本规则
4. 如果当前新版本符合语义规则，就更新，否则不更新



### 创建/初始化模块

```shell
$npm init [options]
```

**Options**

+ `-y` 快速默认初始化



### 查看依赖更新

```shell
$npm outdated [option]
```

**option**

+ `-g` 全局模块
+ `--depth=?` 查看依赖深度

E.g.

```shell
$npm outdated
Package  Current  Wanted  Latest  Location
webpack   4.12.0  4.12.1  4.12.1  vue-component
```



### 打开项目/模块主页

```shell
$npm home
```

如果该包再`package.json`中配置了`homepage`选项的话，该指令会打开homepage中的页面



### 运行项目脚本

```shell
$npm run <script>
```

`run`用于运行`package.json`中`scripts`属性的指令

E.g.

package.json:

```json
{
    "scripts": {
        "build": "webpack"
    }
}
```

则输入`npm run build`的时候会执行`webpack`脚本



### 优化

```shell
$npm prune
```

该命令可以查看已经安装在`node_modules`却在`package.json`中未被引用的模块



## npmjs.com - npm模块库

> 用户注册得去npmjs.com网站上注册



### 添加用户[npmjs.com]

```shell
$npm adduser
```

添加一个npmjs.com上的用户，可用于发布



### 登陆[npmjs.com]

```shell
$npm login
```

登录到npmjs



### 发布[npmjs.com]

```shell
$npm publish [option]
```

将该包发布到npmjs.com供别人下载使用

**option**

+ `--tag` 指定发布标签，默认为`latest`,若要指定为测试版，则`--tag beta`



## config - 配置



### 查看配置

```shell
$npm config ls [option]
```

**option**

+ `-l` 查看所有默认(default)配置



### 查看某个配置

```shell
$npm config get [property-name]
```

E.g.

查询npm配置文件路径

```shell
$npm config get userconfig
/Users/peizangpin/.npmrc
```



### 设置某个配置

```shell
$npm config set [property-name] [value]
```

