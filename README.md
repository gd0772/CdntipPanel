# CloudPanel

This is a panel to manage all kinds of cloud accounts, such as az aws do, linode 这个面板不适合一点linux和docker基础都没有的童鞋

安装Docker

curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh && service docker start ＃如果docker没启动，可以运行这个

docker创建网络

docker network create cdntip_network

启动mysql容器

mkdir /data && docker run -d -it --network cdntip_network --restart=always -v /data/mysql:/var/lib/mysql --name panel_mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=panel mysql:5.7 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci # (更改mysqlroot密码，机器内部也需要修改database.conf文件的密码)

启动 cdntip/panel

docker run -d -it --network cdntip_network -p 8111:80 --name panel cdntip/panel (8111端口可改为任意，此处为实际对外端口)

进入容器

docker exec -it panel /bin/bash

创建管理员 python manage.py createsuperuser --username gd772 --email foeg3fsfe4ifa@wf38sf.com （创建用户）

fe39SI33##3Ss3zb83

添加aws镜像

python manage.py aws_update_images

更新程序

docker stop panel ＃停止当前容器
docker rm panel＃删除当前容器
docker pull cdntip/panel:latest # 拉取最新的镜像
docker run -d -it --network cdntip_network -p 8111:80 --name panel cdntip/panel:latest # 重新创建程序容器
