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
  ```

  ​

