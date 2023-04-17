### Trojan-Go 安装

1.检测系统安装包

```bash
apt update
```

2.更新安装包

```bash
apt upgrade
```

3.下载Trojan-Go客户端 [GitHub地址](https://github.com/p4gefau1t/trojan-go/releases/tag/v0.10.6) 选择最新的安装包

4.使用wget 下载

```bash
wget https://github.com/p4gefau1t/trojan-go/releases/download/v0.10.6/trojan-go-linux-amd64.zip
```

5.安装unzip

```
apt install unzip
```

6.解压文件

```bash
unzip trojan-go-linux-amd64.zip -d trojan-go
```

7.安装 acme 签发 tls 证书

```bash
curl https://get.acme.sh | sh
```

8. 为 acme 创建一个 软连接 也叫快捷方式 方便我们任意位置调用
```bash
ln -s /root/.acme.sh/acme.sh /usr/local/bin/acme.sh
```

9.切换证书机构至letsencrpty
```bash
acme.sh --set-default-ca --server letsencrpyt
```

10.申请证书
```bash
acme.sh --issue -d www.loquatz.one --standalone -k ec-256
```
如果报错，重新设置一下证书机构，并且安装以下包
```bash
apt install socat
```

在安装证书期间如果出现以下问题，说明防火墙有问题
```
Fetching http://www.loquatz.one/.well-known/acme-challenge/G1M92UOahGEleZNsiBHe_vbmgHzFDfOVtwd77yUu0Do: Timeout during connect (likely firewall problem)
```
去服务器服务商查看一下安全策略组，80,和443是否是开启状态

11.创建安装证书的文件夹
```bash
cd / && mkdir /cert
```

12.安装证书
```bash
acme.sh --installcert -d www.loquatz.one --ecc --key-file /cert/www_loquatz_one.key --fullchain-file /cert/www_loquatz_one.cert
```

13.安装Nginx
```bash
apt instsall nginx
```

14.将trojan-go 复制到 /usr/bin下
```bash
cd ~/trojain-go && cp trojan-go /usr/bin/trojan-go
```

15.在etc下创建trojan-go文件夹
```bash
mkdir /etc/trojan-go
```

16.将trojan-go配置文件 server.json 放在 /etc/trojan-go 文件夹下
```bash
cp ~/trojan-go/example/server.json /etc/trojan-go/server.json
```

17.将trojan-go router 文件拷贝到 /etc/trojan-go 文件夹下
```bash
cp geoip.dat /etc/trojan-go/geoip.dat && cp geoip-only-cn-private.dat /etc/trojan-go/geoip-only-cn-private.dat && cp geosite.dat /etc/trojan-go/geosite.dat
```

18.修改trojan-go.service 为root
```bash
vim ~/trojan-go/example/trojan-go.service
```
```
[Unit]
Description=Trojan-Go - An unidentifiable mechanism that helps you bypass GFW
Documentation=https://p4gefau1t.github.io/trojan-go/
After=network.target nss-lookup.target

[Service]
User=root
CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_BIND_SERVICE
AmbientCapabilities=CAP_NET_ADMIN CAP_NET_BIND_SERVICE
NoNewPrivileges=true
ExecStart=/usr/bin/trojan-go -config /etc/trojan-go/service.json
Restart=on-failure
RestartSec=10s
LimitNOFILE=infinity

[Install]
WantedBy=multi-user.target
```

19.将trojan-go.service 放置 /lib/systemd/system/
```bash
cp ~/trojan-go/example/trojan-go.service /lib/systemd/system/trojan-go.service 
```

20.编辑trojain-go server.json
```bash
vim /etc/trojan-go/service.json
```

```json
{
    "run_type": "server",
    "local_addr": "0.0.0.0",
    "local_port": 10443,
    "remote_addr": "127.0.0.1",
    "remote_port": 80,
    "log_level": 2,
    "password": [
        "MTQwMTE2"
    ],
    "ssl": {
        "cert": "/cert/cloud.loquatz.one.cert",
        "key": "/cert/cloud.loquatz.one.key",
        "sni": "cloud.loquatz.one",
        "fallback_addr": "127.0.0.1",
        "fallback_port": 1443,
        "verify": true,
        "verify_hostname": true,
        "alpn": [
            "h2",
            "http\/1.1"
        ],
        "reuse_session": true,
        "session_ticket": true,
        "session_timeout": 600,
        "plain_http_response": "",
        "cipher": "ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384",
        "cipher_tls13": "TLS_AES_128_GCM_SHA256:TLS_CHACHA20_POLY1305_SHA256:TLS_AES_256_GCM_SHA384",
        "prefer_server_cipher": true,
        "curves": "",
        "dhparam": ""
    },
    "router": {
        "enabled": true,
        "block": [
            "geoip:private"
        ],
        "geoip": "/root/trojan-go/geoip.dat",
        "geosite": "/root/trojan-go/geosite.dat"
    }
}
```

21.编辑Nginx配置 三层代理

```bash
vim /etc/nginx/nginx.conf
```

```
stream {
    map $ssl_preread_server_name $backend_name {
        cloud.loquatz.one trojan;
        mj.loquatz.one web;
        #根据需要选择是否开启默认站点
        #default web; # 默认web
    }

    upstream trojan {
        server 127.0.0.1:10443;
    }

    upstream web {
        server 127.0.0.1:1443;
    }

    server {
        listen 443 reuseport;
        listen [::]:443 reuseport;
        proxy_pass  $backend_name;
        ssl_preread on;
    }
}
```

22. 编辑nginx http代理

```bash
vim /etc/nginx/sites-available/cloud.loquatz.one
```
```
server {
        listen       1443 ssl http2;
        server_name  cloud.loquatz.one;
        client_max_body_size 1000M;

        ssl_certificate      /cert/cloud.loquatz.one.cert;
        ssl_certificate_key  /cert/cloud.loquatz.one.key;

        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;

        location / {
            root   html;
            index  index.html index.htm;
        }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
```

23.创建软链接指向sites-enable
```
ln -s /etc/nginx/sites-available/cloud.loquatz.one /etc/nginx/sites-enabled
```

24.重启Nginx
```bash
nginx -s reload
```

25.将trojan-go 添加到systemed 并启动
```bash
systemctl enable --now trojan-go
```

26.查看trojan-go状态
```bash
systemctl status trojan-go
```

​    
