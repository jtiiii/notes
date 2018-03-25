# git-svn

svn和git都是目前国内常用的版本控制软件。根据不同的开发团队协作要求会选择使用git或者svn进行版本控制。这就可能会有git迁移到svn，svn迁移到git上的情况出现。

git早就支持对svn的操作，因此git和svn互相迁移基本使用git就够了

```bash
#git中的 git svn为主要使用命令
$git svn
```





## svn 迁移到 git

迁移测试svn项目：http://\*\*\*\*/sicilin-module

从svn迁移到git有两种方法

1. 直接克隆

   ```bash
   #一步到位
   #git svn clone [url]
   $git svn clone http://****/sicilin-module
   ```

2. 合并原有git仓库

   ```bash
   #初始化并新增svn仓库地址
   #git svn init [url]
   $git svn init http://****/sicilin-module
   #使用fetch 进行获取svn上的文件,fetch之后，会默认存在本地git-svn分支里
   $git svn fetch
   #合并分支master和git-svn分支
   #由于两个分支的提交记录不一致，直接合并会产生历史冲突错误，因此使用--allow-unrelated-histories 进行合并
   $git merge master git-svn --allow-unrelated-historiessd
   ```
   合并后git仓库的Map图例：
   ![avatar](img/9BAEF16F-A14B-44B6-825E-AA9DE3811A51.png)



## git 迁移到 svn

下面方法也不是很完善，要么出现如下错误：Unable to determine upstream SVN information from working tree history

要么就是迁移版本/文件不全



```bash
#在git仓库中建立svn远程仓库地址
$git svn init [url]
#使用fetch 命令获取svn文件以及其版本号
$git svn fetch
#fetch结束后会有如下版本号[svn = git]这的版本号对应记录
#比如：[r2906 = bf956eba5233f35df4d1e7b47f9b28132bcc3530 (refs/remotes/git-svn)]
#查看git当前仓库首次commit记录
$git log --pretty=oneline master | tail -n 1
#比如 243a6579c62193123eccf141e40fe375b7f74981 第一次提交
$echo "243a6579c62193123eccf141e40fe375b7f74981 bf956eba5233f35df4d1e7b47f9b28132bcc3530" >> .git/info/grafts
#把git仓库里的第一次提交记录(243a65...),添加到svn的提交记录（bf956...）之后
$git svn dcommit
```

刚fetch完svn上的代码时候，会自动产生git-svn分支，如下图示：

![avatar](img/D55CC91E-DA1C-45AD-8AE6-0F2D049C826B.png)