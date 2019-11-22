####    酸酸乳一键脚本
-   wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh

####    TCP一键加速脚本
-   wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

####    MTproxy代理一键脚本
-   wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/mtproxy_go.sh && chmod +x mtproxy_go.sh && bash mtproxy_go.sh

####    ipv6解析
~~~text
/etc/sysconfig/network-scripts/ifcfg-eth0
添加
---------------------------------------
DEVICE=eth0
ONBOOT=yes
BOOTPROTO=static
IPADDR=173.199.119.54
NETMASK=255.255.255.0
GATEWAY=173.199.119.1
DNS1=108.61.10.10

IPV6INIT=yes
IPV6ADDR="2001:19f0:5:6b70:5400:02ff:fe34:5eef/64"
IPV6_AUTOCONF="yes"
DNS2=2001:19f0:300:1704::6
-----------------------------------

/etc/sysconfig/network-scripts/route-eth0
添加
---------------------------------------
169.254.0.0/16 dev eth0
---------------------------------------
重启：
service network restart

~~~

-   centos8 修改 /etc/init.d/ssr   的python为python3