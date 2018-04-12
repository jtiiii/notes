# Versions

代码经过多次修改之后，会产生多个版本号

特别是在有多个子模块这样的项目中，父级模块与子模块的版本号不一致。一个个去修改有太费时间了。因此`Maven`中有`versions`插件来进行简易的模块之间的版本控制

一般在父级模块下操作。



###versions:set

设置版本号

E.g.

```bash
mvn versions:set -DnewVersion=0.0.1 -DprocessAllModules=true
```

将版本号修改该为0.0.1，并让该目录下所有模块生效（无视父子模块关系）

执行后，各个模块下的会多出一份`pom.xml.versionsBackup`文件

此时觉得修改不满意的话，可以使用`version:revert`回滚



###versions:revert

回滚操作

E.g.

```bash
mvn versions:revert
```

在修改各个模块的版本之后，即有`pom`的的备份文件`pom.xml.versionBackup`产生时候，可以用于回滚



###versions:commit

版本号提交

E.g.

```bash
mvn version:commit
```

修改版本号的确定操作



###versions:update-child-modules

更新子模块版本号



## 部分参数介绍

| 参数  | 默认值 | 说明 |
| ----- | ------ | ---- |
|allowSnapshots |`false` |是否更新-snapshot快照版|
|artifactId |`${project.artifactId}` |指定artifactId |
|generateBackupPoms |`true` |是否备份pom文件 |
|groupId |`${project.groupId}` |指定groupId |
|newVersion | |设置的新版本号 |
|nextSnapshot |`false` |更新版本号为下一个快照版本号|
|oldVersion |`${project.version}` |指定需要更新的版本号可以使用缺省‘*’|
|processAllModules |`false` |是否更新目录下所有模块无论是否声明父子节点|
|processDependencies |`true` |是否更新依赖其的版本号|
|processParent |`true` |是否更新父节点的版本号|
|processPlugins |`true` |是否更新插件中的版本号|
|processProject |`true` |是否更新模块自身的版本号|
|removeSnapshot |`false` |移除snapshot快照版本，使之为release稳定版|
|updateMatchingVersions |`true` |是否更新在子模块中显式指定的匹配版本(如/项目/版本)。|



该插件的更多用法请参考：http://www.mojohaus.org/versions-maven-plugin/index.html