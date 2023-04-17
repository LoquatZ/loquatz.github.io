>[!TIP] Frp 是一个高性能的反向代理应用，可以帮助您轻松地进行内网穿透，对外网提供服务，支持 tcp, http, https 等协议类型，并且 web 服务支持根据域名进行路由转发。

## 为什么使用 frp ？

通过在具有公网 IP 的节点上部署 frp 服务端，可以轻松地将内网服务穿透到公网，同时提供诸多专业的功能特性，这包括：

- 客户端服务端通信支持 TCP、KCP 以及 Websocket 等多种协议。

- 采用 TCP 连接流式复用，在单个连接间承载更多请求，节省连接建立时间。

- 代理组间的负载均衡。

- 端口复用，多个服务通过同一个服务端端口暴露。

- 多个原生支持的客户端插件（静态文件查看，HTTP、SOCK5 代理等），便于独立使用 frp 客户端完成某些工作。

- 高度扩展性的服务端插件系统，方便结合自身需求进行功能扩展。

- 服务端和客户端 UI 页面。

## Linux 安装Frp

```bash
export FRP_VERSION=0.47.0
sudo mkdir -p /etc/frp
cd /etc/frp
sudo wget "https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_amd64.tar.gz"
sudo tar xzvf frp_${FRP_VERSION}_linux_amd64.tar.gz
sudo mv frp_${FRP_VERSION}_linux_amd64/* /etc/frp
```

>`FRP_VERSION`前往[FrpGit地址](https://github.com/fatedier/frp/releases)查看最新地址

- FRP 默认提供了 2 个服务端配置文件，一个是简化版的 frps.ini，另一个是完整版的 frps_full.ini。初学者只需用简版配置即可，在简版 frps.ini 配置文件里，默认设置了监听端口为 7000，你可以按需修改它。

**`防火墙和安全组开放指定的端口：`**

>请一定要记住，你需要将服务器的系统防火墙，以及阿里云、腾讯云后台里找到“安全组策略”的相关配置，设置 7000 或你修改过的对应端口的「允许入站和出站」，否则会一直连接不上的哦！！！这个切记！！

### 配置frps.ini

```bash
[common]
#公网IP
server_addr = 104.xxx.xxx.71
#端口号
bind_port = 6789
#用于验证Frpc客户端认证
token = Zr5dYt4r76ASFYhK
#监听Frp运行状态端口
dashboard_port = 6443
#监听者账户
dashboard_user = UserName
#监听者密码
dashboard_pwd = UserPassWord
#HTTP对应端口号
vhost_http_port = 6789
#HTTPS对应端口号
vhost_https_port = 6789
```

### 启动 FRP 服务端

```bash
$./frps -c ./frps.ini
```

>至此Frps就可以在服务器运行成功了,我们可以通过104.xxx.xxx.71:6443,查看Frps的运行状态

### 使用systemctl来控制启动

创建服务

```bash
$sudo vim /lib/systemd/system/frps.service
```

在frps.service里写入以下内容

```bash
[Unit]
Description=fraps service
After=network.target syslog.target
Wants=network.target

[Service]
Type=simple
#启动服务的命令（此处写你的frps的实际安装目录）
ExecStart=/your/path/frps -c /your/path/frps.ini

[Install]
WantedBy=multi-user.target
```

然后就启动frps

```bash
$sudo systemctl start frps
```

再打开自启动

```bash
$sudo systemctl enable frps
```

- 如果要重启应用，可以这样，`sudo systemctl restart frps`

- 如果要停止应用，可以输入，`sudo systemctl stop frps`

- 如果要查看应用的日志，可以输入，`sudo systemctl status frps`

### Windows配置Frpc客户端

[windowsFrp下载地址](https://github.com/fatedier/frp/releases)

>需要注意的是Window的版本要跟服务器版本一直哦

### 配置frpc.ini

```bash
[common]
#Frps服务器地址
server_addr = 47.xxx.xxx.6
#Frps服务器端口号
server_port = 6789
#Frps服务器配置的Token
token = Zr5dYt4r76ASFYhK

#nexus服务器
[nexus]
#连接类型
type = tcp
#本地IP
local_ip = 192.168.1.112
#本地端口号
local_port = 8081
#远程端口号
remote_port = 8081

#ssh
[ssh]
type = tcp
local_ip = 192.168.1.112
local_port = 22
remote_port = 8082

#Windows远程访问
[mstsc]
type = tcp
local_ip = 192.168.1.112
local_port = 3389
remote_port = 8083
```

### 启动 FRC 服务端

```bash
$./frpc.exe -c ./frpc.ini
```

>至此Frpc就可以在windows运行成功了,我们可以通过
`104.xxx.xxx.71:外访问的端口号`,通过外网来访问内网的电脑了.
