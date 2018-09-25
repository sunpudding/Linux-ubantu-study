# Ubuntu学习之apt-get命令
## apt-get语法
**apt-get [options] [-o config=string] [-c=cfgfile] command [pkg]**
>**apt-get是用于处理包的命令行工具,接下来让我们进一步的来了解这个强大的命令行工具吧。**
## apt-get -h / apt-get --help
>**apt-get -h 以及 apt-get --help作用是一样的，可查看apt-get帮助信息**
```
sunny@sunny-VirtualBox:~/Repository/linuxstudy$ apt-get -h
apt 1.2.27 (amd64)
用法： apt-get [选项] 命令
　　　 apt-get [选项] install|remove 软件包1 [软件包2 ...]
　　　 apt-get [选项] source 软件包1 [软件包2 ...]

apt-get 可以从认证软件源下载软件包及相关信息，以便安装和升级软件包，
或者用于移除软件包。在这些过程中，软件包依赖会被妥善处理。

常用命令：
  update - 取回更新的软件包列表信息
  upgrade - 进行一次升级
```
## apt-get update
>**通常apt-get在可用包的数据库上工作。如果不更新此数据库，系统将不知道是否有可用的更新包。所以这个命令将告诉我们是否有更新的数据包**

>**更新包数据库需要超级用户权限，所以我们需要使用sudo**

* **sudo apt-get update**
>**当我们运行这个命令时，我们可以看到从各种服务器上获取的检索信息**
```
sunny@sunny-VirtualBox:~/Repository/linuxstudy$ sudo apt-get update
hit:1 http://mirrors.aliyun.com/ubuntu xenial InRelease
hit:2 http://mirrors.aliyun.com/ubuntu xenial-updates InRelease
hit:3 http://mirrors.aliyun.com/ubuntu xenial-backports InRelease             
ign:4 https://packages.microsoft.com/repos/vscode stable InRelease
get:5 http://security.ubuntu.com/ubuntu xenial-security InRelease [107kB]         
```
>**在上面的代码的开头，你会看到三种数据类型，hit,get,ign。让我向你解释一下：**
>>**hit:包版本没有变化**

>>**get:有一个新版本可用。它将下载信息(而不是包本身)。你可以看到上面的截图中有“GET”行的下载信息。**

>>**ign:这个包被忽略了。这可能有各种原因。要么是包太新了，甚至不需要检查，要么是检索文件时出错了，但是错误很小，因此被忽略了。这不是错误。所以没有必要担心。**
## apt-get upgrade
>**一旦更新了包数据库，就可以升级已安装的包。最方便的方法是升级所有更新可用的软件包。为此，我们可以使用下面的命令：**
* **sudo apt-get upgrade**
```
sunny@sunny-VirtualBox:~/Repository/linuxstudy$ sudo apt-get upgrade
正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
正在计算更新... 完成
下列软件包的版本将保持不变：
  libegl1-mesa libgbm1 libgl1-mesa-dri libwayland-egl1-mesa libxatracker2 linux-generic-hwe-16.04
  linux-headers-generic-hwe-16.04 linux-image-generic-hwe-16.04
```
>**若只升级特定程序，请使用以下命令：**

* **sudo apt-get upgrade <package_name>**

>**还有一种方法可以通过使用下面的命令来提供完整的升级：**

* **sudo apt-get dist-upgrade**
> **命令apt-get upgrade非常听话。它从不尝试删除任何软件包或自行安装新软件包。**

> **然而，apt-get dist-upgrade 命令是主动的.它查找已安装的包的新版本的依赖项，并尝试安装新包和自行删除现有的包。看起来dist-upgrade非常智能强大，但是他有可能删除一些不太重要的包，这或许会为我们带来风险。**
##  apt-get update 和 apt-get upgrade的区别
>**apt-get update虽然看起来会更新包。但那不是真的。apt-get update只更新包的数据库。例如，如果安装了XYXPackageVersion1.3，在apt-get update之后，数据库将知道有一个较新的版本1.4可用。**

>**当我们在apt-get update之后进行apt-get upgrade时，它会对安装的软件包进行升级，而不是更新版本。**
## apt-get install
* **sudo apt-get install <package_name>**
>**在使用时只需将<Package_name>替换为所需的包即可。假设我想安装python，我所需要做的就是使用下面的命令：**

* **sudo apt-get install python**
## apt-get remove
* **sudo apt-get remove <package_name>**
>**当我们想要删除不再需要的安装包时，可以使用以上的命令**

>**除此之外还有另一种方法**
* **sudo apt-get purge <package_name>**
>**那么他们的区别是什么呢？**

>**apt-get remove只是删除包的二进制文件。它不接触配置文件**

>**apt-get purge删除与包相关的所有内容，包括配置文件。***

>**因此，如果我们已经“remove”了一个特定的软件，并再次安装它，我们的系统将有相同的配置文件。当然，当我们再次安装时，我们将被要求覆盖现有的配置文件。**

>**当我们扰乱了程序的配置时，purge是特别有用的。我们可以从系统中完全抹去它的痕迹，或许可以重新开始。**
## apt-get clean
>**我们可以使用下面的命令来清除本地存储库中检索到的包文件**
* **sudo apt-get clean**
## apt-get autoclean
>**另一种方法是使用自动清洗。与上面的清洁命令不同,删除已下载的旧包文件**
* **sudo apt-get autoclean**
>**另一种释放磁盘空间的方法是使用autoremove。它删除已安装包的有依赖关系的自动安装的库和包。如果程序包被删除，这些自动安装的包在系统中就是无用的。此命令删除此类包。**

* **sudo apt-get autoremove**
## apt-get sourse
* **sudo apt-get source <package_name>**
>**下载源码包文件**
## apt-get download
* **sudo apt-get download <package_name>**
>**下载指定的二进制包到当前目录**
