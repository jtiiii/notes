# Shell

shell 是一个程序，是用户和计算机交互下发指令的一个程序，是一个**命令解析器**，不过和操作程序的概念还是不一样，shell只服务于解析用户的下达的指令，并执行。

常见的shell有一下几种：

- Bourne SHell(sh) 
- Bourne Again SHell(bash) 
- C SHell(csh) 
- KornSHell(ksh) 
- zsh
- bash

## bash

常见的shell脚本都差不多，但是linux预设的是bash`/bin/bash`

```bash
▶ /bin/bash --help
GNU bash，版本 4.2.46(2)-release-(x86_64-redhat-linux-gnu)
用法：	/bin/bash [GNU 长选项] [选项] ...
	/bin/bash [GNU 长选项] [选项] 脚本文件 ...
GNU 常选项:
	--debug
	--debugger
	--dump-po-strings
	--dump-strings
	--help
	--init-file
	--login
	--noediting
	--noprofile
	--norc
	--posix
	--protected
	--rcfile
	--rpm-requires
	--restricted
	--verbose
	--version
Shell 选项:
	-irsD 或 -c 命令 或 -O shopt选项		(仅适合调用)
	-abefhkmnptuvxBCHP 或 -o 选项
请输入`/bin/bash -c "help set"' 以获得关于 shell 选项的更多信息
请输入 `/bin/bash -c help' 以获得关于 shell 内嵌命令的更多信息.
```

```bash
▶ /bin/bash -c "help"
GNU bash， 版本 4.2.46(2)-release (x86_64-redhat-linux-gnu)
这些 shell 命令是内部定义的。请输入 `help' 以获取一个列表.
输入 `help 名称' 以得到有关函数`名称'的更多信息.
使用 `info bash' 来获得关于 shell 的更多一般性信息
使用 `man -k' 或 `info' 来获取不在列表中的命令的更多信息.

