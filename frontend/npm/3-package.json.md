# 3-package.json

npm是通过package.json来定义项目的。

以`hello-world`项目为例

```bash
#创建hello-world文件夹
$mkdir hello-world

$cd hello-world
~/hello-world

#npm快速初始化项目
$npm init -y

Wrote to ~/hello-world/package.json:

{
  "name": "hello-world",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}


```

上述npm创建初始化后，会有一个package.json文件。文件基础内容就是：

```json
{
  "name": "hello-world",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

+ name

  >  node项目文件名,会出现

+ version

  > 版本号

+ description

  > 项目介绍、说明

+ main

  > 主要js执行入口

+ scripts

  > 执行脚本，例如：
  >
  > ```json
  > {
  >     "script":{
  >         "build": "webpack"
  >     }
  > }
  > ```
  >
  > 则可以执行`npm run build`命令，且实际执行的是webpack命令

+ keywords

  > 关键字，常用于查找分类

+ author

  > 制作人信息

+ license

  > 使用协议



当然除去上面基本选项还有其他常用选项：

+ contributors
+ files
+ bugs
+ bin
+ man
+ directories
+ respository
+ scripts
+ config
+ dependencies
+ git
+ peerDependencies
+ bundleDependencies
+ optionalDependencies