### LINUX

##### 小技巧
```linux
遇到需要输入yes 或者 y 的命令，可以是用echo yes | rm -i aa.txt 
-i以交互模式运行
ntsysv 看服务是否是开机启动
cat /var/log/messages 查看系统日志
cat /var/log/secure 用户登录日志
centos7 查看ip的几种方式 ip addr , ifconfig , hostname -I
```

##### 定时任务

```shell
crontab -e 创建执行定时任务的命令
crontab -l 列出有哪些任务在执行
```

##### 系统级别命令

```shell
命令：systemctl command name.service
启动：service name start –> systemctl start name.service
停止：service name stop –> systemctl stop name.service
重启：service name restart –> systemctl restart name.service
状态：service name status –> systemctl status name.service

条件式重启(已启动才重启，否则不做任何操作)
    systemctl try-restart name.service
重载或重启服务(先加载，然后再启动)
	systemctl reload-or-try-restart name.service
```



##### 防火墙命令

```shell

```



##### tail cat mv

```shell
tail -f 100 filename 显示文件的最后一百行
tail -r -n 10 filename 逆序显示文件的最后10行

跟tail功能类似
cat 从第一行开始显示档案内容。
  	tac 从最后一行開始显示档案内容。
  	more 分页显示档案内容。
  	less 与 more 相似，但支持向前翻页
  	head 仅仅显示前面几行
  	tail 仅仅显示后面几行
  	n 带行号显示档案内容
  	od 以二进制方式显示档案内容
  	
删除任何.log文件；删除前逐一询问确认
	rm -i *.log
删除test子目录及子目录中所有档案删除,并且不用一一确认
	rm -rf test
删除以-f开头的文件
	rm -- -f*
将文件file1改名为file2，如果file2已经存在，则询问是否覆盖
	mv -i log1.txt log2.txt
```

##### 三剑客

> grep 更适合单纯的查找或匹配文本
>
> sed  更适合编辑匹配到的文本
>
> awk  更适合格式化文本，对文本进行较复杂格式处理

- sed

 ```shell
sed可以直接替换文件中的内容
sed -i 's/原字符串/新字符串/' /home/1.txt
sed -i 's/原字符串/新字符串/g' /home/1.txt
sed -i 's/\r$//' portainer.sh #win下结尾是\n\r 在linux下是\r 因此需要改下才可以在linux下执行
 ```

- awk

``` linux
awk 'NR==2{print $2'} NR指定第几行 $指定第几列 NF字段的数量（一行字段数量）length($n)打印出行的字数的个数

AWK 包含两种特殊的模式：BEGIN 和 END。
BEGIN 模式指定了处理文本之前需要执行的操作：
END 模式指定了处理完所有行之后所需要执行的操作：

$NF表示最后一个字段 NF表示被分隔符切开后有多少个字段
```

- grep

```linux
单个文件搜索字符串
	grep "literal-string" filename

-A 显示匹配行之后的n行
    grep -A n "string" filename

-B 显示匹配行之前的n行
    grep -B n "string" filename
    
-C 显示匹配行前后的n行
    $ grep -C n "string" filename
   
递归搜索：-r 搜索当前目录以及子目录下含“this”的全部文件。
    $ grep -r "this" *

不匹配搜索：-v 显示不含搜索字符串“go”的行。
    $ grep -v "go" demo_text

统计匹配的行数：-c 统计文件中含“go”字符串的行数。
    $ grep -c "go" filename

只显示含有符串的文件的文件名：-l 显示含“this”字符串的文件的文件名。
    $ grep -l "this" filename

输出时显示行号：-n 显示含文件中含“this”字符串的行的行号。
    grep -n "this" filename
```

##### java环境变量

```shell
export JAVA_HOME=/usr/local/java/jdk1.8.0_131
export JRE_HOME={JAVA_HOME}/lib:CLASSPATH
export JAVA_PATH={JRE_HOME}/bin
export PATH=​{JAVA_PATH}
```

##### 时间转换

```shell
D1=$(date -d now +%s)
......
D2=$(date -d now +%s)
timex=$(($D2-$D1))
打印两个时间相差的时间戳

date +%s   可以得到UNIX的时间戳;
日期时间与时间戳互转：
date -d "2015-08-04 00:00:00" +%s     输出：1438617600

时间戳转换为字符串：
date -d @1438617600  "+%Y-%m-%d"    输出：2015-08-04

如果需要得到指定日期的前后几天：
seconds=`date -d "2015-08-04 00:00:00" +%s`       #得到时间戳
seconds_new=`expr $seconds + 86400`                   #加上一天的秒数86400
date_new=`date -d @$seconds_new "+%Y-%m-%d"`   #获得指定日前加上一天的日前
```

##### 图形和命令界面启动

```shell
1、命令启动
systemctl set-default multi-user.target

2、图形界面模式
systemctl set-default graphical.target
```

##### 磁盘和内存

```shell
df -hl 查看磁盘空间

free -m以M的方式显示，同理-g就是以G的方式显示
```

##### 服务

```shell
chkconfig --list查看所有的服务
chkconfig和service命令的区别
chkconfig是当前不生效，Linux重启之后才生效的命令(开机自启动项)
service是即使生效，重启后失效的命令

find / -name "filename" 查找功能（不要引号也可以）

获取外网地址 curl getip.name

top -n 1代表运行一次就停止，不再刷新，-n运行 数字代表运行多少次
```



## cat /etc/redhat-release 红帽版本看发行版





## **lsb_release -a 版本信息 linux**

