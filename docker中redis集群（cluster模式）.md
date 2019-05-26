<center><h1>docker中redis集群（cluster模式）<h1/><center/>

### docker-compose.yml

```docker
version: '3'
services:
 redis1:
  image: publicisworldwide/redis-cluster
  network_mode: host
  restart: always
  volumes:
   - /data/redis/6180/data:/data
  environment:
   - REDIS_PORT=6180

 redis2:
  image: publicisworldwide/redis-cluster
  network_mode: host
  restart: always
  volumes:
   - /data/redis/6181/data:/data
  environment:
   - REDIS_PORT=6181

 redis3:
  image: publicisworldwide/redis-cluster
  network_mode: host
  restart: always
  volumes:
   - /data/redis/6182/data:/data
  environment:
   - REDIS_PORT=6182

 redis4:
  image: publicisworldwide/redis-cluster
  network_mode: host
  restart: always
  volumes:
   - /data/redis/6183/data:/data
  environment:
   - REDIS_PORT=6183

 redis5:
  image: publicisworldwide/redis-cluster
  network_mode: host
  restart: always
  volumes:
   - /data/redis/6184/data:/data
  environment:
   - REDIS_PORT=6184

 redis6:
  image: publicisworldwide/redis-cluster
  network_mode: host
  restart: always
  volumes:
   - /data/redis/6185/data:/data
  environment:
   - REDIS_PORT=6185
```

### 启动集群命令

```docker
docker run --rm -it inem0o/redis-trib create --replicas 1 192.168.38.131:6180 192.168.38.131:6181 192.168.38.131:6182 192.168.38.131:6183 192.168.38.131:6184 192.168.38.131:6185
```

