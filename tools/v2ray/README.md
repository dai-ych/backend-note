####    
-   https://www.v2ray.com     官网（附带基础教程）
-   https://steemit.com/@v2ray      博客
-   bash <(curl -L -s https://install.direct/go.sh)    官方安装脚本
-   https://github.com/v2ray/v2ray-core/releases      客户端下载
-   bash <(curl -s -L https://git.io/v2ray.sh)        一键脚本
-   可视化界面一键脚本V2ray.Fun  wget -N --no-check-certificate https://raw.githubusercontent.com/FunctionClub/V2ray.Fun/master/install.sh && bash install.sh  
-   V2rayN Windows可视化客户端：https://github.com/2dust/v2rayN/releases
-   journalctl -u v2ray    查看退出时的日志
-   v2ray -config=<config-file> -test  查看错误信息
####    部署
-   1. date -R 查询时间
-   2. 调整服务器时区和客户端时区相同   timedatectl set-timezone Asia/Shanghai
-   3.  PORT:16326
        UUID:5a0d19d4-531b-4059-bee9-b4b612e81746
-   4. /usr/bin/v2ray/v2ray：V2Ray 程序；
-      /usr/bin/v2ray/v2ctl：V2Ray 工具；
-      /etc/v2ray/config.json：配置文件；
-      /usr/bin/v2ray/geoip.dat：IP 数据文件
-      /usr/bin/v2ray/geosite.dat：域名数据文件
-   5：启动服务：systemctl start v2ray
-   6：检查配置：/usr/bin/v2ray/v2ray -test -config /etc/v2ray/config.json



####    配置案例
~~~~text
{
    "log": {
        "access": "/opt/v2ray/info.log",
        "error": "/opt/v2ray/warn.log",
        "loglevel": "warning"
    },
    "inbounds": [
        {
            "port": 23049,
            "protocol": "vmess",
            "settings": {
                "clients": [
                    {
                        "id": "8a0b0538-b180-4055-8a73-7aa29147c549",
                        "level": 1,
                        "alterId": 64
                    }
                ]
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "freedom",
            "settings": {
                "streamSettings": {
                    "network": "tcp",
                    "security": "none",
                    "tlsSettings": {
                        
                    },
                    "tcpSettings": {
                        
                    },
                    "kcpSettings": {
                        
                    },
                    "wsSettings": {
                        
                    },
                    "httpSettings": {
                        
                    },
                    "dsSettings": {
                        
                    },
                    "quicSettings": {
                        
                    },
                    "sockopt": {
                        "mark": 0,
                        "tcpFastOpen": true,
                        "tproxy": "off"
                    }
                }
            }
        },
        {
            "protocol": "blackhole",
            "settings": {
                
            },
            "tag": "blocked"
        }
    ],
    "routing": {
        "rules": [
            {
                "type": "field",
                "ip": [
                    "geoip:private"
                ],
                "outboundTag": "blocked"
            }
        ]
    }
}


~~~~