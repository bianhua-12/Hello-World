---
title: homework
date: 2022-05-03
---

~~收作业的同学可以给个小星星吗（）~~

-----------------------------------------------------------------------

2022-05-07更新

没审题。。。。原来是要公私钥登录

```
C:\Users\DELL>ssh-keygen
```

```
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\DELL/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\DELL/.ssh/id_rsa.
Your public key has been saved in C:\Users\DELL/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:gZIGxPOqGvj89qd5MaV20Nbw4miqlhbluacoYESb7xQ dell@DESKTOP-PQOMVUV
The key's randomart image is:
+---[RSA 3072]----+
| oo              |
| .o. . .  .      |
|. oo+ . .. +     |
| + E... ..= o    |
|. ...o .SB .     |
|o..o. o B o      |
|+oo  o = +       |
|.+..=.o.+        |
|o o*+o=*         |
+----[SHA256]-----+
```

没改PasswordAuthentication，怕出问题（计算机小白只用过GitHub桌面版）

然后打开公钥

发现公钥是

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+DeRwEPbuMBYzCYvnL9EVqByxesYfosczzhGIKeD0o1OlbVW3a2GyyJSPiLs6O7uBTy+iK470ZaNq+ySdvNmeh+vh8xo27vcMLM2Sl39bC80m4w3WZqm6JzBgvP3FcU3lo2c6cdbIzPiJtX3u/L97G9vxwvPUh9HDQYzq9in2PK9ZO+elKJPh9gUD2DjmGgV/hspckQ8a38d2wuFF4Nb7VOTYboWc7JIqhqOw6bq6D3uvGIASLQPllel06bR31A/JkR/opfOCkkL6aIwRo8trR/P/ST/SGlaMtNGcPUUT1mhfC6XUD13q84IcBf/5Kj5OE7fnNiPQCCFiJ4X1+V05zmwUsf3uFsOUy8zvPUJYoAlTlvZ30iZRPoA4Y/2McFONRafDSxmZtVEprS3AIYY0OSuUVplJvHKWXDHpu+0VfIz3mq9QrDoLlkJzaHuivIJKixnBTMTXQW3Yfa7TveZx+e6Xw0hkoqkboYfMO93eNmyVDKLo6yN2PLp4WPPG+sE= dell@DESKTOP-PQOMVUV

```

上传即可

然后登录

```
C:\Users\DELL>ssh -T git@github.com
```

```
Hi bianhua-12! You've successfully authenticated, but GitHub does not provide shell access.
```

好耶！

##### WSL

这次连接wsl，首先通过shell登录，然后

```
root@DESKTOP-PQOMVUV:/mnt/c/Users/DELL# ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /root/.ssh/id_rsa
Your public key has been saved in /root/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:EvjBW9WasC9rNllG4342Opn5ng4qvRP7jfaGEEc88vA root@DESKTOP-PQOMVUV
The key's randomart image is:
+---[RSA 3072]----+
|         ...     |
|     o  +.+ .    |
|    . + .O +     |
|     . =o E      |
|      + S* .     |
|       .+ =      |
|       . @.=     |
|      . X.O+=.   |
|       +o*+@B.   |
+----[SHA256]-----+
```

然后将公钥导入authorized_keys文件

```
cat id_rsa.pub >>authorized_keys
cat authorized_keys
```

然后将私钥保存到本地（我是直接复制的）

接着，改wsl里的配置

```
vim /etc/ssh/sshd_config
```

```
PubkeyAuthentication yes // 授权公钥登录
AuthorizedKeysFile      .ssh/authorized_keys // 授权文件路径
```

重启sshd服务

```
/etc/init.d/ssh restart
```

为了远程登录我们这里用的是Xshell

导入密钥的时候发现不行，因为是直接复制然后新建txt改后缀名的方式，之前还有密码保护的现在输入密码不好使

裂开

成功将id_rsa导入

```
 cp ./id_rsa /mnt/d/install/
```

然后登录，发现每次要输入密码，跟密钥没关系？？

所以我们把密码关了

```
vim /etc/ssh/sshd_config
```

现在连接，结果

```
csh@172.22.92.72: Permission denied (publickey).
```

```
C:\Users\DELL\.ssh>ssh -p 8022 root@172.22.92.72
Welcome to Ubuntu 20.04 LTS (GNU/Linux 5.10.16.3-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon May  9 19:05:27 CST 2022

  System load:  0.0                Processes:             20
  Usage of /:   2.0% of 250.98GB   Users logged in:       0
  Memory usage: 4%                 IPv4 address for eth0: 172.22.92.72
  Swap usage:   0%


22 updates can be applied immediately.
11 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable



This message is shown once a day. To disable it please create the
/root/.hushlogin file.
root@DESKTOP-PQOMVUV:~#
```

最后发现是用户名不对，我的登录用户是csh，但我之后的所有操作都是开了root做的。。。真的裂开

然后执行要求里的

```
uname -a
ls ~/.ssh
```

```
root@DESKTOP-PQOMVUV:~/.ssh# ls ~/.ssh
authorized_keys  id_rsa.pub
root@DESKTOP-PQOMVUV:~/.ssh# uname -a
Linux DESKTOP-PQOMVUV 5.10.16.3-microsoft-standard-WSL2 #1 SMP Fri Apr 2 22:23:49 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
root@DESKTOP-PQOMVUV:~/.ssh#
```

