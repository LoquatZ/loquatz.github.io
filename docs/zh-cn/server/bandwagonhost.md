## Header <!-- {docsify-ignore} -->

{% cq %}
所谓翻墙，是指绕过相应的IP封锁、内容过滤、域名劫持、流量限制等，实现对网络内容的访问!
{% endcq %}

<!-- more -->

## 一、科学上网方式介绍

{%note info%}
1.什么是`VPN`？
{%endnote%}

- VPN即 Virtual Private Network，即多台计算机在公共互联网上相互建立网络连接，构成一个虚拟的局域网。

---

{%note info%}
2.为什么我们要`翻墙`（GFW）?
{%endnote%}

- 众所周知，国内局域网通过 `GFW` 隔离了我们与外界的交流，当然，这个隔离并非完全隔离，而是选择性的，天朝不希望你上的网站就直接阻断。每一个网络请求都是有数据特征的，不同的协议具备不同的特征，比如 `HTTP/HTTPS` 这类请求，会很明确地告诉 GFW 它们要请求哪个域名；再比如 `TCP` 请求，它只会告诉 GFW 它们要请求哪个 `IP`。

- GFW 封锁包含多种方式，最容易操作也是最基础的方式便是`域名黑白名单`，在黑名单内的域名不让通过，IP 黑白名单也是这个道理。如果你有一台国外服务器不在 GFW 的黑名单内，国内局域网 的机器就可以跟这一台机器通讯。那么一个翻墙的方案就出来了：境内设备与境外机器通讯，境内想看什么网页，就告诉境外的机器，让境外机器代理抓取，然后送回来，我们要做的就是保证境内设备与境外设备通讯时不被 GFW 怀疑和窃听。

- ssh tunnel 是比较具有代表性的防窃听通讯隧道，通过 ssh 与境外服务器建立一条加密通道，此时的通讯 GFW 会将其视作普通的连接。由于大家都这么玩，GFW 着急了，于是它通过各种流量特征分析，渐渐的能够识别哪些连接是 ssh 隧道，并尝试性的对隧道做干扰，结果还是玩不过 GFW，众多隧道纷纷不通。

---

{%note info%}
3.`翻墙`的方式有哪些？
{%endnote%}

    1. VPN翻墙（加密多协议多跳）
    2. 蓝灯（基于SOCKS5加密协议）
    3. VPS （自己搭建国外服务器）

>以上三种方式是当前主流的科学上网方式

---

{%note info%}
4.以上三种方式优劣对比
{%endnote%}

### `VPN翻墙`

优点|缺点
---|---
中国政府的政策上留有空间，特别是OpenVPN协议在商业环境下的广泛使用，使得网络防火墙无法在协议级别实现完全屏蔽|传输开销相比代理类协议（如SOCKS5）大，一般认为VPN的连接与传输速度也相对慢一点
成熟、通用，设备支持更全面，特备是针对路由器等中间网络设备的支持较强，在某些使用场景下没有VPN无法替代|受打击力度大，国内的服务基本全军覆没，国外的服务能用已经不多，选择越来越少
个人终端客户端使用友好，基本无需配置，装好就能用，升级全自动|供求关系失衡决定了VPN相对自助翻墙方法成本往往更高
节点选择多，商业VPN的服务器遍布全球，虽然绝大部分都不适合中国，但周边的香港、日本等地的服务器集群也足够用|达不到全年100%可用标准，至少我还没找到一年365天都能连上的VPN，特殊时期必挂，一般持续约一周

### `蓝灯`

优点|缺点
---|---
基于SOCK5协议，建立连接快，传输开销比VPN小|不支持iOS设备
是商业软件，相比SSR有更好的客服支持|只支持自动连接，不适合需要手动控制连接IP的场景
有设计良好，好用的客户端|隐私保护能力较一线VPN弱

---

### 自建VPS服务器

#### `ShadowSocksR`(SSR)

>目前最新的ShadowSocksR服务器和主流设备客户端其实是由一个叫ShadowSocksRR（常被称作SSRR）的项目维护的，这是它的Github链接。它是目前最成熟的自建翻墙技术，在国内网民尤其是程序员群体中有着极其广泛的应用，随便找几个码农，瞥一眼他们的工作笔记本，你会注意到任务栏里的“小飞机”图标。

