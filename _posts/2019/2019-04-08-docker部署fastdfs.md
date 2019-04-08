# docker部署fastdfs
# 拉取fastdfs
docker image pull delron/fastdfs

# 运行tracker
docker run -dti --network=host --name tracker -v /var/fdfs/tracker:/var/fdfs delron/fastdfs tracker

我们将fastDFS tracker运行目录映射到本机的 /var/fdfs/tracker目录中。

# 运行storage
docker run -dti --network=host --name storage -e TRACKER_SERVER=192.168.3.42:22122 -v /var/fdfs/storage:/var/fdfs delron/fastdfs storage
docker run -dti --network=host --name storage -e TRACKER_SERVER=47.92.123.226:22122 -v /var/fdfs/storage:/var/fdfs delron/fastdfs storage

TRACKER_SERVER=192.168.3.42:22122 中的ip地址为fastdfs服务运行主机的ip，如果是本机ip地址不要使用127.0.0.1
我们将fastDFS storage运行目录映射到本机的/var/fdfs/storage目录中

# 更改端口（可选）（默认的端口为8888）
## 进入容器
docker exec -it storage  /bin/bash

## 修改storage服务的http端口为91
vi /etc/fdfs/storage.conf

**/etc/fdf目录下包含很多配置文件**

## 修改Nginx监听的端口为91
vi /usr/local/nginx/conf/nginx.conf

## 重启storage
docker restart storage 