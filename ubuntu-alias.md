# Linux学习之alias命令
## 1.1 alias功能介绍
>**当我们经常需要在命令窗键入复杂冗长的命令时，alias就派上用场啦。alias允许用户为命令创建简单的名称或缩写，哪怕这个缩写只有一个字符。即为指令设置别名。**
## 1.2 alias语法
> **语法：alias [name=”value”]**

>  **Alias为当前用户提供啦有效的别名列表，注意：等号前后没有空格。**
```sunny@sunny-VirtualBox:~$ alias
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l='ls -CF'
alias la='ls -A'
alias ll='ls -alF'
alias ls='ls --color=auto'
```

## 1.3 简单示例
```
sunny@sunny-VirtualBox:~$ ls
Anaconda   backups   local    Repository    测试文件  模板  图片  下载  桌面
anaconda3  commands  pycharm  tutorialwork  公共的    视频  文档  音乐
sunny@sunny-VirtualBox:~$ alias ls='ls -al'
sunny@sunny-VirtualBox:~$ ls
总用量 280
drwxr-xr-x 34 sunny sunny  4096 9月  25 13:21 .
drwxr-xr-x  3 root  root   4096 7月  11 23:40 ..
drwxrwxr-x  2 sunny sunny  4096 8月  15 22:09 Anaconda
drwxrwxr-x 23 sunny sunny  4096 8月  15 22:19 anaconda3
drwxrwxr-x  9 sunny sunny  4096 9月  25 13:03 .atom

```
>**ls是一个常用的命令，默认列出当前路径下的文件以及文件夹，-a选项指示ls显示隐藏文件和文件夹，-l告诉ls提供文件和子目录的详细信息。
若想要暂时禁用ls别名，可以使用\ls,注意不要留有空格**
```
sunny@sunny-VirtualBox:~$ \ls
Anaconda   backups   local    Repository    测试文件  模板  图片  下载	桌面
anaconda3  commands  pycharm  tutorialwork  公共的    视频  文档  音乐
```
>**当然，这个示例我们还可以进一步的简化。**
```
sunny@sunny-VirtualBox:~$ alias l='ls -al'
sunny@sunny-VirtualBox:~$ l
总用量 280
drwxr-xr-x 34 sunny sunny  4096 9月  25 13:21 .
drwxr-xr-x  3 root  root   4096 7月  11 23:40 ..
drwxrwxr-x  2 sunny sunny  4096 8月  15 22:09 Anaconda
drwxrwxr-x 23 sunny sunny  4096 8月  15 22:19 anaconda3
drwxrwxr-x  9 sunny sunny  4096 9月  25 13:03 .atom
```
>**除了-l这样的选项，我们还可以在values中添加参数。**
```
sunny@sunny-VirtualBox:~$ alias l='ls -al /etc'
sunny@sunny-VirtualBox:~$ l
总用量 1188
drwxr-xr-x 132 root root   12288 9月  25 12:39 .
drwxr-xr-x  24 root root    4096 9月  18 10:47 ..
drwxr-xr-x   3 root root    4096 3月   1  2018 acpi
-rw-r--r--   1 root root    3028 3月   1  2018 adduser.conf
drwxr-xr-x   2 root root    4096 9月  24 23:43 alternatives
```
>**你以为这样就完了吗，nonono，让我们继续前进。**

>**alias可以将多个命令包含在value中，各个命令用分号分隔。**

>**alias l=‘pwd;ls’ 别名l首先启动pwd显示当前路径，然后启动ls显示当前的文件目录。**
```
sunny@sunny-VirtualBox:~$ alias l='pwd;ls'
sunny@sunny-VirtualBox:~$ l
/home/sunny
总用量 280
drwxr-xr-x 34 sunny sunny  4096 9月  25 13:21 .
drwxr-xr-x  3 root  root   4096 7月  11 23:40 ..
drwxrwxr-x  2 sunny sunny  4096 8月  15 22:09 Anaconda
drwxrwxr-x 23 sunny sunny  4096 8月  15 22:19 anaconda3
drwxrwxr-x  9 sunny sunny  4096 9月  25 13:03 .atom
```
>**我们甚至可以用别名来调用其他的别名。**
```
sunny@sunny-VirtualBox:~$ unalias ls
sunny@sunny-VirtualBox:~$ ls
Anaconda   backups   local    Repository    测试文件  模板  图片  下载	桌面
anaconda3  commands  pycharm  tutorialwork  公共的    视频  文档  音乐
sunny@sunny-VirtualBox:~$ pwd
/home/sunny
sunny@sunny-VirtualBox:~$ alias p='pwd'
sunny@sunny-VirtualBox:~$ alias l='ls'
sunny@sunny-VirtualBox:~$ alias pl='p;l'
sunny@sunny-VirtualBox:~$ pl
/home/sunny
Anaconda   backups   local    Repository    测试文件  模板  图片  下载	桌面
anaconda3  commands  pycharm  tutorialwork  公共的    视频  文档  音乐
```
>**想要了解的更多的话，那么就继续跟我进行下去吧。**

>**alias dir=“ls -al | grep ^d” ls -al用于获取当前目录下的所有文件和子目录列表，然后通过|管道将这个输出传递给过滤器grep，^d表示以d开头的文件夹，因此这个命令用来显示当前路径下的所有文件夹。利用别名来显示复杂命令，是不是相当方便呢，我相信你已经感受到他的魅力啦。**
```
sunny@sunny-VirtualBox:~$ alias dir='ls -al | grep ^d'
sunny@sunny-VirtualBox:~$ dir
drwxr-xr-x 34 sunny sunny  4096 9月  25 13:21 .
drwxr-xr-x  3 root  root   4096 7月  11 23:40 ..
drwxrwxr-x  2 sunny sunny  4096 8月  15 22:09 Anaconda
drwxrwxr-x 23 sunny sunny  4096 8月  15 22:19 anaconda3
```
##1.4 alias 永久化
>**你有没有发现，当你重启计算机的时候，这些别名已经不存在啦，这是alias的主要缺点。不过不用担心，我们可以通过一些设置去使alias永久化。
在我们的主目录下（/home/user）有一个.bashrc的文件，我们可以通过vim .bashrc去编辑这个文件，添加任何我们想要的别名，如：alias p=’pwd’，位于下方代码底部。**
```
sunny@sunny-VirtualBox:~$ cat .bashrc
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;

# setting alias
alias p='pwd'
```
## 1.5 去除别名
> **当我们不再需要某些别名的时候，我们可以通过unalias命令，去除掉我们不想要的别名。**
```
sunny@sunny-VirtualBox:~/Repository/linuxstudy$ p
/home/sunny/Repository/linuxstudy
sunny@sunny-VirtualBox:~/Repository/linuxstudy$ unalias p
sunny@sunny-VirtualBox:~/Repository/linuxstudy$ p
p：未找到命令
```
