## dperf <https://github.com/baidu/dperf>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-C-blue)
![Author](https://img.shields.io/badge/Author-Benjamin-orange)
![GitHub stars](https://img.shields.io/github/stars/baidu/dperf.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.7.0-red)
![Time](https://img.shields.io/badge/Join-20230410-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

dperf 是一个100Gbps的网络性能与压力测试软件。

## 优点
- 性能强大：
  - 基于 DPDK，使用一台普通 x86 服务器就可以产生巨大的流量：千万级的 HTTP 每秒新建连接数，数百Gbps的带宽，几十亿的并发连接数
- 统计信息详细：
  - 能够输出详细的统计信息，并且识别每一个丢包
- 使用场景丰富：
  - 可用于对四层负载均衡等四层网关进行性能压力测试、长稳测试
  - 可用于对云上虚拟机的网络性能进行测试
  - 可用于对网卡性能、CPU的网络报文处理能力进行测试
  - 压测场景下，可作为高性能的HTTP Server或HTTP Client单独使用

## 性能
### HTTP每秒新建连接数
|Client Cores|Server Cores|HTTP CPS|
|------------|------------|--------|
|1|1|2,101,044|
|2|2|4,000,423|
|4|4|7,010,743|
|6|6|10,027,172|

### HTTP吞吐
|Client Cores|Server Cores|RX(Gbps)|TX(Gbps)|Client CPU Usage(%)|Server CPU Usage(%)|
|------------|------------|--------|--------|-------------------|-------------------|
|1|1|18|18|60|59|
|2|2|35|35|60|59|
|4|4|46|46|43|43|

### HTTP并发连接数
|Client Cores|Server Cores|Current Connections|Client CPU Usage(%)|Server CPU Usage(%)|
|------------|------------|-------------------|-------------------|-------------------|
|1|1|100,000,000|34|39|
|2|2|200,000,000|36|39|
|4|4|400,000,000|40|41|

### UDP TX PPS
|Client Cores|TX MPPS|Client CPU Usage(%)|
|------------|-------|-------------------|
|1|15.96|95|
|2|29.95|95|
|4|34.92|67|
|6|35.92|54|
|8|37.12|22|

注意：本测试基于单张25Gbps Mellanox CX4

### 测试环境配置（客户端、服务器）
dperf 的以上性能数据，基于下面的配置测试得到：

- 内存: 512GB(大页 100GB)
- 网卡: Mellanox MT27710 25Gbps * 2
- 内核: 4.19.90

## 统计数据
dperf 每秒输出多种统计数据：
- TPS, CPS,  各种维度的PPS
- TCP/Socket/HTTP级别的错误数
- 丢包数
- 按照TCP Flag分类的报文重传数

```
seconds 22                 cpuUsage 52
pktRx   3,001,058          pktTx    3,001,025          bitsRx   2,272,799,040      bitsTx  1,920,657,600      dropTx  0
arpRx   0                  arpTx    0                  icmpRx   0                  icmpTx  0                  otherRx 0          badRx 0
synRx   1,000,345          synTx    1,000,330          finRx    1,000,350          finTx   1,000,350          rstRx   0          rstTx 0
synRt   0                  finRt    0                  ackRt    0                  pushRt  0                  tcpDrop 0
skOpen  1,000,330          skClose  1,000,363          skCon    230                skErr   0
httpGet 1,000,345          http2XX  1,000,350          httpErr  0
ierrors 0                  oerrors  0                  imissed  0
```

## 开始使用
### 设置大页
    #参考如下参数编辑 '/boot/grub2/grub.cfg'，然后重启OS
    linux16 /vmlinuz-... nopku transparent_hugepage=never default_hugepagesz=1G hugepagesz=1G hugepages=8

### 编译DPDK
    #编辑'config/common_base'打开PMD开关
    #Mellanox CX4/CX5 requires 'CONFIG_RTE_LIBRTE_MLX5_PMD=y'
    #HNS3 requires 'CONFIG_RTE_LIBRTE_HNS3_PMD=y'
    #VMXNET3 requires 'CONFIG_RTE_LIBRTE_VMXNET3_PMD=y'
    
    TARGET=x86_64-native-linuxapp-gcc #or arm64-armv8a-linuxapp-gcc
    cd /root/dpdk/dpdk-stable-19.11.10
    make install T=$TARGET -j16

### 编译dperf
    cd dperf
    make -j8 RTE_SDK=/root/dpdk/dpdk-stable-19.11.10 RTE_TARGET=$TARGET

### 绑定网卡 
    #Mellanox网卡跳过此步
    #假设PCI号是0000:1b:00.0
    
    modprobe uio
    modprobe uio_pci_generic
    /root/dpdk/dpdk-stable-19.11.10/usertools/dpdk-devbind.py -b uio_pci_generic 0000:1b:00.0

### 启动dperf server
    #dperf server监听6.6.241.27:80, 网关是6.6.241.1
    ./build/dperf -c test/http/server-cps.conf

### 从客户端发送请求
    #客户端IP必须要在配置文件的'client'范围内
    ping 6.6.241.27
    curl http://6.6.241.27/

## 运行测试
下面的例子运行一个HTTP CPS压力测试。    
    #在server端运行dperf
    ./build/dperf -c test/http/server-cps.conf
    
    #以另一台机器作为client端，运行dperf
    ./build/dperf -c test/http/client-cps.conf

## 文档
请访问[https://dperf.org/](https://dperf.org/).

## 限制
 - dperf 要求HTTP消息在一个数据包中，所以不适合7层负载均衡的测试。
 - dperf 要求独占使用网络接口。
 - dperf 没有路由功能。建议配合三层交换机搭建测试环境。

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.7.0] - 2024-06-06

**新增**  
- 发送http post请求  
- dpdk pdump  
- fast_close：使用RST关闭连接  
- 支持DPDK-23.11和DPDK-24  
- 启用simd512  
- 禁用ack  
- 配置重发超时  

**更改**  
- 配置DPDK日志级别  
- clear_screen：dperf可以清除屏幕输出，让屏幕更干净  
- 静态链接  

**修复**  
- dpdk清理  
- CFLAGS覆盖  
- 拼写错误  
- 不要清除处于等待时间状态的序列

#### [v1.6.0] - 2023-10-10

**新增**  
- dperf 服务器可返回较大的 payload  
- 现在可使用 l3/l3l4 的网卡 RSS 分流算法  

**改动**  
- 最小本地端口范围可以设置为 1  
- 优化移除了 lport_range 之外的无用 socket  
- 将文档移至 dperf.org  
- 调整最大的 MTU 默认值  

**修复**  
- 修复 udp 连接数为负数的问题  
- 启动失败时将打印更多信息  
- 修复拼写错误和表达问题  
- 修复查找端口 id 时的错误  
- 修复创建新连接时长计算的错误  
- 仅当启用 http 时才能配置 http_host 或 http_path  
- 修复 dpdk-18.11 上构建错误的问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
