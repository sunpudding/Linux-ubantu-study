# Ubuntu-SSH-RemoteLogin


## 一、简介

__SSH是一种远程登录的程序，主要用于给远程登录会话数据进行加密，保证数据传输的安全，默认端口号是22__
>详细信息可以使用`man ssh`命令进行查看

## 二、ssh安装与配置
**在ubuntu上默认安装openssh，且装上了openssh-client，可以使用命令进行查看**
```
sunny@sunny-VirtualBox:~$ dpkg -l | grep ssh
ii  libssh-4:amd64                             0.6.3-4.3                                    amd64        tiny C SSH library (OpenSSL flavor)
ii  openssh-client                             1:7.2p2-4ubuntu2.4                           amd64        secure shell (SSH) client, for secure access to remote machines
```
**但是我们还需要自行去安装openssh-server**
>`sudo apt-get install openssh-server`

**若系统中没有安装ssh，我们也可以自行安装**
>`sudo apt-get install openssh-client`

**安装好后ssh服务的启动和停止命令如下：**
* 启动
>`sudo service ssh start`
* 查看ssh是否启动
>`sudo ps -e | grep ssh`

```
sunny@sunny-VirtualBox:~$ sudo ps -e | grep ssh
 6525 ?        00:00:00 sshd
```
>**有sshd表示已经启动**
* 停止
>`sudo service ssh stop`

##三、查看本机ip
**命令如下：**

>`ip a`

**或者**
> `ifconfig`

enp0s3下面的inet后面的地址即为本机ip地址

## 四、 SSH远程登录
### 4.1 虚拟机规则
**由于我使用的是虚拟机搭建的Ubuntu，所以若要进行ssh远程登录还需要掌握虚拟机下的一些规则**

|Network type   |Gast -> other Guests | Host -> Guest  |Gast -> external Network|
| ------------- |:-------------:| :-----:|:----------:|
| Not attached  | -             | -      | -          |
| Network Address Translation (NAT)   | -      |   - | ✔|
| Network Address Translation Service |     ✔  |   - | ✔|
| Bridged networking |  ✔             |     ✔  |  ✔  |
|Internal networking |  ✔             |     -  |  -  |
|Host-only networking| ✔              | 	✔    |	-  |


**详细的内容说明可以点击以下的地址**


[overview table of accessoptions](https://www.thomas-krenn.com/en/wiki/Network_Configuration_in_VirtualBox#Internal_networking)

### 4.2 SSH免密登录
**当我们设置好以上内容时，就可以进行SSH远程登录啦，使用命令`ssh user@host`但是每次远程登录都需要输入密码，就比较费劲啦，这个时候我们可以设置免密登录，非常简单方便，let`s go**

* 生成密钥
> 使用命令:`ssh-keygen -t rsa`
```
sun@sun-VirtualBox:~$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/sun/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/sun/.ssh/id_rsa.
Your public key has been saved in /home/sun/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:YAc2nZbyAdq8sc3Q6GYXBOG2tTdefvH7NJQhLaQHRrk sun@sun-VirtualBox
The key's randomart image is:
+---[RSA 2048]----+
|      B=.o.+..   |
|     *.** ..+ .  |
|    . @+=. ..+ o |
|     + %.o E. o o|
|      B S o . .o |
|     o . o +  .o |
|          . . ..o|
|             . .o|
|               .o|
+----[SHA256]-----+
```
**此时在我们的/root/.ssh路径下会生成两个密钥，一个是私钥id_rsa,一个是公钥id_rsa.pub**

* 发送私钥给本机
>命令`ssh-copy-id localhost`
* 发送公钥给其他的计算机
>命令`ssh-copy-id user@host`

```
sun@sun-VirtualBox:~$ ssh-copy-id sunny@10.0.2.15
The authenticity of host '10.0.2.15 (10.0.2.15)' can't be established.
ECDSA key fingerprint is SHA256:X6jZ6D0ybIMu6B5iCxztFVP3CtrCOsSY/aoOYfa/wYQ.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
sunny@10.0.2.15's password:
```
* 测试免密登录
> `ssh localhost`
```
sun@sun-VirtualBox:~$ ssh localhost
Welcome to Ubuntu 16.04.4 LTS (GNU/Linux 4.13.0-36-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

333 packages can be updated.
174 updates are security updates.

New release '18.04.1 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

Last login: Tue Oct  9 18:14:16 2018 from 10.0.2.15

```
> `ssh user@host`
```
sun@sun-VirtualBox:~$ ssh sunny@10.0.2.15
Welcome to Ubuntu 16.04.5 LTS (GNU/Linux 4.13.0-36-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

23 个可升级软件包。
13 个安全更新。

Last login: Mon Oct  8 20:40:42 2018 from 10.7.249.97
```
#### 现在我们已经完成了linux间的远程登录啦^-^
