#####   安装依赖软件
-   yum install  gcc 

#####  下载解压redis
-   cd /usr/local
-   wget http://download.redis.io/releases/redis-6.0.5.tar.gz
-   tar -xzvf redis-6.0.5.tar.gz /usr/local/redis
-   cd redis
-   make MALLOC=libc   // 编译
-   cd src
-   make install  //安装
-   redis-cli -v    // 查看版本


####    配置redis 
-   进入/usr/local/redis/redis.conf  
-   port:6379       //默认端口
-   bind 0:0:0:0    //不限制外网ip访问
-   daemonize yes    //可在后台执行   
-   protected-mode  no        //解除保护 
-   requirepass  密码       //设置redis远程连接密码     
-   maxmemory 751619276       //最大内存：0.75G   单位byte
-   maxmemory-policy volatile-lru           //内存回收算法
~~~text
过期策略详解
volatile-lru -> 根据LRU算法生成的过期时间来删除。
allkeys-lru -> 根据LRU算法删除任何key。
volatile-random -> 根据过期设置来随机删除key。
allkeys->random -> 无差别随机删。
volatile-ttl -> 根据最近过期时间来删除（辅以TTL）
noeviction -> 谁也不删，直接在写操作时返回错误
~~~
-   /usr/local/bin/redis-server /usr/local/redis-6.0.5/redis.conf       //指定redis.conf文件启动


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
ExecStart=/usr/local/bin/redis-server /usr/local/redis-6.0.5/redis.conf
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


-   redis-cli 进入redis
-   auth "密码"
-   info memory   //查看内存
-   info clients  //查看连接数
-   CONFIG GET maxclients  //查看最大连接数
-   CLIENT LIST      //获取客户端列表

  
