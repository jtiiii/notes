[TOC]

# git

git和subversion 一样属于文件管理系统

git最初是由linux的创始人为了管理linux代码而开发的**分布式**代码管理工具

分布式管理是每个服务器都可以当主版本取决于你想要什么服务器。

该笔记只记录常用的一些git命令，完整命令查看请[https://git-scm.com/docs](https://git-scm.com/docs)





# Git安装

略。自行百度总能找到适合自己的安装方式



远程仓库 —> 本地仓库 —> Index —> workspace



首先git会在每一台机子上建一个本地仓库。主要日常代码是在本地仓库中进行版本库

想要发布到远程仓库（比如github）则需要将本地仓库的代码推送(push)到远程仓库



# Git命令

几个命令基础

## git init

```Shell
#初始话当前文件夹为git仓库
$git init
```


## git remote

```shell
#列出远程仓库
$git remote

#列出远程仓库的详细信息
$git remote -v
```
### git remote add

```shell
#添加远程仓库地址
$git remote add [name] [git-url]
```

### git remote rename

```shell
#重命名远程仓库地址
$git remote rename [oldName] [newName]
```

### git remote remove

```shell
#删除远程仓库地址
$git remote remove [name]
```



## git clone

```shell
#将远程仓库克隆到本地
$git clone [git-url]
```



##git log

```shell
#查看历史提交信息
$git log

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
....
```

可以看到有**commit**,**Author**,**Date**和**备注**这几个信息

commit后面一大串字符为提交的版本的唯一ID，可以利用这个字符串来进行回退、比价差别等



## git status

```shell
#查看当前git仓库状态
$git status

#示例(中文转成Unicode)
localhost:notes peizangpin$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed: #可以commit的文件
  (use "git reset HEAD <file>..." to unstage)

	renamed:    "Javascript\345\206\215\345\255\246\344\271\240/1-\346\225\260\346\215\256\347\261\273\345\236\213\357\274\214\346\223\215\344\275\234\347\254\246\357\274\214\350\257\255\345\217\245\357\274\214\345\207\275\346\225\260.md" -> "Javascript/1-\346\225\260\346\215\256\347\261\273\345\236\213\357\274\214\346\223\215\344\275\234\347\254\246\357\274\214\350\257\255\345\217\245\357\274\214\345\207\275\346\225\260.md"
	renamed:    "Javascript\345\206\215\345\255\246\344\271\240/2-\345\217\230\351\207\217\343\200\201\344\275\234\347\224\250\345\237\237\343\200\201\345\206\205\345\255\230.md" -> "Javascript/2-\345\217\230\351\207\217\343\200\201\344\275\234\347\224\250\345\237\237\343\200\201\345\206\205\345\255\230.md"
	renamed:    "Javascript\345\206\215\345\255\246\344\271\240/3-\345\274\225\347\224\250\347\261\273\345\236\213.md" -> "Javascript/3-\345\274\225\347\224\250\347\261\273\345\236\213.md"
	renamed:    "Javascript\345\206\215\345\255\246\344\271\240/4-\345\237\272\346\234\254\345\214\205\350\243\205\347\261\273\345\236\213.md" -> "Javascript/4-\345\237\272\346\234\254\345\214\205\350\243\205\347\261\273\345\236\213.md"
	renamed:    "Javascript\345\206\215\345\255\246\344\271\240/Javascript \345\206\215\345\255\246\344\271\240.md" -> "Javascript/Javascript \345\206\215\345\255\246\344\271\240.md"
	renamed:    "Javascript\345\206\215\345\255\246\344\271\240/\346\255\243\345\210\231\350\241\250\350\276\276\345\274\217.md" -> "Javascript/\346\255\243\345\210\231\350\241\250\350\276\276\345\274\217.md"

#无法被commit的文件，要想commit需要执行，按照如下指令执行 git add或者rm
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    "git\345\255\246\344\271\240\344\275\277\347\224\250.md"

#没有进入git版本管理的文件，需要执行git add来加入版本管理
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	git/

localhost:notes peizangpin$ 

```



## git add

```shell
#将Untracked的文件加入到git版本管理中去
$git add [file-path]
```



## git rm

```shell
#类似rm，将指定文件或者文件夹移除git仓库
$git rm  -<param> [file-path]
```



## git commit

```shell
#将改动提交形成一个新的版本
$git commit
```

 

## git reset

```shell
#将指定文件返回到HEAD版本状态(常用来撤销git add)
$git reset HEAD [file-path]

#将整个仓库退回指定git版本
$git reset --hard [commit-id]
```





# Git 分支管理

## git checkout

检出——创建/切换分支

`git checkout [options] <branchName>`

**options**

+ `-b` 创建并切换新分支

  > ```bash
  > #创建并切换到名为issu34分支
  > $git checkout -b issu34
  > 
  > #相当于执行了下面两条命令
  > #$git branch issu34
  > #$git checkout issu34
  > ```



## git branch

分支管理

`git branch [options] <branchName>`

**options**

+ `--list` 查看分支列表
+ `--all` 查看所有分支列表（包括远程分支）
+ `-v` 带有hash信息的查看分支列表
+ `-d` 删除分支

