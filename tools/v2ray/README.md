####    
-   https://www.v2ray.com     官网（附带基础教程）
-   https://steemit.com/@v2ray      博客
-   bash <(curl -L -s https://install.direct/go.sh)    官方安装脚本
-   https://github.com/v2ray/v2ray-core/releases      客户端下载
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
-   7：使用此命令生成 MTProto 代理所需要的用户密钥：openssl rand -hex 16



####    第三方脚本
-   地址：https://github.com/Jrohy/multi-v2ray   有TFO
-   安装命令：source <(curl -sL https://multi.netlify.com/v2ray.sh) --zh

-   地址：https://github.com/233boy   无TFO
-   命令：bash <(curl -s -L https://git.io/v2ray.sh)

-   地址：https://github.com/wulabing/V2Ray_ws-tls_bash_onekey 
-   命令：wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install.sh" && chmod +x install.sh && bash install.sh


####    配置案例
~~~~text
{
  "log": {
    "access": "/opt/v2ray/info.log",
    "error": "/opt/v2ray/warn.log",
    "loglevel": "warning"
				     },
  "inbounds": [{
    "port": 23049,
    "protocol": "vmess",
    "settings": {
      "clients": [
        {
          "id": "8a0b0538-b180-4055-8a73-7aa29147c549",
          "level": 1,
          "alterId": 128
        }
      ]
    },
    "streamSettings": {
      "network": "tcp",
      "security": "none",
      "sockopt": {
	      "mark": 0,
          "tcpFastOpen": true,
	      "tproxy": "off"
      }
    }
  },
    {
    "port":  8000,
    "protocol": "mtproto",
    "settings": {
      "users": [
	{"secret": "dd240064237845e9548edb25ac8c9942"}
      ]	
    },
    "tag": "mttag-in"
    }],
  "outbounds": [
    {
    "protocol": "freedom",
    "settings": {}
  },
    {
    "protocol": "blackhole",
    "settings": {},
    "tag": "blocked"
  },{
    "protocol": "mtproto",
    "tag": "mttag-out",
    "settings": {}
  }],
  "routing": {
    "rules": [
      {
        "type": "field",
        "ip": ["geoip:private"],
        "outboundTag": "blocked"
      },
      {
	"type": "field",
        "inboundTag": ["mttag-in"],
	"outboundTag": "mttag-out"
      }
    ]
  }
}

ss默认配置
IP: www.vpeve.xyz
Port: 443
TLS: 开启
UUID: 0efe4e00-669d-11ea-b0d9-5600029e59e6
Alter ID: 2
Network: WebSocket host: www.vpeve.xyz, path: /03TIu7HX/
~~~~


###     bash <(curl -s -L https://git.io/v2ray.sh)        一键脚本
-   客户端下载
    V2RayNG android
    
    https://github.com/2dust/v2rayNG/releases
    V2RayW Win
    
    https://github.com/Cenmrev/V2RayW/releases
    V2RayN Win
    
    https://github.com/2dust/v2rayN/releases
    V2RayX MAC
    
    https://github.com/Cenmrev/V2RayX
    管理命令
    v2ray info 查看 V2Ray 配置信息
    
    v2ray config 修改 V2Ray 配置
    
    v2ray link 生成 V2Ray 配置文件链接
    
    v2ray infolink 生成 V2Ray 配置信息链接
    
    v2ray qr 生成 V2Ray 配置二维码链接
    
    v2ray ss 修改 Shadowsocks 配置
    
    v2ray ssinfo 查看 Shadowsocks 配置信息
    
    v2ray ssqr 生成 Shadowsocks 配置二维码链接
    
    v2ray status 查看 V2Ray 运行状态
    
    v2ray start 启动 V2Ray
    
    v2ray stop 停止 V2Ray
    
    v2ray restart 重启 V2Ray
    
    v2ray log 查看 V2Ray 运行日志
    
    v2ray update 更新 V2Ray
    
    v2ray update.sh 更新 V2Ray 管理脚本
    
    v2ray uninstall 卸载 V2Ray

