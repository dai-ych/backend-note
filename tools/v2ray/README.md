####    
-   https://www.v2ray.com     官网（附带基础教程）
-   https://steemit.com/@v2ray      博客
-   bash <(curl -L -s https://install.direct/go.sh)    官方安装脚本
-   https://github.com/v2ray/v2ray-core/releases      客户端下载
-   bash <(curl -s -L https://git.io/v2ray.sh)        一键脚本

-   /usr/bin/v2ray/v2ray：V2Ray 程序；
-   /usr/bin/v2ray/v2ctl：V2Ray 工具；
-   /etc/v2ray/config.json：配置文件；
-   /usr/bin/v2ray/geoip.dat：IP 数据文件
-   /usr/bin/v2ray/geosite.dat：域名数据文件

-   journalctl -u v2ray    查看退出时的日志
-   v2ray -config=<config-file> -test  查看错误信息
####    部署
-   1.调整服务器时区和客户端时区相同   timedatectl set-timezone Asia/Shanghai
-   2.

