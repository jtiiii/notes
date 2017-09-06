# git

git和subversion 一样属于文件管理系统

git最初是由linux的创始人为了管理linux代码而开发的**分布式**代码管理工具

分布式管理是每个服务器都可以当主版本取决于你想要什么服务器。



# Git安装

略。自行百度总能找到适合自己的安装方式



远程仓库 —> 本地仓库 —> Index —> workspace



首先git会在每一台机子上建一个本地仓库。主要日常代码是在本地仓库中进行版本库

想要发布到远程仓库（比如github）则需要将本地仓库的代码推送(push)到远程仓库



几个命令基础

+ 初始化本地仓库

  ```Shell
  $git init
  ```


+ 将本地仓库连接远程仓库

  ```shell
  $git remote
  ```

+ 从远程仓库克隆到本地仓库

  ```shell
  $git clone user@server:repoPath.git
  ```

+ 查看历史提交信息

  ```shell
  $git log
  ```

  ```shell
  #示例
  localhost:git-learn peizangpin$ git log
  commit c539cfede5ecbf38613ac1db92cfbbbe55311fb3
  Author: 陪葬品 <874972403@qq.com>
  Date:   Thu Sep 7 07:11:17 2017 +0800

      提交一部分

  commit a18780ef27614d9ba36118f8bb5ae7a37d0a0445
  Author: 陪葬品 <874972403@qq.com>
  Date:   Wed Sep 6 18:10:18 2017 +0800

      没什么好说的

  commit d6b2398b3890a9f17dce1eb3125361087c5499c7
  Author: 陪葬品 <874972403@qq.com>
  Date:   Wed Sep 6 18:05:25 2017 +0800

      感觉没啥好些的

  commit e3358c84c156326de095aeb518e60da222fbc03a
  Author: 陪葬品 <874972403@qq.com>
  Date:   Wed Sep 6 15:01:18 2017 +0800

      增加

  commit 556f390281fd4df3a26553f58ea0ec3b07bdd1f6
  Author: 陪葬品 <874972403@qq.com>
  Date:   Wed Sep 6 14:59:21 2017 +0800

      添加一个正则表达式的对照表

  commit de425ff1add6c4fedbbc62d2a972df658df94aad
  Author: 陪葬品 <874972403@qq.com>
  Date:   Wed Sep 6 07:24:17 2017 +0800

      new file

  commit 6f5dc817e7e8f86dccabd373183b5c9f824824d8
  Author: 陪葬品 <874972403@qq.com>
  Date:   Tue Sep 5 18:11:29 2017 +0800

      修正

  ```

  可以看到有**commit**,**Author**,**Date**和**备注**这几个信息

  commit后面一大串字符为提交的版本的唯一ID，可以利用这个字符串来进行回退


