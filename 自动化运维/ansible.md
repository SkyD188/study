## ansible

> 可以实现在一台服务器上操控所有子节点服务器，可以发送文件，执行命令。。。非常强大

- 安装ansible

```ansible
#Ansible仓库默认不在yum仓库中，因此我们需要使用下面的命令启用epel仓库。
	rpm -iUvh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
#yum下载
	yum install -y ansible
#查看ansible版本
	ansible --version
```

- ansible添加子节点（控制节点，使用ssh来控制的）

```ansible
#添加子节点服务器
	vim /etc/ansible/hosts
	添加如下内容
	
	#########################################
	#   [dhy-test] #随便写，但是要记得        #
	#   192.168.38.131 #需要维护的IP         #
	#   192.168.33.111 #需要维护的IP         # 
	#########################################
	
#在主服务器上生成ssh（一直点回车即可，然后输入主节点密码）
	ssh-keygen
#复制公钥到子节点（有多少字节点就复制多少）
	ssh-copy-id -i root@192.168.38.131
	ssh-copy-id -i root@192.168.33.111
#ping检测下是否成功（显示成功代表连接成功）
	ansible -m ping dhy-test
```

- ansible命令

> -m代表需要执行的模块

```ansible
#将本地文件复制到远程服务器
	ansible dhy-test -m copy -a "src=/root/dhy dest=/usr/local/docker/ owner=root group=root mode=0644"
#显示远程主机的详细命令
	ansible dhy-test -m setup
#列出主机清单 all可以改为管理名字
	ansible all --list-hosts
```

- 总结

> ansible模块多达2000个，用到哪些学那些。ansible-doc ping 可以查看ping模块的帮助，其他模块同理
>
> playbook可以编写很多有用的东西，用到在上网看看