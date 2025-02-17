## fscan <https://github.com/shadow1ng/fscan>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-shadow1ng-orange)
![GitHub stars](https://img.shields.io/github/stars/shadow1ng/fscan.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.0.0-red)
![Time](https://img.shields.io/badge/Join-20210422-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

# 0x00 新增功能

1、UI/UX 优化

2、增加修改-f -o参数，-f支持txt/csv/json，输出格式优化

3、增加端口指纹识别功能。

4、增加本地信息搜集模块，增加本地域控探测模块，增加本地Minidump模块

5、增加Telnet、VNC、Elasticsearch、RabbitMQ、Kafka、ActiveMQ、LDAP、SMTP、IMAP、POP3、SNMP、Zabbix、Modbus、Rsync、Cassandra、Neo4j扫描。

6、架构重构，以反射+插件模块构建

7、增加-log参数，支持INFO，SUCCESS、ERROR、DEBUG参数，用于调试具体信息。

8、优化线程，现在会以更好的多线程运行



**新版由于对旧版代码进行了全面的重构，难免会有Bug，请在遇到Bug时提交Issue，会尽快修复处理，感谢。**

**欢迎提交新的插件模块，目前插件为快速热插拔形式，适用于简易开发。**

# 0x01 简介

一款功能丰富的内网综合扫描工具，提供一键自动化、全方位的漏洞扫描能力。

## 主要功能

- 主机存活探测：快速识别内网中的活跃主机
- 端口扫描：全面检测目标主机开放端口
- 服务爆破：支持对常见服务进行密码爆破测试
- 漏洞利用：集成MS17-010等高危漏洞检测
- Redis利用：支持批量写入公钥进行权限获取
- 系统信息收集：可读取Windows网卡信息
- Web应用检测：
  - Web指纹识别
  - Web漏洞扫描
- 域环境探测：
  - NetBIOS信息获取
  - 域控制器识别
- 后渗透功能：支持通过计划任务实现反弹shell

# 0x02 主要功能
## 1. 信息搜集
- 基于ICMP的主机存活探测：快速识别网络中的活跃主机设备
- 全面的端口扫描：系统地检测目标主机的开放端口情况

## 2. 爆破功能
- 常用服务密码爆破：支持SSH、SMB、RDP等多种协议的身份认证测试
- 数据库密码爆破：覆盖MySQL、MSSQL、Redis、PostgreSQL、Oracle等主流数据库系统

## 3. 系统信息与漏洞扫描
- 网络信息收集：包括NetBIOS探测和域控制器识别
- 系统信息获取：能够读取目标系统网卡配置信息
- 安全漏洞检测：支持MS17-010等高危漏洞的识别与检测

## 4. Web应用探测
- 网站信息收集：自动获取网站标题信息
- Web指纹识别：可识别常见CMS系统与OA框架
- 漏洞扫描能力：集成WebLogic、Struts2等漏洞检测，兼容XRay POC

## 5. 漏洞利用模块
- Redis利用：支持写入公钥或植入计划任务
- SSH远程执行：提供SSH命令执行功能
- MS17-010利用：支持ShellCode注入，可实现添加用户等操作

## 6. 辅助功能
- 扫描结果存储：将所有检测结果保存至文件，便于后续分析

# 0x03 使用说明

## 基础扫描配置

**以下参数由于重构原因并不能保证每一个参数都可以正常运行，出现问题请及时提交Issue。**

**目标配置**

```
-h      指定目标(支持格式:192.168.1.1/24, 192.168.1.1-255, 192.168.1.1,192.168.1.2)
-eh     排除特定目标
-hf     从文件导入目标
```

**端口配置**
```
-p      指定端口范围(默认常用端口)，如: -p 22,80,3306 或 -p 1-65535
-portf  从文件导入端口列表
```

## 认证配置

**用户名密码**
```
-user   指定用户名
-pwd    指定密码
-userf  用户名字典文件
-pwdf   密码字典文件
-usera  添加额外用户名
-pwda   添加额外密码
-domain 指定域名
```

**SSH相关**
```
-sshkey SSH私钥路径
-c      SSH连接后执行的命令
```

## 扫描控制

**扫描模式**
```
-m      指定扫描模式(默认为All)
-t      线程数(默认60)
-time   超时时间(默认3秒)
-top    存活检测结果展示数量(默认10)
-np     跳过存活检测
-ping   使用ping代替ICMP
-skip   跳过指纹识别
```

## Web扫描配置

```
-u      指定单个URL扫描
-uf     从文件导入URL列表
-cookie 设置Cookie
-wt     Web请求超时时间(默认5秒)
```

## 代理设置

```
-proxy  HTTP代理(如: http://127.0.0.1:8080)
-socks5 SOCKS5代理(如: 127.0.0.1:1080)
```

## POC扫描配置

```
-pocpath POC文件路径
-pocname 指定POC名称
-full    启用完整POC扫描
-dns     启用DNS日志
-num     POC并发数(默认20)
```

## Redis利用配置

```
-rf      Redis文件名
-rs      Redis Shell配置
-noredis 禁用Redis检测
```

## 输出控制

```
-o       输出文件路径(默认关闭)
-f       输出格式(默认txt)
-no      禁用结果保存
-silent  静默模式
-nocolor 禁用彩色输出
-json    JSON格式输出
-log     日志级别设置
-pg      显示扫描进度条
```

## 其他配置

```
-local   本地模式
-nobr    禁用暴力破解
-retry   最大重试次数(默认3次)
-path    远程路径配置
-hash    哈希值
-hashf   哈希文件
-sc      Shellcode配置
-wmi     启用WMI
-lang    语言设置(默认zh)
```

**以上参数由于重构原因并不能保证每一个参数都可以正常运行，出现问题请及时提交Issue。**

## 编译说明

```bash
# 基础编译
go build -ldflags="-s -w" -trimpath main.go

# UPX压缩（可选）
upx -9 fscan
```

## 系统安装
```bash
# Arch Linux
yay -S fscan-git
# 或
paru -S fscan-git
```

# 0x04 运行截图

`fscan.exe -h 192.168.x.x  (全功能、ms17010、读取网卡信息)`
![](https://github.com/shadow1ng/fscan/raw/main/image/1.png)

![](https://github.com/shadow1ng/fscan/raw/main/image/4.png)

`fscan.exe -h 192.168.x.x -rf id_rsa.pub (redis 写公钥)`
![](https://github.com/shadow1ng/fscan/raw/main/image/2.png)

`fscan.exe -h 192.168.x.x -c "whoami;id" (ssh 命令)`
![](https://github.com/shadow1ng/fscan/raw/main/image/3.png)

`fscan.exe -h 192.168.x.x -p80 -proxy http://127.0.0.1:8080 一键支持xray的poc`
![](https://github.com/shadow1ng/fscan/raw/main/image/2020-12-12-13-34-44.png)

`fscan.exe -h 192.168.x.x -p 139 (netbios探测、域控识别,下图的[+]DC代表域控)`
![](https://github.com/shadow1ng/fscan/raw/main/image/netbios.png)

`go run .\main.go -h 192.168.x.x/24 -m netbios(-m netbios时,才会显示完整的netbios信息)`
![](https://github.com/shadow1ng/fscan/raw/main/image/netbios1.png)

`go run .\main.go -h 192.0.0.0/8 -m icmp(探测每个C段的网关和数个随机IP,并统计top 10 B、C段存活数量)`
![img.png](https://github.com/shadow1ng/fscan/raw/main/image/live.png)

新的展示

![2.0-1](https://github.com/shadow1ng/fscan/raw/main/image/2.0-1.png)

![2.0-2](https://github.com/shadow1ng/fscan/raw/main/image/2.0-2.png)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2022-12-09 发布演示视频[404星链计划开源安全工具演示——fscan](https://www.bilibili.com/video/BV1Cv4y1R72M/)

## 最近更新

#### [v2.0.0] - 2024-12-19

**更新**  
- 全面代码重构，项目结构重构，插件逻辑优化，项目文档添加，规范化输出、新增本地敏感信息搜集插件等

#### [v1.8.4] - 2024-05-11

**更新**  
* 优化报错处理，避免部分扫描模块报错后导致的程序退出  
* linux(amd64)默认使用fscan  
* windows(x64)默认使用fscan.exe

#### [v1.8.2] - 2022-11-19

**更新**  
- 新增 hash 碰撞  
- 新增 wmiiexec 无回显命令执行

#### [v1.8.1] - 2022-07-06

**更新**  
- 加入手工gc回收,尝试节省无用内存  
- -url 支持逗号隔开  
- 修复一个poc模块bug

#### [v1.8.0] - 2022-07-02

**更新**  
- 加强poc fuzz模块,支持跑备份文件、目录、shiro-key等  
- 新增ms17017利用,可在ms17010-exp.go自定义shellcode,内置添加用户等功能  
- 新增poc、指纹  
- 支持socks5代理  
- 因body指纹更全,默认不再跑ico图标

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