名称旁边的星号 (*) 意味着该命令被禁用.

 job_spec [&]                            history [-c] [-d 偏移量] [n] 或 >
 (( 表达式 ))                         if 命令; then 命令; [ elif 命?>
 . 文件名 [参数]                    jobs [-lnprs] [任务声明 ...] 或>
 :                                       kill [-s 信号声明 | -n 信号编>
 [ 参数... ]                           let 参数 [参数 ...]
 [[ 表达式 ]]                         local [option] 名称[=值] ...
 alias [-p] [名称[=值] ... ]          logout [n]
 bg [任务声明 ...]                   mapfile [-n 计数] [-O 起始序号>
 bind [-lpvsPVS] [-m 键映射] [-f ?>  popd [-n] [+N | -N]
 break [n]                               printf [-v var] 格式 [参数]
 builtin [shell 内嵌 [参数 ...]]     pushd [-n] [+N | -N | 目录]
 caller [表达式]                      pwd [-LP]
 case 词 in [模式 [| 模式]...) ?>  read [-ers] [-a 数组] [-d 分隔?>
 cd [-L|[-P [-e]]] [dir]                 readarray [-n 计数] [-O 起始序?>
 command [-pVv] 命令 [参数 ...]      readonly [-aAf] [name[=value] ...] o>
 compgen [-abcdefgjksuv] [-o 选项]  >  return [n]
 complete [-abcdefgjksuv] [-pr] [-DE] >  select NAME [in 词语 ... ;] do 命>
 compopt [-o|+o 选项] [-DE] [名称 >  set [-abefhkmnptuvxBCHP] [-o option->
 continue [n]                            shift [n]
 coproc [名称] 命令 [重定向]      shopt [-pqsu] [-o] [选项名 ...]
 declare [-aAfFgilrtux] [-p] [name[=va>  source 文件名 [参数]
 dirs [-clpv] [+N] [-N]                  suspend [-f]
 disown [-h] [-ar] [任务声明 ...]    test [表达式]
 echo [-neE] [参数 ...]                time [-p] 管道
 enable [-a] [-dnps] [-f 文件名] [?>  times
 eval [参数 ...]                       trap [-lp] [[参数] 信号声明 ..>
 exec [-cl] [-a 名称] [命令 [参?>  真
 exit [n]                                type [-afptP] 名称 [名称 ...]
 export [-fn] [名称[=值] ...] 或 e>  typeset [-aAfFgilrtux] [-p] name[=va>
 伪                                     ulimit [-SHacdefilmnpqrstuvx] [限?>
 fc [-e 编辑器名] [-lnr] [起始] >  umask [-p] [-S] [模式]
 fg [任务声明]                       unalias [-a] 名称 [名称 ...]
 for 名称 [in 词语 ... ] ; do 命?>  unset [-f] [-v] [名称 ...]
 for (( 表达式1; 表达式2; 表达>  until 命令; do 命令; done
 function 名称 { 命令 ; } 或 name>  variables - 一些 shell 变量的?>
 getopts 选项字符串 名称 [参?>  wait [编号]
 hash [-lr] [-p 路径名] [-dt] [名?>  while 命令; do 命令; done
 help [-dms] [模式 ...]                { 命令 ; }
```

平常进入的linux终端控制台其实就是`/bin/bash -c`环境

比如：`/bin/bash -c "ls -l"`与`ls -l`是相同的





# .sh -- shell脚本

Linux操作基本是使用命令行操作，但是重复一个复杂的操作是非常繁琐的事情，这时候就需要shell编程

将多个操作写成脚本文件。然后使用或者`source`或者`.`命令执行

虽然shell脚本里面`#`代表注释，但是首行`#!`却代表执行环境，比如:`#!/bin/bash`意思是使用/bin/bash来执行该脚本

E.g.

cat_profile.sh:

```shell
#!/bin/bash
#查看全局配置文件
cat /etc/profile
```

执行cat_profile.sh脚本

```bash
▶ source cat_profile.sh

# /etc/profile

# System wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc

# It's NOT a good idea to change this file unless you know what you
# are doing. It's much better to create a custom.sh shell script in
# /etc/profile.d/ to make custom changes to your environment, as this
# will prevent the need for merging in future updates.

pathmunge () {
    case ":${PATH}:" in
        *:"$1":*)
            ;;
        *)
            if [ "$2" = "after" ] ; then
                PATH=$PATH:$1
            else
                PATH=$1:$PATH
            fi
    esac
}


if [ -x /usr/bin/id ]; then
    if [ -z "$EUID" ]; then
        # ksh workaround
        EUID=`/usr/bin/id -u`
        UID=`/usr/bin/id -ru`
    fi
    USER="`/usr/bin/id -un`"
    LOGNAME=$USER
    MAIL="/var/spool/mail/$USER"
fi

# Path manipulation
if [ "$EUID" = "0" ]; then
    pathmunge /usr/sbin
    pathmunge /usr/local/sbin
else
    pathmunge /usr/local/sbin after
    pathmunge /usr/sbin after
fi

HOSTNAME=`/usr/bin/hostname 2>/dev/null`
HISTSIZE=1000
if [ "$HISTCONTROL" = "ignorespace" ] ; then
    export HISTCONTROL=ignoreboth
else
    export HISTCONTROL=ignoredups
fi

export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL

# By default, we want umask to get set. This sets it for login shell
# Current threshold for system reserved uid/gids is 200
# You could check uidgid reservation validity in
# /usr/share/doc/setup-*/uidgid file
if [ $UID -gt 199 ] && [ "`/usr/bin/id -gn`" = "`/usr/bin/id -un`" ]; then
    umask 002
else
    umask 022
fi

for i in /etc/profile.d/*.sh ; do
    if [ -r "$i" ]; then
        if [ "${-#*i}" != "$-" ]; then 
            . "$i"
        else
            . "$i" >/dev/null
        fi
    fi
done

unset i
unset -f pathmunge

```



## $ - 参数

### 执行shell文件的参数

在执行shell脚本的时候可以传递参数, 使用 `$[n]` 来获取传递的参数

E.g.

```shell
$1 #获取传入的第一个参数
$2 #获取传入的第二个参数
$3 #获取传入的第三个参数
...
$# #为传入参数的总数
```

执行的时候则直接在`.sh` 后面添加需要传入的参数即可

E.g.

**run.sh**

```shell
#!/bin/bash
echo $1
echo $2
echo $3
echo $#
```

运行输出

```bash
▶ ./run.sh arg-1 arg-2 arg-3
arg-1
arg-2
arg-3
3
```

### 最后一次执行命令的退出的状态

**`$?` 是shell变量,表示"最后一次执行命令"的退出状态.0为成功,非0为失败**



## if 条件判断

`shell` 中的 `if`

判断条件：

+ `-eq` 等于 equal
+ `-ne` 等于 not equal
+ `-le` 小于等于 less than or equal to
+ `-ge` 大于等于 great than or equal to
+ `-lt` 小于 less than
+ `-gt` 大于 great than

直接使用比较符需要**双括号 (( ... ))**

+ `<` 小于，如 ` if [ (( $a < $b )) ];`
+ `>` 大于
+ `>=` 大于等于
+ `<=` 小于等于

E.g.

```shell
if [ $? -ne 0 ]; then
	echo "最后一次指令执行失败!"
fi
```



## <<

持续输入代码块，使用该符号意思是，开始产生一个缓冲区来储存多个指令，不执行，直至遇到设定结束字符串

E.g.

```shell
▶ <<END-BLOCK
◀ echo 'hello'
◀ echo 'friends'
◀ END-BLOCK
echo 'hello'
echo 'friends'

```



## EOF

`EOF` 为 End Of File 的缩写，表示为一个文件的结尾或者终止符。

`EOF`可以自定义为任何值，经常配合 `<<` 来一起使用

E.g.

```shell
▶ <<EOF #指令集开始
some commands
EOF #指令集结束
```

