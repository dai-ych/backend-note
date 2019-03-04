#####   安装依赖软件
-   yum install  gcc 

#####  下载解压redis
-   wget XXXX
-   tar -xzvf redis.tar.gz /usr/local/redis
-   cd redis
-   make MALLOC=libc   // 编译
-   cd src
-   make install  //安装
-   redis-cli -v    // 查看版本


####    配置redis 以后台进程方式启动  
-   默认port:6379
-   /usr/local/redis/redis.conf：    daemonize no   将值改为yes 保存退出                     
-   /usr/local/bin/redis-server /usr/local/redis/redis.conf       //指定redis.conf文件启动
-   设置redis远程连接：.因为redis默认设置允许本地连接，所以我们要将redis.conf中将bind 127.0.0.1 改为bind 0.0.0.0或者注释该行
-   requirepass   密码       //在redis.conf中搜索requirepass这一行，设置redis连接密码


####    查看进程
-   ps -ef|grep redis   /   ps -aux | grep redis


####    设置redis开机自启动
-   在/usr/lib/systemd/system目录下增加redis.service：
~~~text
#表示基础信息
[Unit]
#描述
Description=Redis
#在哪个服务之后启动
After=syslog.target network.target remote-fs.target nss-lookup.target

#表示服务信息
[Service]
Type=forking
#注意：需要和redis.conf配置文件中的信息一致
PIDFile=/var/run/redis_6379.pid
#启动服务的命令
#redis-server安装的路径 和 redis.conf配置文件的路径
ExecStart=/usr/local/bin/redis-server /usr/local/redis/redis.conf
#重新加载命令
ExecReload=/bin/kill -s HUP $MAINPID
#停止服务的命令
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

#安装相关信息
[Install]
#以哪种方式启动
WantedBy=multi-user.target
#multi-user.target表明当系统以多用户方式（默认的运行级别）启动时，这个服务需要被自动运行。
~~~
-   systemctl daemon-reload    //刷新配置
-   systemctl enable redis   //设置开机启动
-   systemctl is-enabled redis.service    //查看是否开机自启
-   systemctl start redis.service
-   firewall-cmd --zone=public --add-port=6379/tcp --permanent   开放端口
  
