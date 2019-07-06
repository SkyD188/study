## docker常用命令

#### 容器生命周期管理

```docker
run 
start/stop/restart 
kill 杀掉一个容器
rm
pause/unpause 暂停容器中所有的进程 以及 恢复容器中所有的进程。
create 创建一个新容器但是不启动
exec 进入容器
```

####  容器操作

```docker
ps （ps -a 查看所有容器）
inspect 获取容器/镜像的元数据。
top 查看容器中运行的进程信息，支持 ps 命令参数。
attach
events 从服务器获取实时事件
logs 日志
wait 阻塞运行直到容器停止，然后打印出它的退出代码。
export 将文件系统作为一个tar归档文件导出到STDOUT。
port 列出指定的容器的端口映射，或者查找将PRIVATE_PORT NAT到面向公众的端口。
cp 复制
```

#### 本地镜像操作

```docker
images
rmi
tag
build 构建镜像
history 查看指定镜像的创建历史。
save 将指定镜像保存成 tar 归档文件。
load 导入使用 docker save 命令导出的镜像。
import 从归档文件中创建镜像。
```

#### docker信息

````docker
info
version
search 搜索docker仓库里的镜像
login
loginout
````

#### docker 命令高级用法

```docker
docker stop $(docker ps -q)  停用全部运行中的容器:

docker rm $(docker ps -aq)   删除全部容器：

docker rm `docker ps -a -q`

docker rmi `docker images -q` 删除所有镜像

docker container update --restart=always 容器名字

docker cp docker的复制命令。可以容器复制到宿主机，也可以复制到容器
```

#### docker网络模式

```docker
网络模式：docker的默认网络模式是网桥模式
	host：docker会用宿主机的IP和端口，不会获得一个独立的network  namespace
	container：这个模式指定新创建的容器和已经存在的一个容器共享一个Network Namespace，而不是和宿主机共享
	none：这个模式有自己的独立的网络配置。但是不是docker提供的，需要自己手动配置
	bridge：docker会为容器创建一个网络配置，并将docker容器链接到一个虚拟网桥上
```

#### docker高级用法

```docker
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name_or_id可直接获得容器的ip地址如：172.18.0.4

显示所有容器IP地址：docker inspect --format='{{.Name}} - {{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $(docker ps -aq)

docker container update --restart=always 容器名字
```

