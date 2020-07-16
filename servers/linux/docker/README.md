####    


####    安装使用Mysql
-   修改mysql配置
-   docker inspect 容器id  查看容器所在的物理路径
-   找到MergedDir 下路径，进入 diff/etc/mysql 后修改 my.cnf
-   保存后重启mysql

-   进入容器：docker exec -it mysql8.0 bash


####    安装使用jenkins
-   1.安装
-   2.  docker pull jenkins/jenkins:lts;        拉取最新版镜像
-   3.  docker images;                          查看已经安装的jenkins镜像      



####    进入容器
-   docker exec -it jenkins /bin/bash
-   apt-get update && apt-get install vim   容器内安装vim


####    基本操作



####    基础工具包
