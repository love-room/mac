# Docker

- ##### 获取镜像

  ```shell
  docker pull [source] [REPOSITORY] [:version]
  ```

- ##### 查看本地镜像

  ```shell
  docker images
  ```

- ##### 查看镜像详细信息

  ```shell
  docker inspect [imageId]
  ```

- ##### 搜索镜像

  ```shell
  docker search [REPOSITORY]
  ```

- ##### 删除镜像

  ```shell
  docker rmi [REPOSITORY]:[TAG]	`不加TAG默认latest`
  ```

- ##### 强制删除镜像

  ```shell
  docker rmi -f java
  ```

- ##### 镜像打标签

  ```shell
  docker tag [REPOSITORY]:[TAG] [REPOSITORY]:[TAG]	`不加TAG默认latest`
  ```

- ##### 创建镜像(基于容器创建)

  ```shell
  docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
  	-a, --author=“” 作者信息
  	-m, --message=“” 提交信息
  	-p, --pause=true 提交时暂停容器运行
  ```

- ##### 上传镜像

  ```shell
  docker push [REPOSITORY]
  ```

- ##### 创建容器

  ```shell
  docker create [-OPTIONS] [REPOSITORY][:TAG]
  ```

- ##### 启动容器

  ```shell
  docker start [-OPTIONS] [REPOSITORY]
  ```

- ##### 创建并运行容器

  ```shell
  docker run [-OPTIONS] java
  	-t, 让docker分配一个伪终端并绑定到容器的标准输入上
  	-i, 让容器的标准输入保持打开
  	-d, 后台运行
  	-p, 端口映射，5000:50000
  	-v, 文件挂载，/宿主机地址:/容器地址
  	--privileged=true, 获取宿主机所有权限
  	
  docker run -d -p 5000:5000 -v /Users/caojunming/registry/:/tmp/registry registry
  ```

- ##### 终止容器

  ```shell
  docker stop [containerId]
  ```

- ##### 重启容器

  ```shell
  docker restart [containerId]
  ```

- ##### 删除容器

  ```shell
  docker rm [containerId]
  ```

- ##### 退出容器控制台

  ```shell
  exit / Ctrl + D
  ```

- ##### 查看容器

  ```shell
  docker ps [-OPTIONS]
  	-a, 查看所有容器(包括已停止的)
  ```

- ##### 进入容器(attach)

  ```shell
  docker attach [containerName]
  ```

- ##### 进入容器(exec)

  ```shell
  docker exec [-OPTIONS] [containerId] /bin/bash
  ```

- ##### 删除Docker<None>镜像

  ```shell
  docker rmi $(docker images -f "dangling=true" -q)
  docker image prune
  ```






# Docker-machine

- ##### 创建本地主机实例

  ```shell
  docker-machine create -d xhyve --xhyve-boot2docker-url /Users/caojunming/.docker/machine/cache/boot2docker.iso edwin
  ```

- ##### 登录目标主机

  ```shell
  docker-machine ssh edwin
  ```

- ##### 显示连接到某个主机需要的环境变量

  ```shell
  docker-machine env edwin
  ```

- ##### 初始化集群

  ```shell
  docker swarm init
  ```

- ##### 查看加入集群命令

  ```shell
  docker swarm join-token worker
  ```

- ##### 查看集群

  ```shell
  docker node ls
  ```

- ##### 取消集群

  ```shell
  docker swarm leave --force
  ```

- ##### 创建服务

  ```shell
  docker service create --replicas 3 -p 80:80 --name nginx nginx:1.13.7-alpine
  ```

- ##### 查看全部服务

  ```shell
  docker service ls
  ```

- ##### 查看服务详情

  ```shell
  docker service ps tomcat
  ```

- ##### 查看服务日志

  ```shell
  docker service logs tomcat
  ```

- ##### 删除服务

  ```shell
  docker service rm tomcat
  ```

- ##### 






# Dockerfile

- #### FROM：指定基础镜像

  ```dockerfile
  #空镜像
  FROM scratch
  ```


- #### RUN：执行命令

  - ##### shell格式

    ```dockerfile
    #RUN <shell命令>
    RUN echo '<h1>Hello, Docker!</h1>' > /usr/share/nginx/html/index.html
    ```

  - ##### exec格式

    ```dockerfile
    #RUN ["可执行文件", "参数1", "参数2"]
    RUN ["sh", "c", "java -jar app.jar"]
    ```

  ```dockerfile
  FROM debian:jessie

  RUN buildDeps='gcc libc6-dev make' \
      && apt-get update \
      && apt-get install -y $buildDeps \
      && wget -O redis.tar.gz "http://download.redis.io/releases/redis-3.2.5.tar.gz" \
      && mkdir -p /usr/src/redis \
      && tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1 \
      && make -C /usr/src/redis \
      && make -C /usr/src/redis install \
      && rm -rf /var/lib/apt/lists/* \
      && rm redis.tar.gz \
      && rm -r /usr/src/redis \
      && apt-get purge -y --auto-remove $buildDeps
  ```

- #### COPY：复制文件

  - ##### shell格式

    ```dockerfile
    #COPY <源路径[宿主机]> <目标路径[容器]>
    COPY xxx.jar /usr/src/app/
    ```

  - ##### exec格式

    ```dockerfile
    #COPY ["<源路径1>",... "<目标路径>"]
    ```

- #### ADD：自动解压的复制文件

- #### CMD：容器启动命令

  - ##### shell格式

    ```dockerfile
    #CMD <shell命令>
    CMD echo $HOME
    ```

  - ##### exec格式

    ```dockerfile
    #CMD ["可执行文件", "参数1", "参数2"...]
    CMD ["sh", "-c", "echo $HOME"]
    ```

- #### 