####    
-   lsmod | grep bbr  查询是否安装bbr
-   bbr脚本：   wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
-   tcp脚本:    wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
-   tcp脚本2:   wget -N --no-check-certificate "https://github.com/ylx2016/Linux-NetSpeed/releases/download/sh/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

####    部署


####    tcp fast open
-    查询  sysctl -a | grep fastopen
-    验证是否net.ipv4.tcp_fastopen=3
-    不是则 echo net.ipv4.tcp_fastopen = 3 >> /etc/sysctl.conf
-    echo 3 > /proc/sys/net/ipv4/tcp_fastopen / 且添加 net.ipv4.tcp_fastopen = 3   后ssr/v2ray中可开启tcp加速
-    sysctl -p 保存生效





