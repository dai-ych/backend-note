####    环境安装
-   yum install gcc gcc-c++
-   yum install gcc gcc-c++ autoconf automake
-   yum install -y pcre pcre-devel
-   yum install -y zlib zlib-devel
-   yum install -y openssl openssl-devel
-   或者 dnf group install "Development Tools"  安装开发工具包
-   dnf groupinfo "Development Tools"  查看工具包列表
-   dnf group remove "Development Tools"  去除工具包

####    nginx下载
-   https://nginx.org/en/download.html       //下载页
-   wget https://nginx.org/download/nginx-1.19.1.tar.gz -P /opt
-   tar -xzvf 解压
-   openssl version -a  查看openssl版本

####    配置
-   未指定路径时默认安装在/usr/local/nginx
-   ./configure --prefix=/usr/local/nginx                           \
                --pid-path=/usr/local/nginx/nginx.pid               \
                --with-http_ssl_module                              \
                --with-http_gzip_static_module                      \
                --with-http_stub_status_module                      \
                --with-pcre                                         \
                --with-http_realip_module                           \
                --with-http_flv_module                              \
                --with-http_mp4_module                              \
                --with-http_secure_link_module                      \
                --with-http_v2_module                             
```text
nginx path prefix: "/usr/local/nginx"
nginx binary file: "/usr/local/nginx/sbin/nginx"
nginx modules path: "/usr/local/nginx/modules"
nginx configuration prefix: "/usr/local/nginx/conf"
nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
nginx pid file: "/usr/local/nginx/logs/nginx.pid"
nginx error log file: "/usr/local/nginx/logs/error.log"
nginx http access log file: "/usr/local/nginx/logs/access.log"
nginx http client request body temporary files: "client_body_temp"
nginx http proxy temporary files: "proxy_temp"
nginx http fastcgi temporary files: "fastcgi_temp"
nginx http uwsgi temporary files: "uwsgi_temp"
nginx http scgi temporary files: "scgi_temp"
```
-   make && make install      编译安装
-   cd /usr/local/nginx/sbin/     启动停止nginx
-   ./nginx 
-   ./nginx -s stop         此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程。
-   ./nginx -s quit         此方式停止步骤是待nginx进程处理任务完毕进行停止。
-   ./nginx -s reload
-   重新加载配置文件
```text
当 ngin x的配置文件 nginx.conf 修改后，要想让配置生效需要重启 nginx，使用-s reload不用先停止
 ngin x再启动 nginx 即可将配置信息在 nginx 中生效，如下：
./nginx -s reload

开机自启动
即在rc.local增加启动代码就可以了。

vi /etc/rc.local
增加一行 /usr/local/nginx/sbin/nginx
设置执行权限：

chmod 755 rc.local

```


####  增加nginx systemctl启动：
-   touch /usr/lib/systemd/system/nginx.service
-   chmod 777 /usr/lib/systemd/system/nginx.service 
-   systemctl daemon-reload
-   nginx -t -c /usr/local/nginx/conf/nginx.conf   检验配置文件

```text
[Unit]
Description=nginx 
Documentation=http://nginx.org/en/docs/
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/usr/local/nginx/logs/nginx.pid
ExecStartPre=/usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf
ExecStart=/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
ExecStartPost=/bin/sleep 0.5
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s stop
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```           


####    验证nginx配置文件是否正确
-   进入nginx安装目录sbin下，输入命令./nginx -t
-   ps -ef|grep nginx    查看进程


####    nginx.conf
~~~text
server
        {
        listen       80;
        server_name  jenkins.vpeve.com;
        #root        /opt/tomcat8/webapps/jenkins;
        location / {
            rewrite ^/(.*)$ http://jenkins.vpeve.com/jenkins;
        }
        location /jenkins {
            proxy_pass http://localhost:8888/jenkins;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_redirect off;

        }
    }

https配置：
切换到源码包：
cd /opt//nginx-1.15.3
查看nginx原有的模块
/usr/local/nginx/sbin/nginx -V
在configure arguments:后面显示的原有的configure参数如下：
--prefix=/usr/local/nginx --with-http_stub_status_module
那么我们的新配置信息就应该这样写：
./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module
配置完成后，运行命令
make
这里不要进行make install，否则就是覆盖安装
然后备份原有已安装好的nginx
cp /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx.bak
然后将刚刚编译好的nginx覆盖掉原有的nginx（这个时候nginx要停止状态）
cp ./objs/nginx /usr/local/nginx/sbin/
然后启动nginx，仍可以通过命令查看是否已经加入成功
/usr/local/nginx/sbin/nginx -V
~~~


--//查询nginx主进程号
  $ ps -ef | grep nginx
  
  //从容停止Nginx：
  $kill -QUIT 主进程号
  
  //快速停止Nginx：
  kill -TERM 主进程号
  
  //强制停止Nginx：
  pkill -9 nginx


####    docker 安装
-   docker pull nginx:latest
-   docker run --name nginx -p 80:80 -d nginx    默认后台运行
-   docker exec -it nginx bash       进入容器
-   /etc/nginx                  配置目录
-   /usr/share/nginx/html       默认首页
-   /var/log/nginx              默认日志文件