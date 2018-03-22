# Linux新建用户如何添加root权限

个人用户的权限只可以在本home下有完整权限，其他目录要看别人授权。而经常需要root用户的权限，这时候sudo可以化身为root来操作。我记得我曾经sudo创建了文件，然后发现自己并没有读写权限，因为查看权限是root创建的。

新创建的用户并不能使用sudo命令，需要给他添加授权。

sudo命令的授权管理是在sudoers文件里的。可以看看sudoers：

```shell
[root@localhost ~]# sudoers
bash: sudoers: 未找到命令...
[root@localhost ~]# whereis sudoers
sudoers: /etc/sudoers /etc/sudoers.d /usr/libexec/sudoers.so /usr/share/man/man5/sudoers.5.gz
```

找到这个文件位置之后再查看权限：

```shell
[root@localhost ~]# ls -l /etc/sudoers
-r--r----- 1 root root 4251 9月  25 15:08 /etc/sudoers
```

是的，只有只读的权限，如果想要修改的话，需要先添加w权限：

```
[root@localhost ~]# chmod -v u+w /etc/sudoers
mode of "/etc/sudoers" changed from 0440 (r--r-----) to 0640 (rw-r-----)
```

然后就可以添加内容了，在下面的一行下追加新增的用户：

```shell
root@localhost ~]# vim /etc/sudoers


## Allow root to run any commands anywher  
root    ALL=(ALL)       ALL  
linuxidc  ALL=(ALL)       ALL  #这个是新增的用户
```

wq保存退出，这时候要记得将写权限收回：

```shell
[root@localhost ~]# chmod -v u-w /etc/sudoers
mode of "/etc/sudoers" changed from 0640 (rw-r-----) to 0440 (r--r-----)
```

这时候使用新用户登录，使用sudo:

```shell
[linuxidc@localhost ~]$ sudo cat /etc/passwd
[sudo] password for linuxidc: 

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.
```

第一次使用会提示你，你已经化身超人，身负责任。而且需要输入密码才可以下一步。如果不想需要输入密码怎么办，将最后一个ALL修改成NOPASSWD: ALL。

> 转自：https://blog.csdn.net/ggxiaobai/article/details/53504989