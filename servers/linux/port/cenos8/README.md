
####  一、查看端口
-   firewall-cmd --state          //查看防火墙状态
-   netstat -anp           //查询已开放的端口
-   netstat -nlp |grep :8083        //查看端口是否被占用
-   firewall-cmd --query-port=2345        //查询指定端口是否已开 
-   firewall-cmd --zone=public --list-ports    // 查看已开放的全部端口
-   firewall-cmd --zone=public --remove-port=2333/tcp --permanent      //关闭端口
-   firewall-cmd --reload           //端口重新载入

####  二、简单介绍systemctl命令的使用
-   systemctl list-unit-files --type service   //查看全部服务命令
-   systemctl status name.service       //查看服务命令
-   systemctl start name.service        //启动服务
-   systemctl stop name.service         //停止服务
-   systemctl restart name.service      //重启服务
-   systemctl enable name.service       //增加开机启动
-   systemctl disable name.service      //删除开机启动

-  添加端口进防火墙： firewall-cmd --zone=public --add-port=443/tcp --permanent
-  启动/重启/停止服务： systemctl start/restart/stop name.service
-  查看服务状态：  systemctl status name.service




    