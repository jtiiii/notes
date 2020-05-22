SSH 登陆

```shell
$ssh
usage: ssh
        [-b bind_address] 
        [-c cipher_spec]

        [-D [bind_address:]port] 
        [-E log_file] 
        [-e escape_char]

        [-F configfile] 
        [-I pkcs11] 
        [-i identity_file]

        [-J [user@]host[:port]] 
        [-L address] 
        [-l login_name] 
        [-m mac_spec]

        [-O ctl_cmd] 
        [-o option] 
        [-p port] 
        [-Q query_option] 
        [-R address]

        [-S ctl_path] 
        [-W host:port] 
        [-w local_tun [:remote_tun]]

        [user@]hostname [command]
```

一般常用示例：

```shell
$ssh root@192.168.3.200
```



SSL证书的使用:

生成KeyGen

```shell
$ssh-keygen

usage: ssh-keygen [-q] [-b bits] [-t dsa | ecdsa | ed25519 | rsa]
                  [-N new_passphrase] [-C comment] [-f output_keyfile]
       ssh-keygen -p [-P old_passphrase] [-N new_passphrase] [-f keyfile]
       ssh-keygen -i [-m key_format] [-f input_keyfile]
       ssh-keygen -e [-m key_format] [-f input_keyfile]
       ssh-keygen -y [-f input_keyfile]
       ssh-keygen -c [-P passphrase] [-C comment] [-f keyfile]
       ssh-keygen -l [-v] [-E fingerprint_hash] [-f input_keyfile]
       ssh-keygen -B [-f input_keyfile]
       ssh-keygen -D pkcs11
       ssh-keygen -F hostname [-f known_hosts_file] [-l]
       ssh-keygen -H [-f known_hosts_file]
       ssh-keygen -R hostname [-f known_hosts_file]
       ssh-keygen -r hostname [-f input_keyfile] [-g]
       ssh-keygen -G output_file [-v] [-b bits] [-M memory] [-S start_point]
       ssh-keygen -T output_file -f input_file [-v] [-a rounds] [-J num_lines]
                  [-j start_line] [-K checkpt] [-W generator]
       ssh-keygen -s ca_key -I certificate_identity [-h] [-U]
                  [-D pkcs11_provider] [-n principals] [-O option]
                  [-V validity_interval] [-z serial_number] file ...
       ssh-keygen -L [-f input_keyfile]
       ssh-keygen -A
       ssh-keygen -k -f krl_file [-u] [-s ca_public] [-z version_number]
                  file ...
       ssh-keygen -Q -f krl_file file ...
```

一般使用示例：

```Shell
$ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/peizangpin/.ssh/id_rsa): test
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in test.
Your public key has been saved in test.pub.
The key fingerprint is:
SHA256:9WFbJfcLHYCn4gBj4KXGKAcfMl30PUnt1/LnaSXkxaQ peizangpin@localhost
The key's randomart image is:
+---[RSA 2048]----+
|+..++.  ..  ..o.o|
| ==.o= o ... ..++|
|..o=. + +.. =o.=.|
|...    . +.+o+E +|
|        S ..o= o |
|         .    + o|
|               +o|
|               o.|
|              .  |
+----[SHA256]-----+
#执行完毕后会产生test和test.pub文件
```



将SSL证书上传到服务器，使之免密码登陆

ssh-copy-id

```shell
$ssh-copy-id -i ~/.ssh/test root@192.168.3.200
```