优点|缺点
---|---
可以选择用商业SSR节点，也可以自己架设，相比VPN更灵活|协议开源，长期来说被GFW团队攻破是迟早的事，其实不完全攻破只需解析出流量特征，SSR的死期也就到了
自建SSR服务器，能用的概率比自建VPN服务器能用的概率大很多|缺乏成熟的一体化、友好的部署方案，服务器安装需要一定手动配置，客户端界面可用性比商用VPN软件也还有距离，所以目前SSR主要在电脑技术人员群体中流行
商业节点或自建服务器硬件要求不高，所以扩展容易、成本低|暂无
因为基于SOCKS5协议，连接快传输开销相比VPN小，效率高|暂无

- ##### 基本原理

  - 具体而言，Shadowsocks 将原来 ssh 创建的 Socks5 协议拆开成 Server 端和 Client 端，两个端分别安装在境外服务器和境内设备上。

        +------+     +------+     +=====+     +------+     +-------+
        | 设备  | <-> |Client| <-> | GFW | <-> |Server| <-> | 服务器 |
        +------+     +------+     +=====+     +------+     +-------+

  - Client 和 Server 之间可以通过多种方式加密，并要求提供密码确保链路的安全性。

---

#### `Brook`

优点|缺点
---|---
多协议支持：SOCKS5，VPN，隧道等|暂无
多模式：单服，多服，shadowsocks单服/多服|暂无
跨平台：支持MacOS，iOS，Android，Windows以及多种Linux发行版|暂无
安装方便：提供多平台一键安装包，几乎无需手动配置|暂无
易用：设计良好的命令行工具|暂无

