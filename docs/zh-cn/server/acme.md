## ACME 管理HTTPS证书

### 1.安装ACME
>需要在 **Root用户** 下安装因为需要自动重启Nginx和自动申请证书
```zsh
git clone https://github.com/acmesh-official/acme.sh.git
cd acme.sh
./acme.sh --install -m  你的邮箱地址
```
### 2.创建ZeroSSL账号
>ACME默认使用ZeroSSL发放证书需创建账号 [前往官网](https://app.zerossl.com)

### 3.在ZeroSSL Developer中创建EAB
[点击前往](https://app.zerossl.com/developer)

### 4.添加ZeroSSL 账号
```zsh
acme.sh  --register-account  --server zerossl \
        --eab-kid  你的kid  \
        --eab-hmac-key  你的key
```
!>如果失败需要多试几次，可能是网络问题


### 5.设置阿里云AccessToken
```zsh
export Ali_Key="你的Key"
export Ali_Secret="你的Secret"
```

### 6.申请泛域名证书
```zsh
acme.sh --issue --dns dns_ali -d "你的域名.cn" -d "*.你的域名.cn" --debug --log
```
!> 网络问题会导致失败，多试几次

### 7.创建证书存放文件夹
```zsh
mkdir /etc/nginx/ssl
```

### 8.颁发证书
```zsh
acme.sh --install-cert -d 你的域名 \
--key-file       /etc/nginx/ssl/你的域名.key  \
--fullchain-file /etc/nginx/ssl/你的域名.crt \
--ca-file        /etc/nginx/ssl/你的域名.crt \
--reloadcmd     "service nginx force-reload"
```

> 至此已经完成证书的签名下发