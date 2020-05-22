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

+ **name**

  >  node项目文件名,会出现

+ **version**

  > 版本号

+ **description**

  > 项目介绍、说明

+ **main**

  > 主要js执行入口

+ **scripts**

  > scripts是一个对象，里面制定了项目的生命周期各个环节需要执行的命令，key为事件，value为需要执行的命令
  >
  > 执行脚本，例如：
  >
  > ```json
  > {
  >     "script": {
  >         "build": "webpack"
  >     }
  > }
  > ```
  >
  > 则可以执行`npm run build`命令，且实际执行的是webpack命令
  >
  > npm都会提供部分指令的钩子:pre...,post...
  >
  > + **install: preinstall ,postinstall**
  > + **pack: prepack, postpack**
  > + **publish: prepublish, postpublish**
  > + **test: pretest, posttest**
  > + **uninstall: preuninstall, postuninstall**
  > + ....
  >
  > 需要注意的是部分复合命令，比如**restart** 会顺序执行三个脚本命令: **stop, restart, start**
  >
  > 实际执行顺序的时候为：
  >
  > `prereastart -> prestop -> stop -> poststrop -> restart -> prestart -> start -> poststart -> postrestart `
  >
  > 

+ **keywords**

  > 关键字，常用于查找分类

+ **author**

  > 制作人信息

+ **license**

  > 使用协议



当然除去上面基本选项还有其他常用选项：

+ **contributors**

  > 和 author 类似， 不过contributors 是一群制作者
  >
  > E.g.
  >
  > ```json
  > {
  >     "contributors":[
  >         {
  >             "name": "Funeral Objects",
  >             "email": "874972403@qq.com",
  >             "url": "https://github.com/jtiiii"
  >         }
  >     ]
  > }
  > ```
  >
  > 

+ **files**

  > files属性是一个数组,内容是模块下的文件或文件名，如果是文件夹名，则文件夹所有的文件都会被包含进来，如果想排除一些文件，你可以在模块根目录下创建`.npmignore`文件

+ **bugs**

  > 出现bug的时候提交的建议和反馈的地址或者邮箱,url和email均为可选
  >
  > E.g.
  >
  > ```json
  > {
  >     "bugs": {
  >         "url": "https://github.com/jtiiii/notes/issues",
  >         "email": "874972403@qq.com"
  >     }
  > }
  > ```
  >
  > 

+ **bin**

  > 有很多模块需要有些额外的可执行模块，可以让npm工作变得更简单

+ **man**

  > 指定一个或通过数组指定一些文件让Liunx下的man命令查找文档地址

+ **respository**

  > 指定一个代码存放位置，如果想要对你的项目贡献代码的人有帮助
  >
  > E.g.
  >
  > ```json
  > {
  >     "repository" : {
  >         "type": "git",
  >         "url": "https://github.com/jtiiii/notes.git"
  >     }
  > }
  > ```
  >
  > 

+ **config**

  > 该字段可以用于设定环境变量
  >
  > E.g.
  >
  > ```json
  > {
  >     "config": {
  >         "port": "8080"
  >     }
  > }
  > ```
  >
  > 

+ **dependencies**

  > 该字段指定了项目所需模块
  >
  > E.g.
  >
  > ```json
  > {
  >     "dependencies": {
  > 	    "jquery": "^3.3.1"
  >     }
  > }
  > ```
  >
  > 

+ **devdependencies**

  > 该字段制定了项目开发阶段所需模块
  >
  > E.g.
  >
  > ```json
  > {
  >     "devdependencies": {
  >         "webpack": "^4.12.0",
  >         "webpack-cli": "^3.0.7"
  >     }
  > }
  > ```
  >
  > 

+ **peerDependencies**

  > 指定插件宿主依赖
  >
  > 比如我我写了一个jquery插件：`my-jquery-plugin` 只能在`jquery-3.x.x`版中使用（而且我没有写`require` 来引入 jquery使用，而是从`global`中获取jquery对象），但是在其他模块下使用`my-jquery-plugin`插件时候，也同时引入了`jquery-1.x.x`版本，此时树形图是这样的：
  >
  > ```
  > -- jquery 1.11.0
  > -- my-jquery-plugin 1.0.0
  > 	└─ jquery 3.3.1
  > ```
  >
  > 此时my-jquery-plugin在global对象中引用 jquery却是1.11.0版本的，会导致部分错误。而且很难察觉。
  >
  > 这时候就需要peerDepeendencies来提示安装my-jquery-plugin的时候，引用的jquery必须为3.3.1
  >
  > ```json
  > {
  >     "name": "my-jquery-plugin",
  >     "peerDependencies":{
  >         "jquery": "^3.3.1"
  >     }
  > }
  > ```
  >
  > 

+ **bundleDependencies**

  > 值为数组，需要同时打包的依赖
  >
  > E.g.
  >
  > ```json
  > {
  >     "dependencies": {
  >         "jquery": "^3.3.1"
  >     },
  >     "bundleDependencies": ["jquery"]
  > }
  > ```
  >
  > 在打包时候将jquery一起打包进去
  >
  > 

+ **optionalDependencies**

  > 可选依赖

+ **preferGlobal**

  > 是否建议部署时候为全局模块
  >
  > E.g.
  >
  > ```json
  > {
  >     "preferGlobal": "true"
  > }
  > ```
  >
  > 此时如果该包被非全局模式下部署会显示警告建议。

+ **engines**

  > 指定在什么环境平台
  >
  > E.g.
  >
  > ```json
  > {
  >     "engines": {
  >         "node": ">= 0.10.0 <0.12",
  >         "npm": "~1.0.20"
  >     }
  > }
  > ```

+ **browser**

  > 指定browser指定该模板供浏览器使用的版本。Browserify这样的浏览器打包工具，通过它就知道该打包那个文件。 



##关于指定版本配置

+ 无符号，表示完全指定版本E.g. `1.2.2`，版本号按照**大版本.次要版本.小版本**
+ `~` 波浪号，表示保持小版本最新，E.g. `~1.2.2` 表示引用1.2.x 最新版
+ `^` 插入号，表示保持大版本最新，E.g. `^1.2.2` 表示1.x.x 最新版
+ `latest`, 表示保持最新包