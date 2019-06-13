- tail -f 100 filename 显示文件的最后一百行

  tail -r -n 10 filename 逆序显示文件的最后10行

- sed可以直接替换文件中的内容
  sed -i 's/原字符串/新字符串/' /home/1.txt
  sed -i 's/原字符串/新字符串/g' /home/1.txt

- echo \`date\`   注意： 这里使用的是反引号 `, 而不是单引号 '。结果将显示当前日期 Thu Jul 24 10:08:46 CST 2014

- systemctl set-default multi-user.target用命令行页面

- 获取外网地址 curl getip.name

- df -hl 查看磁盘空间

- sed -i 's/\r$//' portainer.sh #win下结尾是\n\r 在linux下是\r 因此需要改下才可以在linux下执行

- 跟tail功能类似
  	cat 从第一行開始显示档案内容。
  	tac 从最后一行開始显示档案内容。
  	more 分页显示档案内容。
  	less 与 more 相似，但支持向前翻页
  	head 仅仅显示前面几行
  	tail 仅仅显示后面几行
  	n 带行号显示档案内容
  	od 以二进制方式显示档案内容

- mkdir -p 文件路径 不存在会自己创建

- 删除任何.log文件；删除前逐一询问确认
  	rm -i *.log
  删除test子目录及子目录中所有档案删除,并且不用一一确认
  	rm -rf test
  删除以-f开头的文件
  	rm -- -f*
- 将文件file1改名为file2，如果file2已经存在，则询问是否覆盖
  	mv -i log1.txt log2.txt



- export JAVA_HOME=/usr/local/java/jdk1.8.0_131
  export JRE_HOME=${JAVA_HOME}/jre
  export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib:$CLASSPATH
  export JAVA_PATH=${JAVA_HOME}/bin:${JRE_HOME}/bin
  export PATH=$PATH:${JAVA_PATH}