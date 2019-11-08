####    
-   lsmod | grep bbr  查询是否安装bbr
-   bbr脚本：   wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh

####    部署


####    tcp fast open
-    查询  sysctl -a | grep fastopen
-    验证是否net.ipv4.tcp_fastopen=3
-    不是则 echo net.ipv4.tcp_fastopen = 3 >> /etc/sysctl.conf
-    echo 3 > /proc/sys/net/ipv4/tcp_fastopen / 且添加 net.ipv4.tcp_fastopen = 3   后ssr/v2ray中可开启tcp加速
-    sysctl -p 保存生效





