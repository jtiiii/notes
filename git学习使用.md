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
  git init
  ```


+ 将本地仓库连接远程仓库

  ```shell
  git remote
  ```

+ 从远程仓库克隆到本地仓库

  ```shell
  git clone user@server:repoPath.git
  ```

  ​

