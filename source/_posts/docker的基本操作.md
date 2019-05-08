
---
title: docker的基本操作
date: 2019-05-06 12:36:15
tags: 杂记
---


### docker的基本操作

流程

docker search  mongo  				搜索镜像

docker pull mongo					下载镜像

docker run -itd  --name=spider  py3_spider:v2      启动        

1   检查运行中的镜像

docker ps

2  运行docker镜像

docker run spider   echo "hello word"        

镜像名		命令

3  进入容器

docker exec -it 2c272247bca /bin/bash	

​    退出

Ctrl + d

4     终止和重新启动

docker  stop   name/id

docker   kill    name/id

启动    docker start name

5   文件复制

从主机复制到容器sudo docker cp host_path containerID:container_path

从容器复制到主机sudo docker cp containerID:container_path host_path

6  文件挂载

docker run -itd -v /home/xiaofei/scrapyd/:/xiaofei --name=spider1  REPOSITORY:v1

7  删除所有未运行的容器（已经运行的删除不了，未运行的就一起被删除了）

sudo docker rm $(sudo docker ps -a -q)

8 删除none的images
 
docker rmi $(docker images |grep "<none>”)

    