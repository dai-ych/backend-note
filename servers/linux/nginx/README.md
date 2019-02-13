####    环境安装
-   yum install gcc-c++
-   yum install -y pcre pcre-devel
-   yum install -y zlib zlib-devel
-   yum install -y openssl openssl-devel

####    nginx下载
-   https://nginx.org/en/download.html


####    配置
-   ./configure
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
-   make        编译安装
-   make install
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


####  增加tomcat systemctl启动：
-    在/usr/lib/systemd/system目录下增加nginx.service：
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
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s stop
ExecQuit=/usr/local/nginx/sbin/nginx -s quit
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```
-   chmod 755 nginx.service 
-   systemctl daemon-reload