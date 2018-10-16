# Ubuntu-commands-practice

* 利用 alias ，使得用户登录之后，可以使用 check-baidu 代替命令 "curl -vI https://www.baidu.com/"

>`alias check-baidu="curl -vI https://www.baidu.com/"`

* 使用 apt 搜索 bittorrent 客户端，然后安装一个。

>`apt-cache search bittorrent`

>`sudo apt-get install bittornado`

* 使用 awk 过滤出监听在 127.0.0.1 的所有端口。

>` ss -nlt |awk '{split($4,a,":");if(a[1]=="127.0.0.1"){print a[2]}}'`

* 根据 "/proc/cpuinfo" 文件，打印出 CPU 型号，及核数。

>`cat /proc/cpuinfo | grep "cpu cores" | uniq`

>`cat /proc/cpuinfo | grep "model name" |uniq`

* 修改目录 src 权限，使得只有用户 gom 可以进入，其他用户/组不能。

>`sudo chown gom src`

>`sudo chmod 700 src`

* 用 date 打印出当前时间，格式 "年/月/日 时:分:秒"。

>`date +"%Y/%m/%d %H:%M:%S"`

* 使用 df 找出使用率超过 10% 的磁盘分区

>`df | awk -F'[ %]+' '{if($5>10)print}'`

* 找出所有以 "SH" 开头的环境变量设置

>`env | grep '^SH'`

* 重命名 src/ 目录下的所有 .txt 文件, 改成 .md 文件

>`rename 's/.txt/.md/' *.txt`

* 监测内存使用率, 当使用率大于 80% 时, 播放警示音频 alert.mp3
>**由于本机的内存使用率较低，所以暂时将判定值定为30%**

>`free -m |grep "Mem" |awk '{a=($3/$2)*100;if(a>30){print "alert.mp3"}}' | xargs play`
