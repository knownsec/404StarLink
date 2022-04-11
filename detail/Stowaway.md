## Stowaway <https://github.com/ph4ntonn/Stowaway>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-ph4ntonn-orange)
![GitHub stars](https://img.shields.io/github/stars/ph4ntonn/Stowaway.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1-red)
![Time](https://img.shields.io/badge/Join-20210702-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


Stowaway是一个利用go语言编写、专为渗透测试工作者制作的多级代理工具

用户可使用此程序将外部流量通过多个节点代理至内网，突破内网访问限制，构造树状节点网络，并轻松实现管理功能

PS:谢谢大家的star，同时欢迎大家使用后提出问题&&Bug :kissing_heart:。

PPS:**请务必在使用前详细阅读使用方法及文末的注意事项**

> 此工具仅限于安全研究和教学，用户承担因使用此工具而导致的所有法律和相关责任！ 作者不承担任何法律和相关责任！

[English](README_EN.md)

## 特性

- 管理端更加友好的交互,支持命令补全/历史
- 一目了然的节点树管理
- 丰富的节点信息展示
- 节点间正向/反向连接
- 节点间支持重连
- 节点间可通过socks5代理进行连接
- 节点间可通过ssh隧道连接
- 节点间流量可选择TCP/HTTP
- 多级socks5流量代理转发,支持UDP/TCP,IPV4/IPV6
- 节点支持ssh访问远程主机
- 远程shell
- 上传及下载文件
- 端口本地/远程映射
- 节点可端口复用
- 自由开关各类服务
- 节点间相互认证
- 节点间流量以AES-256-GCM进行加密
- 相较于v1.0，文件体积减小25%
- 支持各类平台(Linux/Mac/Windows/MIPS/ARM)

## 下载及演示

- 不想编译的盆油可以直接用[release](https://github.com/ph4ntonn/Stowaway/releases)下编译完成的程序
-  演示视频：[Youtube](https://www.youtube.com/watch?v=Lh5Q0RPWKMU&list=PLkbGxnHFIhA_g5XZtKzN4u-JXRq41L2g-)

## 使用方法

### 角色
Stowaway一共包含两种角色，分别是：

- ```admin```    渗透测试者使用的主控端
- ```agent```    渗透测试者部署的被控端

### 名词定义

- 节点: 指admin || agent
- 主动模式: 指当前操作的节点主动连接另一个节点
- 被动模式: 指当前操作的节点监听某个端口，等待另一个节点连接
- 上游: 指当前操作的节点与其父节点之间的流量
- 下游：指当前操作的节点与其**所有**子节点之间的流量

### 参数解析

- admin

```
参数:
-l 被动模式下的监听地址[ip]:<port>
-s 节点通信加密密钥,所有节点(admin&&agent)必须一致
-c 主动模式下的目标节点地址
--proxy socks5代理服务器地址
--proxyu socks5代理服务器用户名(可选)
--proxyp socks5代理服务器密码(可选)
--down 下游协议类型,默认为裸TCP流量,可选HTTP
```

- agent

```
参数:
-l 被动模式下的监听地址[ip]:<port>
-s 节点通信加密密钥
-c 主动模式下的目标节点地址
--proxy socks5代理服务器地址
--proxyu socks5代理服务器用户名(可选)
--proxyp socks5代理服务器密码(可选)
--reconnect 重连时间间隔
--rehost 端口复用时复用的IP地址
--report 端口复用时复用的端口号
--up 上游协议类型,默认为裸TCP流量,可选HTTP
--down 下游协议类型,默认为裸TCP流量,可选HTTP
```

### 参数用法

#### -l

此参数admin&&agent用法一致，仅用在被动模式下 

若不指定IP地址，则默认监听在```0.0.0.0```上

- admin:  ```./stowaway_admin -l 9999``` or ```./stowaway_admin -l 127.0.0.1:9999```

- agent:  ```./stowaway_agent -l 9999```  or ```./stowaway_agent -l 127.0.0.1:9999```

#### -s

此参数admin&&agent用法一致，可用在主动&&被动模式下

可选，若为空，则代表通信不被加密，反之则通信基于用户所给出的密钥加密

- admin:  ```./stowaway_admin -l 9999 -s 123``` 

- agent:  ```./stowaway_agent -l 9999 -s 123``` 

#### -c

此参数admin&&agent用法一致，仅用在主动模式下

代表了希望连接到的节点的地址

- admin:  ```./stowaway_admin -c 127.0.0.1:9999``` 

- agent:  ```./stowaway_agent -c 127.0.0.1:9999``` 

#### --proxy/--proxyu/--proxyp

这三个参数admin&&agent用法一致，仅用在主动模式下

```--proxy```代表socks5代理服务器地址，```--proxyu```以及```--proxyp```可选

无用户名密码：

- admin:  ```./stowaway_admin -c 127.0.0.1:9999 --proxy xxx.xxx.xxx.xxx```

- agent:  ```./stowaway_agent -c 127.0.0.1:9999 --proxy xxx.xxx.xxx.xxx``` 

有用户名密码:

- admin:  ```./stowaway_admin -c 127.0.0.1:9999 --proxy xxx.xxx.xxx.xxx --proxyu xxx --proxyp xxx```

- agent:  ```./stowaway_agent -c 127.0.0.1:9999 --proxy xxx.xxx.xxx.xxx--proxyu xxx --proxyp xxx``` 

#### --up/--down

这两个参数admin&&agent用法一致，可用在主动&&被动模式下

但注意admin上没有```--up```参数

这两个参数可选，若为空，则代表上/下游流量为裸TCP流量

若希望上/下游流量为HTTP流量，设置此两参数即可

- admin:  ```./stowaway_admin -c 127.0.0.1:9999 --down http``` 

- agent:  ```./stowaway_agent -c 127.0.0.1:9999 --up http```  or ```./stowaway_agent -c 127.0.0.1:9999 --up http --down http```

**注意一点，当你设置了某一节点上/下游为TCP/HTTP流量后，与其连接的父/子节点的下/上游流量必须设置为一致！！！**

如下

- admin:  ```./stowaway_admin -c 127.0.0.1:9999 --down http``` 

- agent:  ```./stowaway_agent -l 9999 --up http```

上面这种情况，agent必须设置```--up```为http，否则会导致网络出错

agent间也一样

假设agent-1正在```127.0.0.1:10000```端口上等待子节点的连接，并且设置了```--down http```

那么agent-2也必须设置```--up```为http，否则会导致网络出错

- agent-2:  ```./stowaway_agent -c 127.0.0.1:10000 --up http```

#### --reconnect

此参数仅用在agent，且仅用在主动模式下

参数可选，若不设置，则代表节点在网络连接断开后不会主动重连，若设置，则代表节点会每隔x(你设置的秒数)秒尝试重连至父节点

- admin:  ```./stowaway_admin -l 9999``` 

- agent:  ```./stowaway_agent -c 127.0.0.1:9999 --reconnect 10```

上面这种情况下，代表如果agent与admin之间的连接断开，agent会每隔十秒尝试重连回admin

agent之间也与上面情况一致

并且```--reconnect```参数可以与```--proxy```/```--proxyu```/```--proxyp```一起使用，agent将会参照启动时的设置，通过代理尝试重连

#### --rehost/--report

这两个参数比较特别，仅用在agent端，详细请参见下方的端口复用机制

## 端口复用机制

  当前Stowaway提供基于SO_REUSEPORT和SO_REUSEADDR特性的端口复用功能及基于IPTABLES的端口复用功能

   - 在linux下可以大部分的功能端口

   - 在windows下不可复用iis，rdp端口，可以复用mysql，apache服务的端口


### 复用方式
- SO_REUSEPORT和SO_REUSEADDR模式

  假设agent端采用端口复用机制复用80端口

  此时agent端必须设置```--rehost```&&```--report```&&```-s```参数

  - --rehost代表希望复用的IP地址，不可为0.0.0.0，普遍应当是网卡的外部地址

  - --report代表希望复用的端口

  - -s代表通信密钥

  **主要支持windows、mac环境下的复用，linux亦可，但限制较多**
  
  - admin端：```./stowaway_admin -c 192.168.0.105:80 -s 123```
  - agent端： ```./stowaway_agent  --report 80 --rehost 192.168.0.105 -s 123```


- IPTABLES模式

  假设agent端采用端口复用机制复用22端口

  此时agent端必须设置```-l```&&```--report```&&```-s```参数

  - -l 代表无法被正常访问的端口，也就是你真正想让agent监听并接受连接的端口

  - --report代表希望复用的端口

  - -s代表通信密钥

  **仅支持linux环境下的复用，agent会自动修改IPTABLES，需要root权限**

  - agent端： ```./stowaway_agent --report 22 -l 10000 -s 123```

    在agent启动后，请使用```script```目录下的```reuse.py```

    先设置SECRET的值(SECRET的值就是在启动各个节点时所设置的通信密钥),

    之后执行：```python reuse.py --start --rhost xxx.xxx.xxx.xxx --rport xxx```

    - --rhost代表agent的地址

    - --rport代表被复用的端口,在本例中应当为22
  
  - 此时admin端就可以连接：```./stowaway_admin -c 192.168.0.105:22 -s 123```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-11-16 发布文章[《Stowaway : 专为渗透测试工作者制作的多级代理工具》](https://mp.weixin.qq.com/s/L7Ikxd_Nql8SkezY4l0blQ)

## 最近更新

#### [v2.1] - 2022-04-08

**更新**  
- 修复关闭短连接时的数据丢失错误  
- 添加 gzip 功能  
- 优化关键代码  
- 修复一些 bugs

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
