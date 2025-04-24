下载镜像
  检索 ：docker search xxxx
  下载 ：docker pull xxx:xxx
  列表 ：docker images
  删除 ：docker rmi xxx:xxx、
----------------------------------------------------------------
运行容器
  运行 ：docker run       -d -i -t --name -p
  查看 ：docker ps
  停止 ：docker stop
  启动 ：docker start
  重启 ：docker restart
  状态 ：docker stats
  日志 ：docker logs
  进入 ：docker exec
  删除 ：docker rm
----------------------------------------------------------------
分享
  提交 ：docker commit
  保存 ：docker save
  加载 ：docker load
  登录 ：docker login
  改名 ：docker tag
  推送 ：docker push
----------------------------------------------------------------
存储
  1.目录挂载 （没有/app/nghtll会自动创建, -v可以多个？）
    docker run -d -p 80:80 -v /app/nghtll:/usr/share/nginx/html
  2.卷映射
    -v ngcpnf:/etc/ngix
    注：卷的位置/var/lib/docker/volumes/ngcpnf
    docker volume
----------------------------------------------------------------
网络
  容器内部访问 默认网络docker0
    docker container inspect
  自定义网络（域名）
    docker network create mynet
    docker run -d-p --name --network mynet 
    容器名访问 http：//容器名