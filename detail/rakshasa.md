## rakshasa <https://github.com/Mob2003/rakshasa>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-Mob2003-orange)
![GitHub stars](https://img.shields.io/github/stars/Mob2003/rakshasa.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.2.3-red)
![Time](https://img.shields.io/badge/Join-20230410-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

rakshasa是一个使用Go语言编写的强大多级代理工具，专为实现**多级代理**，**内网穿透**而设计。它可以在节点群里面任意两个节点之间转发TCP请求和响应，同时支持**socks5代理**，**http代理**，并且可以**引入外部http、socks5代理池，自动切换请求IP**。

节点之间使用内置证书的TLS加密TCP通讯，再叠加一层自定义秘钥的AES加密，可以在所有Go支持的平台使用。可以在你所有的的Windows和Linux服务器上搭建节点并组成节点群网络。

节点分为普通节点(node)与控制节点(fullnode)
- 普通节点，无法控制其他节点进行代理、shell等操作
- 控制节点，全功能节点

## 项目结构示例和截图
[点击查看更多介绍](https://github.com/Mob2003/rakshasa/blob/main/readme/rakshasa%E9%A1%B9%E7%9B%AE%E8%AE%BE%E8%AE%A1.md)

[win10+Proxifier实现内网穿透](https://github.com/Mob2003/rakshasa/blob/main/readme/rakshasa%E5%86%85%E7%BD%91%E7%A9%BF%E9%80%8F--win10+Proxifier%E4%BD%BF%E7%94%A8%E6%A1%88%E4%BE%8B.md)

## 版本迭代
-  **v0.1.0**  2023-03-28
    - 首次发布
-  **v0.2.0**  2023-04-02
    - 更改为fullnode版本，fullnode为全功能版本可以控制别人也能被控
    - 增加node版本，去掉私钥，无法发起代理等关键操作，适合被控
    - 增加lite版本，在上面版本的基础上，精简cli交互与http代理池，体积缩小2mb
    - 优化节点连接逻辑，并且遍历网卡ip进行net.Dail，解决多网卡下，无法连接的问题
-  **v0.2.2**  2023-04-08
    - 增加http_proxy重连逻辑，节点掉线后重连http代理能够正常重连使用
    - 优化节点重连逻辑
    - 增加uuid选项，默认uuid使用网卡mac作为随机数种子，进行生成

## 编译与使用

生成新的证书，编译所有版本节点
```shell
go run build.go -all
```

编译所有版本节点（不更新证书）
```shell
go run build.go -all -nocert
```

生成覆盖证书
```shell
go run build.go -gencert
```

生成控制节点与普通节点
```shell
go run build.go -fullnode
```

只生成普通节点
```shell
go run build.go -node
```

证书保存在cert目录下，可以使用第三方工具生成，请使用RSA PKCS1-V1.5
```shell
private.go     --编译普通节点的时候要删除此文件
private.pem  --与public.pem对应的公钥私钥，普通节点不包含私钥
public.pem
server.crt     --tls通讯证书
server.key    --tls通讯私钥
```
## 版本区别

|     | fullnode  | node|fullnode_lite|node_lite|
|  ----  | ----  |----  |----  |----  |
|连接其他节点  | √ |√ |√ |√ |
|启动本地socks5代理 | √ |√ |√ |√ |
|启动本地http代理 | √ |√ |√ |√ |
|启动多层代理 | √ |× |√ |× |
|远程shell| √ |× |√ |× |
|其他远程功能| √ |× |√ |× |
| 交互式CLI  | √ |√ |× |× |
| check_proxy  | √ |√ |× |× |

简单来讲
- fullnode 完全版，能控制别人，也能被控
- node 能连接其他节点，但是不能对其他节点操控，适合作为被控端
- lite版本，精简掉cli和net/http，与一些debug的代码

## 使用图示
![image](https://user-images.githubusercontent.com/128351726/226882870-f4f3cbc0-61df-486c-afc0-511d87586402.png)


## 使用方法



### 启动一个带CLI节点
不带任何参数即可启动：
```shell
d:\>rakshasa.exe
start on port: 8883
rakshasa>
rakshasa>help

Commands:
  bind              进入bind功能
  clear             clear the screen
  config            配置管理
  connect           进入connect功能
  exit              exit the program
  help              display help
  httpproxy         进入httpProxy功能
  new               与一个或者多个节点连接，使用方法 new ip:端口 多个地址以,间隔 如1080 127.0.0.1:1081,127.0.0.1:1082
  ping              ping 节点
  print             列出所有节点
  remoteshell       远程shell
  remotesocks5      进入remotesocks5功能
  shellcode         执行shellcode
  socks5            进入socks5功能


rakshasa>
```
请查阅[CLI使用说明](https://github.com/Mob2003/rakshasa/blob/main/readme/cli.md)了解详细信息

## 其他启动参数说明
### -nocli
在无法后台执行的情况下，启动一个不带 CLI 的节点:
```shell
nohup /root/rakshasa -nocli > /root/rakshasa.log 2>&1 &
#Linux下配合nohup后台执行
```

### -p 端口
以指定端口启动:
```shell
rakshasa -p 8883
```

### -d ip:port,ip:port...
连接下一层代理或更多层代理，多个地址以逗号隔开，生效在最后一个 ip:port：
```shell
rakshasa -d 192.168.1.1:8883,192.168.1.2:8883,192.168.1.3:8883 -socks5 1080
#从本地1080端口启动一个socks5代理，流量通过三层转发ip最后在192.168.1.3请求目标数据
```

### -socks5 用户名:密码@ip:端口 
本地开启SOCKS5代理穿透到远程节点，可以不带-d：
```shell
rakshasa -socks5 1080 
#不使用-d参数，则表示直接在本机启动一个socks5代理
```



### -remotesocks5 端口 
远程开启SOCKS5代理流量出口到本地：
```shell
rakshasa -remotesocks5 1081  -d 192.168.1.2:1080,192.168.1.3:1080
#方向从右往左(加上本机是3个节点)，在192.168.1.3这台机器开启一个socks5端口1081，流量穿透到本地节点出去
```

### -connect ip:port,remote_ip:remote_port 
本地监听并转发到指定 IP 端口，使用场景为本机连接 teamserver，隐藏本机 IP：
```shell
rakshasa -connect 127.0.0.1:50050,192,168,1,2:50050 -d 192.168.1.3:1080,192.168.1.4:1080 
#本机cs连接127.0.0.1:50050实际上通过1.3,1.4节点后，再连接到192.168.1.2:50050 teamserver，teamserver看到你的ip是最后一个节点的ip
```

### -bind  ip:port,remote_ip:remote_port
反向代理模式，必须配合-d使用：
```shell
rakshasa -bind 192.168.1.2:50050,0,0,0.0:50050 -d 192.168.1.3:1080,192.168.1.4:1080
#与上面相反，在最右端节点监听端口50050，流量到本机节点后，最终发往192.168.1.2，最终上线ip为本机ip
```
### -http_proxy 用户名:密码@ip:端口
启动一个http代理，可以不使用-d，建议配合-http_proxy_pool使用代理池，自动切换代理ip：
```shell
rakshasa -http_proxy 8080 -http_proxy_pool out.txt
```

### -password 密钥
各节点除了证书校验之外，还额外支持密钥连接，建议使用并定期更换密钥，以避免二进制泄露后被别人连上
```shell
rakshasa -password 123456
```


### -f yaml文件 [详细说明](https://github.com/Mob2003/rakshasa/blob/main/readme/config.md)
指定配置文件启动。

### -help 
更多启动参数使用帮助

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v0.2.3] - 2023-04-23

**更新**  
- 优化一个连接失败可能会导致nil的bug  
- 修改一个nodeMap为sync.Map以减少代码里面lock的使用

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
