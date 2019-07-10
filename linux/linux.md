### LINUX

##### linux允许远程使用root账号

```shell
1.先用其他账号登录上去
2.sudo passwd root 为管理员设置密码
3.su 切换到管理员
4.vi /etc/ssh/sshd_config 进去ssh配置文件
5.复制 PermitRootLogin yes 加入到配置文件中
6.systemctl restart ssh 或者 service ssh restart 重启服务
```

##### 小技巧

```linux
遇到需要输入yes 或者 y 的命令，可以是用echo yes | rm -i aa.txt 
-i 以交互模式运行
ntsysv 看服务是否是开机启动
cat /var/log/messages 查看系统日志
cat /var/log/secure 用户登录日志
centos7 查看ip的几种方式 ip addr , ifconfig , hostname -I
yum list 插件名字（docker-ce）--showduplicates | sort -r 列出仓库所有的插件版本，并选择指定的安装并排序
yum update 更新centos版本
```

##### 定时任务

> [计算时间网站](https://tool.lu/crontab/)

```shell
crontab -e 创建执行定时任务的命令
crontab -l 列出有哪些任务在执行
cat /etc/crontab 查看官方指导的说明

# 买那个了使用如下  eg：* * * * * /usr/local/dhy.sh
# .---------------- minute (0 - 59)
# | .------------- hour (0 - 23)
# | | .---------- day of month (1 - 31)
# | | | .------- month (1 - 12) OR jan,feb,mar,apr ... 月份的缩写
# | | | | .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat 日期缩写
# | | | | | 空一格
# * * * * * user-name command to be executed 用户要执行的文件位置或者是命令
```

##### 系统级别命令

> **systemctl是CentOS7的服务管理工具中主要的工具，它融合之前service和chkconfig的功能于一体。**

```shell
服务命令：systemctl command name.service
服务启动：service name start –> systemctl start name.service
服务停止：service name stop –> systemctl stop name.service
服务重启：service name restart –> systemctl restart name.service
服务状态：service name status –> systemctl status name.service
服务开机启动：systemctl enable firewalld.service
服务开机禁用：systemctl disable firewalld.service
查看服务是否开机启动：systemctl is-enabled firewalld.service
查看已启动的服务列表：systemctl list-unit-files | grep enabled
查看启动失败的服务列表：systemctl --failed

条件式重启(已启动才重启，否则不做任何操作)
    systemctl try-restart name.service
重载或重启服务(先加载，然后再启动)
	systemctl reload-or-try-restart name.service
```

##### 防火墙命令

> **只需要看前三段即可，后面的命令基本用不着**
>
> **centos6的防火墙 iptables 命令一样，只需要把 firewalld 改为 iptables 即可**

```shell
防火墙基本命令（具体看系统级别命令即可）
 	启动： systemctl start firewalld
    查看状态： systemctl status firewalld 
    停止运行： systemctl stop firewalld
    
配置firewalld-cmd
    查看版本： firewall-cmd --version
    查看帮助： firewall-cmd --help
    显示状态： firewall-cmd --state
    查看所有打开的端口： firewall-cmd --zone=public --list-ports
    更新防火墙规则： firewall-cmd --reload
    更新防火墙规则，重启服务： firewall-cmd --completely-reload
    查看已激活的Zone信息:  firewall-cmd --get-active-zones
    查看指定接口所属区域： firewall-cmd --get-zone-of-interface=eth0
    拒绝所有包：firewall-cmd --panic-on
    取消拒绝状态： firewall-cmd --panic-off
    查看是否拒绝： firewall-cmd --query-panic
    
防火墙开启和关闭端口（以下都是指在public的zone下的操作，不同的Zone只要改变Zone后面的值就可以）
    添加：firewall-cmd --zone=public --add-port=80/tcp --permanent（--permanent永久生效，没有此参数重		   启后失效） 
    重新载入：firewall-cmd --reload
    查看：firewall-cmd --zone=public --query-port=80/tcp
    删除：firewall-cmd --zone=public --remove-port=80/tcp --permanent
 
 								下面命令基本用不着
 
防火墙信任级别 通过Zone的值指定
    drop: 丢弃所有进入的包，而不给出任何响应 
    block: 拒绝所有外部发起的连接，允许内部发起的连接 
    public: 允许指定的进入连接 
    external: 同上，对伪装的进入连接，一般用于路由转发 
    dmz: 允许受限制的进入连接 
    work: 允许受信任的计算机被限制的进入连接，类似 workgroup 
    home: 同上，类似 homegroup 
    internal: 同上，范围针对所有互联网用户 
    trusted: 信任所有连接
    	
防火墙管理服务
    以smtp服务为例， 添加到work zone
    添加：
    firewall-cmd --zone=work --add-service=smtp
    查看：
    firewall-cmd --zone=work --query-service=smtp
    删除：
    firewall-cmd --zone=work --remove-service=smtp
  
防火墙配置IP地址伪装
    查看：
    firewall-cmd --zone=external --query-masquerade
    打开：
    firewall-cmd --zone=external --add-masquerade
    关闭：
    firewall-cmd --zone=external --remove-masquerade
    
防火墙端口转发
    打开端口转发，首先需要打开IP地址伪装 firewall-cmd --zone=external --add-masquerade
    转发 tcp 22 端口至 3753： 
    firewall-cmd --zone=external --add-forward-port=22:porto=tcp:toport=3753
    转发端口数据至另一个IP的相同端口：
    firewall-cmd --zone=external --add-forward-port=22:porto=tcp:toaddr=192.168.1.112
    转发端口数据至另一个IP的 3753 端口：
    firewall-cmd --zone=external --add-forward-port=22:porto=tcp:toport=3753:toaddr=192.168.1.112
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

##### vi和vim

> vim是vi的升级版，不推荐用vi。

相比vi的优势

1. 多级撤消 （在vi编辑器中，按u只能撤消上次命令，而在vim里可以无限制的撤消）
2. 易用性 （ vi编辑器只能运行于unix中，而vim不仅可以运行于unix，还可用于windows、mac等多操作平台。）
3. 语法加亮 （vim用不同颜色加亮代码）
4.  对vi完全兼容 （完全可以把vim当作vi来用）

快捷键

```vim
1.正常 --> 插入模式
    i：在当前光标所在字符的前面，转为输入模式；
    a：在当前光标所在字符的后面，转为输入模式；
    o：在当前光标所在行的下方，新建一行，并转为输入模式；
    I：在当前光标所在行的行首，转为输入模式；
    A：在当前光标所在行的行尾，转为输入模式；
    O：在当前光标所在行的上方，新建一行，并转为输入模式；
    
2.退出
	在正常模式下按组合键shift zz可以保存并退出
	
3.移动光标（正常模式）
    1）逐字符移动：
        h: 左；
        l: 右；
        j: 下；
        k: 上；
        #h: 移动#个字符
    2）以单词为单位移动
        w: 移至下一个单词的词首；
        e: 跳至当前或下一个单词的词尾；
        b: 跳至当前或前一个单词的词首；
        #w: 移动#个单词
    3）行内跳转：
        0: 绝对行首；
        ^: 行首的第一个非空白字符；
        $: 绝对行尾
    4）行间跳转
        #G：跳转至第#行；
        gg: 第一行；
        G：最后一行
    5）末行模式
        .: 表示当前行；
        $: 最后一行；
        #：第#行；
        +#: 向下的#行
        
4、翻屏（正常模式）
        Ctrl+f: 向下翻一屏；
        Ctrl+b: 向上翻一屏；
        Ctrl+d: 向下翻半屏；
        Ctrl+u: 向上翻半屏
        
5、复制字符
    1）正常模式
    
        复制：
            yy：复制当前行
            nyy：复制当前行至下面的n行
        
        粘贴：
            p：粘贴到光标的后面
            P：粘贴到光标的前面
    2）可视模式

        复制：
            y：复制当前行
            ny：复制当前行至下面的n行

        粘贴：
            p：粘贴到光标的后面
            P：粘贴到光标的前面
            
6、删除字符（正常模式）
        x: 删除光标所在处的单个字符；
        #x: 删除光标所在处及向后的共#个字符；
        d$或D:从当前光标处删除至行尾；
        d^:从当前光标处删除之行首；
        dd: 删除当前光标所在行；
        #dd: 删除包括当前光标所在行在内的#行；
注：dd相当于剪切操作，如果你dd之后按p或者P可以进行粘贴。

7、替换字符
        r：替换单个字符（按完r在按你要替换的字符即可）
        R：替换多个字符（从你要替换的位置开始替换，直至你退出正常模式）
8、撤销编辑操作：u
        u：撤消前一次的编辑操作；
        #u：直接撤消最近#次编辑操作；
        温馨提示：连续u命令可撤消此前的n次编辑操作；
        
9、将另外一个文件（/path/sunhui.txt）的内容填充在当前文件夹中
        ：r   /path/sunhui.txt ：填充到当前文件所在光标的后面

10、修改vim配置文件
        vim   ~/.vimrc：修改当前用户的vim配置文件
        vim    /etc/vimrc：修改所有用户的vim配置文件
        例：在当前用户的vim配置文件中添加显示行数的命令
        vim    ~/.vimrc：在末行添加 set nu 即可
        
11、拓展（末行模式）
    1）显示或取消显示行号
        ：set    nu            //显示
        ：set    number    //显示
        ：set    nonu        //取消
    2）设置语法高亮
        ：syntax    on    //开启
        ：syntax    off    //关闭
    3）分屏
        ：vsp xxx.x    //将两个文件垂直分屏
        ：ctrl+w w   //切屏
注：该特性当前有效，如果想要永久有效需修改配置文件
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
    grep -C n "string" filename
   
递归搜索：-r 搜索当前目录以及子目录下含“this”的全部文件。
    grep -r "this" *

不匹配搜索：-v 显示不含搜索字符串“go”的行。
    grep -v "go" demo_text

统计匹配的行数：-c 统计文件中含“go”字符串的行数。
    grep -c "go" filename

只显示含有符串的文件的文件名：-l 显示含“this”字符串的文件的文件名。
    grep -l "this" filename

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

##### 管道

> **在内存中创建一个共享文件，从而使通信双方利用这个共享文件来传递信息。由于这种方式具有单向传递数据的特点，所以这个作为传递消息的共享文件就叫做“管道”。**

- 管道需要在内核和用户空间进行四次的数据拷贝：由用户空间的缓存中将数据拷贝到内核中 -> 内核将数据拷贝到内存中 -> 内存到内核 -> 内核到用户空间的缓存。**而共享内存则只拷贝两次数据：用户空间到内存 -> 内存到用户空间。**
- 管道用循环队列实现，连续传送数据可以不限大小。共享内存每次传递数据大小是固定的；
- 共享内存可以随机访问被映射文件的任意位置，管道只能顺序读写；
- 管道可以独立完成数据的传递和通知机制，共享内存需要借助其他通讯方式进行消息传递。

> **两者最大的区别：**
>
> **共享内存区是最快的可用IPC形式，一旦这样的内存区映射到共享它的进程的地址空间，这些进程间数据的传递，就不再通过执行任何进入内核的系统调用来传递彼此的数据，节省了时间。**

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





## **lsb_release -a  linux版本信息**

