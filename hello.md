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