
-  添加端口进防火墙： firewall-cmd --zone=public --add-port=3306/tcp --permanent
-  启动/重启/停止服务： systemctl start/restart/stop name.service
-  查看服务状态：  systemctl status name.service


-  tomcat增加启动参数:
   tomcat 需要增加一个pid文件:
   在tomca/bin 目录下面，增加 setenv.sh 配置，catalina.sh启动的时候会调用，同时配置java内存参数。
```xml   
#add tomcat pid
CATALINA_PID="$CATALINA_BASE/tomcat.pid"
#add java opts
JAVA_OPTS="-server -XX:PermSize=256M -XX:MaxPermSize=1024m -Xms512M -Xmx1024M -XX:MaxNewSize=256m"
```
-   chmod a+x /opt/tomcat8/bin/setenv.sh    //修改文件权限变为可执行
####  创建tomcat账户来启动tomcat，并修改tomcat文件的属性
-   getent group tomcat || groupadd -r tomcat
-   getent passwd tomcat || useradd -r -d /opt -s /bin/nologin -g tomcat tomcat
-   chown -R tomcat:tomcat /opt/tomcat8
-  增加tomcat systemctl启动：
    在/usr/lib/systemd/system目录下增加tomcat.service：
```text
[Unit]
Description=Tomcat
After=syslog.target network.target remote-fs.target nss-lookup.target
[Service]
Type=forking
PIDFile=/opt/tomcat8/tomcat.pid
ExecStart=/opt/tomcat8/bin/startup.sh
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true
User=tomcat
Group=tomcat
[Install]
WantedBy=multi-user.target
```
-   systemctl daemon-reload    //刷新配置
-   systemctl enable tomcat   //设置开机启动
-   systemctl start tomcat.service     //启动如果报错
~~~text
Job for tomcat.service failed because the control process exited with error code. See "systemctl status tomcat.service" 
and "journalctl -xe" for details.  
~~~
-   在catlina.sh 最上面导入home: 
~~~text
export JAVA_HOME=/opt/jdk1.8  
export JRE_HOME=/opt/jdk1.8/jre
export JENKINS_HOME=/opt/tomcat8/webapps/jenkins
~~~

-   如果报错权限不足，即可先删除logs下所有root权限日志
-   如果还是报错，先：
~~~text
ps -ef |grep tomcat   //tomcat用户不能关闭root用户的进程
kill -9 [进程]    //先用root用户关闭root进程
chown -R tomcat:tomcat /opt/tomcat8
~~~