>此种方式暂未研究，有兴趣可以去官网查看 [Brook](https://txthinking.github.io/brook/#/)

---

#### `V2Ray（V2Ray+Websockt+Nginx+TLS）`

优点|缺点
---|---
v2ray支持的传输方式有很多，包括：普通TCP、HTTP伪装、WebSocket流量、普通mKCP、mKCP伪装FaceTime通话、mKCP伪装BT下载流量、mKCP伪装微信视频流量，不同的传输方式其效果会不同，有可能会遇到意想不到的效果哦！当然国内不同的地区、不同的网络环境，效果也会不同，所以具体可以自己进行测试。现在v2ray客户端也很多了，有windows、MAC、linux和安卓版。|暂无

##### **WebSocket (WS)**

- WebSocket是一种在单个TCP连接上进行[`全双工通信`](https://blog.csdn.net/a493823882/article/details/78253617)的协议。WebSocket使得客户端和服务器之间的数据交换变得更加简单，允许服务端主动向客户端推送数据。在WebSocket API中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输。

- 简单说，WebSocket解决了HTTP协议的部分问题，比如每次求都携带状态信息(如身份认证等)、请求每次都要携带完整的头部等等。再加上由于WebSocket[`全双工通信`](https://blog.csdn.net/a493823882/article/details/78253617)，因此能够很好的进行实时通信。用在V2Ray上时，请求与应答的效率要远高于HTTP，而V2Ray的请求要远高于普通的请求，所以WebSocket可以说是一种不错的选择。同时由于WebSocket本身已经成熟，因此有Cloudflare这类云服务商支持基于WebSocket流量的CDN服务，这进一步增进了原本的服务器的安全性。

##### **TLS**

- 传输层安全性协议(英语：Transport Layer Security，缩写作TLS)，及其前身安全套接层(Secure Sockets Layer，缩写作SSL)是一种安全协议，目的是为互联网通信提供安全及数据完整性保障。

- 对于TLS，其实大家不应该觉得陌生，TLS作用于HTTP便诞生出了现今最为常用的协议HTTPS，那么作用于WebSocket，自然便成了WSS，也就是WebSocket+TLS。

- TLS的作用就好比是一个保险箱，不管在传输HTTP还是WebSocket的时候，传输中的内容均是以明文的方式传输的。也就是说，只要有人对传输数据拦截，是完全可以知道你在传输什么东西。而TLS就是用来交换最开始的“锁”的方式，保证传输的保密。

- 对于V2Ray来说，虽然经过了协议的加密，但是这类流量本身就并不“正常”。试想，你手机连接了V2ray，大量数据通过协议向一个固定IP请求，而数据内容与普通的数据格格不入。这自然会引起部分人的警觉。如果嵌套一个保险箱(TLS)，让数据显得和其他请求的数据没什么两样，这样一方面减少了审查者的怀疑，另一方面又加强了数据的安全性。当然由于TLS本身存在一个加密解密的过程，因此势必会对传输的效率带来影响。不过影响是微乎其微的，想要追求安全，自然也需要一定的牺牲。

##### **h2 (HTTP/2)**

- h2便是HTTP/2 (原名HTTP/2.0)即超文本传输协议 2.0，是下一代HTTP协议。对于V2Ray，使用h2必须同时使用TLS。h2本质是HTTP协议，对于传统http1.1协议传输速度快了不少，无主界便是基于h2的网站。h2的下层协议是TCP，因此大家应该知道这类协议的共同缺点了。

- 较之类似的WebSocket协议，传输效率略逊于WebSocket。但是它却有比WebSocket更加好的伪装，由于大部分网站使用HTTP协议，因此h2+TLS这种协议能使V2Ray流量伪装在正常流量中，并且难以察觉。

##### **Nginx**

- Nginx (engine x) 是一个高性能的`HTTP`和`反向代理web`服务器，Nginx是一款轻量级的Web 服务器/反向代理服 务器及电子邮件（IMAP/POP3）代理服务器，在BSD-like 协议下发行。其特点是占有内存少，并发能力强，事实上nginx的并发能力在同类型的网页服务器中表现较好

- V2Ray中的TLS则是配置配置Nginx中

- 由ta来监听 443 端口(443 比较常用，并非 443 不可)，然后将流量转发到 V2Ray 的 WebSocket 所监听的内网端口，V2Ray 服务器端则不需要配置 TLS。

{%note success%}
🔥 `SSR`作为最大众的自建服务器使用策略，一年前曾是首选方式，但是由于国内GWF对于`SSR`的攻破，导致使用`SSR`大概率会出现，`IP被封`，`V2Ray`则是近期兴起的最优策略，采用新的协议，因功能强大、能有效抵抗墙的干扰
{%endnote%}

---

## 二、VPS服务器购买与搭建

{%note info%}
此次文章使用的是`搬瓦工`海外服务器,[搬瓦工 官网地址](https:/bandwagonhost.com/"搬瓦工")
{%endnote%}

### 购买搬瓦工服务器

{%note primary%}
**1.选择套餐**
{%endnote%}
![选择套餐](http://cdn.loquat-z.com/uPic/WX20200903-113805.png)

{%note primary%}
**2.选择具体档次**
{%endnote%}

![选择具体档次](http://cdn.loquat-z.com/uPic/1599104600176.jpg)

{%note primary%}
**3.确认订单**
{%endnote%}

![确认订单](http://cdn.loquat-z.com/uPic/WX20200903-114650.png)

{%note primary%}
**4.填写优惠码**
{%endnote%}

![填写优惠码](http://cdn.loquat-z.com/uPic/WX20200903-114931.png)

>网上找的可用的优惠码`BWH3HYATVBJW`粘贴到优惠码上即可
![网上找的可用的优惠码](http://cdn.loquat-z.com/uPic/WX20200903-115116.png)

{%note primary%}
**5.点击购买**
{%endnote%}
![点击购买](http://cdn.loquat-z.com/uPic/WX20200903-115200.png)

{%note primary%}
**6.确认购买**
{%endnote%}
![确认购买](http://cdn.loquat-z.com/uPic/WX20200903-115423.png)

>我已经购买过了，此处省略支付流程

{%note primary%}
**7.前往我的服务**
{%endnote%}
![前往我的服务](http://cdn.loquat-z.com/uPic/WX20200903-120159.png)

{%note primary%}
**8.前往KVM服务器管理页面**
{%endnote%}
![前往KVM服务器管理页面](http://cdn.loquat-z.com/uPic/WX20200903-121058.png)

{%note primary%}
**9.使用IP与端口通过SSH访问服务器**
{%endnote%}
![使用IP与端口通过SSH访问服务器](http://cdn.loquat-z.com/uPic/WX20200903-121614.png)

{%note primary%}
**10.得到Root访问密码**
{%endnote%}
![得到Root访问密码](http://cdn.loquat-z.com/uPic/WX20200903-121817.png)

{%note primary%}
**11.服务器节点切换**
{%endnote%}
![服务器节点切换](http://cdn.loquat-z.com/uPic/WX20200903-122137.png)

>注意:切换节点后服务器的IP会更改，拿到新的IP然后使用SSH登录服务器就可以了~

{%note primary%}
**11.快照使用**
{%endnote%}
![创建快照](http://cdn.loquat-z.com/uPic/WX20200903-123030.png)

![使用快照重置服务器](http://cdn.loquat-z.com/uPic/WX20200903-123242.png)

>使用SSH登录服务器有很多种方式比如，win平台`XShell`，mac平台`Terminus`,或者系统自带命令行，此处就不一一列举了

## 三、V2Ray搭建

- **安装wget**

    ```bash
    $ yum install wget
    ```

- **安装V2Ray脚本**

    ```bash
    $ wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install.sh" && chmod +x install.sh && bash install.sh
    ```

      >安装脚本之后，会自动运行脚本，脚本存放于执行命令目录下，也可直接运行

    ```bash
     $ ./install.sh
    ```

![脚本运行](http://cdn.loquat-z.com/uPic/WX20200903-134507.png)

- **执行 `1` 采用 V2Ray(Nginx+ws+tls)方式安装**
    ![WX20200903-135008](http://cdn.loquat-z.com/uPic/WX20200903-135008.png)

  > 确认下载 y

![WX20200903-135125](http://cdn.loquat-z.com/uPic/WX20200903-135125.png)

  > 确认时间 y
  > 等待下载....

- **V2Ray需要一个国外的域名用于解析 [Domain](https://ap.www.namecheap.com/)**

  >注册域名省略

- **添加域名解析**

    ![WX20200903-140053](http://cdn.loquat-z.com/uPic/WX20200903-140053.png)

- **配置好域名之后，在脚本中填写，已经配置好的域名**

    ![WX20200903-140255](http://cdn.loquat-z.com/uPic/WX20200903-140255.png)

- **填写端口号，此端口默认443就可以**

    ![WX20200903-140630](http://cdn.loquat-z.com/uPic/WX20200903-140630.png)

- **填写 alterID 默认 2就可以**

    ![WX20200903-140656](http://cdn.loquat-z.com/uPic/WX20200903-140656.png)

    > 等待脚本自动安装，和配置环境，时间2-5分钟左右
    > 执行脚本过程中SSL证书可能会签发失败，重新运行脚本，按步骤重新，走一遍即可

- **选择链接的种类，使用 1  `V2RayNG/V2RayN` 即可**
    ![WX20200903-141311](http://cdn.loquat-z.com/uPic/WX20200903-141311.png)

- **选择兼容类型 默认 选 1即可**

    ![WX20200903-141414](http://cdn.loquat-z.com/uPic/WX20200903-141414.png)

![WX20200903-141803](http://cdn.loquat-z.com/uPic/WX20200903-141803.png)

- **V2Ray客户端下载 [V2Ray客户端](https://github.com/2dust/v2rayN/releases)**

- **安装脚本分析，[脚本地址](https://github.com/wulabing/V2Ray_ws-tls_bash_onekey/blob/master/install.sh)**

{%note success%}
**至此V2Ray就部署完成了吖，使用V2Ray客户端，扫描二维码，或者填入URL导入链接vmess: 开头...就可以愉快的科学上网了~**
{%endnote%}

{%note danger%}
**科学上网仅限于自己使用，最好不要到处传播，更不要通过科学上网，传播反华言辞，浏览不良网站，绿色使用谨记！！！**
{%endnote%}
