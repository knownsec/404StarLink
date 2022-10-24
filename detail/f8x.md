## f8x <https://github.com/ffffffff0x/f8x>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Bash-blue)
![Author](https://img.shields.io/badge/Author-ffffffff0x-orange)
![GitHub stars](https://img.shields.io/github/stars/ffffffff0x/f8x.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.6.2-red)
![Time](https://img.shields.io/badge/Join-20210223-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


一款红/蓝队环境自动化部署工具,支持多种场景,渗透,开发,代理环境,服务可选项等。


大多数场景下，在不同的云购买一些 vps 服务器用于部署红 / 蓝队设施，不能做到开箱即用，使用 f8x 可以快速部署所需要的各类服务。同时兼顾到本地 VM 虚拟机的需求，可以选择走 socket 代理进行安装部署，Proxychains-ng 也会自动安装，只需做好 Proxychains-ng 配置即可。

## 开始

**下载**
- 通过 CF Workers 下载 [推荐]
  - wget : `wget -O f8x https://f8x.io/`
  - curl : `curl -o f8x https://f8x.io/`

- 访问 [releases](https://github.com/ffffffff0x/f8x/releases) 下载

**使用**
```bash
bash f8x -h
```

如果你希望方便点使用可以直接加到环境变量中
- wget : `wget -O f8x https://f8x.io/ && mv --force f8x /usr/local/bin/f8x && chmod +x /usr/local/bin/f8x`
  - `f8x -h`
- curl : `curl -o f8x https://f8x.io/ && mv --force f8x /usr/local/bin/f8x && chmod +x /usr/local/bin/f8x`
  - `f8x -h`

**系统依赖**

f8x 基本上不需要任何依赖,或者说它就是为了帮助你安装各种依赖而生的😁

**f8x-ctf**

该脚本用于部署 CTF 环境,支持 (Web、Misc、Crypto、Pwn、Iot) 分类

- wget : `wget -O f8x-ctf https://f8x.io/ctf`
  - `bash f8x-ctf -help`
- curl : `curl -o f8x-ctf https://f8x.io/ctf`
  - `bash f8x-ctf -help`

**f8x-dev**

该脚本用于部署中间件和数据库环境,支持 (apache、nginx、tomcat、Database、php) 分类

- wget : `wget -O f8x-dev https://f8x.io/dev`
  - `bash f8x-dev -help`
- curl : `curl -o f8x-dev https://f8x.io/dev`
  - `bash f8x-dev -help`

---

## 支持选项

目前 f8x 支持以下部署选项 (Linux arm64 下大部分都支持)

**1. 批量化安装**
- 使用 -b 选项安装基本环境 (gcc、make、git、vim、telnet、jq、unzip 等基本工具)
- 使用 -p 选项安装代理环境 (警告:国外云服务器上不要用,会降速)
- 使用 -d 选项安装开发环境 (python3、pip3、Go、Docker、Docker-Compose、SDKMAN)
- 使用 -k 选项安装渗透环境 (hashcat、ffuf、OneForAll、ksubdomain、impacket 等渗透工具)
  - -ka 信息收集、扫描、爆破、抓取
  - -kb 漏洞利用
  - -kc 后渗透、C2
  - -kd 其他
  - -ke 功能重叠或长期不维护
- 使用 -s 选项安装蓝队环境 (Fail2Ban、chkrootkit、rkhunter、河马webshell查杀工具)
- 使用 -f 选项安装其他工具 (Bash_Insulter、vlmcsd、AdguardTeam、trash-cli 等辅助工具)
- 使用 -cloud 选项安装云应用 (Terraform、Serverless Framework、wrangler)
- 使用 -all 选项全自动化部署 (默认不走代理,兼容 CentOS7/8,Debain10/9,Ubuntu20/18,Fedora33)

**2. 开发环境**
- 使用 -docker 选项安装 docker 环境
- 使用 -lua 选项安装 lua 环境
- 使用 -nn 选项安装 npm & NodeJs 环境
- 使用 -go 选项安装 go 环境
- 使用 -oraclejdk(8/11) 选项安装 oraclejdk 环境
- 使用 -openjdk 选项安装 openjdk 环境
- 使用 -py3(7/8/9/10) 选项安装 python3 环境
- 使用 -py2 选项安装 python2 环境
- 使用 -pip2-f 选项强制安装 pip2 环境 (建议在 -python2 选项失败的情况下运行)
- 使用 -perl 选项安装 perl 环境
- 使用 -ruby 选项安装 ruby 环境
- 使用 -rust 选项安装 rust 环境
- 使用 -code 选项安装 code-server 环境
- 使用 -chromium 选项安装 Chromium 环境 (用于配合 -k 选项中的 rad、crawlergo)
- 使用 -phantomjs 选项安装 PhantomJS

**3. 蓝队工具**
- 使用 -binwalk 选项安装 binwalk 环境
- 使用 -binwalk-f 选项强制安装 binwalk 环境 (建议在 -binwalk 选项失败的情况下运行)
- 使用 -clamav 选项安装 ClamAV 工具
- 使用 -lt 选项部署 LogonTracer 环境 (非超高配置机器不要部署,这个应用太吃配置了)
- 使用 -suricata 选项部署 Suricata 环境
- 使用 -vol 选项安装 volatility 取证工具
- 使用 -vol3 选项安装 volatility3 取证工具

**4. 红队工具**
- 使用 -aircrack 选项部署 aircrack-ng 环境
- 使用 -bypass 选项部署 Bypass 环境
- 使用 -goby 选项部署 Goby 环境 (需要图形化环境)
- 使用 -wpscan 选项安装 wpscan 工具
- 使用 -yakit 选项部署 yakit 环境

**5. 红队基础设施**
- 使用 -awvs14 选项部署 AWVS13 环境(1.04 GB)
- 使用 -cs 选项部署 CobaltStrike4.3 环境
- 使用 -cs45 选项部署 CobaltStrike4.5 环境
- 使用 -frp 选项部署 frp 工具
- 使用 -interactsh 选项部署 interactsh 工具 (https://github.com/projectdiscovery/interactsh)
- 使用 -merlin 选项部署 merlin 环境 (https://github.com/Ne0nd0g/merlin)
- 使用 -msf 选项部署 Metasploit 环境
- 使用 -nps 选项部署 nps 工具
- 使用 -pupy 选项部署 pupy 环境 (https://github.com/n1nj4sec/pupy)
- 使用 -rg 选项部署 RedGuard 工具 (https://github.com/wikiZ/RedGuard)
- 使用 -sliver 选项部署 sliver 环境 (https://github.com/BishopFox/sliver)
- 使用 -sliver-client 选项安装 sliver-client 工具
- 使用 -sps 选项部署 SharPyShell 工具 (https://github.com/antonioCoco/SharPyShell)
- 使用 -viper 选项部署 Viper 环境(2.1 GB)

**6. 基于 Docker 的环境部署**
- 使用 -arl 选项部署 ARL 环境(872 MB)
- 使用 -mobsf 选项部署 MobSF 环境(1.54 GB)
- 使用 -nodejsscan 选项部署 nodejsscan 环境(873 MB)
- 使用 -vulhub 选项部署 vulhub 环境(210 MB)
- 使用 -vulfocus 选项部署 vulfocus 环境(1.04 GB)
- 使用 -TerraformGoat 选项部署 TerraformGoat 环境

**7. 杂项服务**
- 使用 -asciinema 选项安装 asciinema 截图工具
- 使用 -bt 选项部署宝塔服务
- 使用 -clash 选项安装 clash 工具 (https://github.com/juewuy/ShellClash)
- 使用 -nginx 选项配置 nginx 服务
- 使用 -ssh 选项配置 ssh 环境 (RedHat 系默认可用,无需重复安装)
- 使用 -ssr 选项部署 ssr 工具
- 使用 -zsh 选项部署 zsh 工具

**8. 其他**
- 使用 -clear 选项清理系统使用痕迹
- 使用 -info 选项查看系统各项信息
- 使用 -optimize 选项改善设备选项,优化性能
- 使用 -remove 选项卸载国内 vps 云监控
- 使用 -rmlock 选项运行除锁模块
- 使用 -swap 选项配置 swap 分区
- 使用 -update 选项更新 f8x 工具
- 使用 -upgrade 选项更新渗透工具

---

## 实际效果

**-h 查看帮助**

<h3 align="center">
  <img src="https://github.com/ffffffff0x/f8x/raw/main/assets/img/1.png"></a>
</h3>

**-all 全自动化部署**

以 vultr vps 为例,结果分别如下

| <br><b><p align="center">CentOS 7(完全兼容)</p> | <br><b><p align="center">Debian 10(完全兼容)</p> |
| - | - |
| <p align="center"><a href="https://asciinema.org/a/WTGNRBd9WYLHUOgZcce9sjkeY"><img src="https://asciinema.org/a/WTGNRBd9WYLHUOgZcce9sjkeY.svg" /></p></a> | <p align="center"><a href="https://asciinema.org/a/Mq0N07O9K2jWsDuUoukHTEVOt"><img src="https://asciinema.org/a/Mq0N07O9K2jWsDuUoukHTEVOt.svg" /></p></a> |
| <br><b><p align="center">Fedora 33</p> | <br><b><p align="center">Ubuntu 20.10</p> |
| <p align="center"><a href="https://asciinema.org/a/NccoFLvW5Xcl0PW0HnTu32vHf"><img src="https://asciinema.org/a/NccoFLvW5Xcl0PW0HnTu32vHf.svg" /></p></a> | <p align="center"><a href="https://asciinema.org/a/Us90ody5ffAOIrr9p93dmO8Ct"><img src="https://asciinema.org/a/Us90ody5ffAOIrr9p93dmO8Ct.svg" /></p></a> |


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-11-30 发布视频[《f8x：红/蓝队环境自动化部署工具》](https://mp.weixin.qq.com/s/9MMujhu4PwmRvg0k7hPPUg)

## 最近更新

#### [v1.6.2] - 2022-09-04

**兼容性**  
- 支持 CentOS 9 Stream  
- 支持 Fedora 36  

**功能添加**  
- -k 选项添加 iprange/dnsx/MoreFind  
- 添加 -wpscan/-cs45-interactsh/等 选项  

**功能修改与优化**  
- 优化对docker环境的判断  
- 添加了对ruby的检测  
- 优化了对keytool工具的判断

#### [v1.6.1] - 2022-06-06

**兼容性**  
- 支持 ubuntu 22.04  

**功能添加**  
- -k 选项添加 CDK- 添加 -yakit 选项- 添加 -py310 选项- 添加 -oraclejdk11 选项- 添加 -docker 选项 (安装docker)- 添加 -code 选项 (安装 code-server)  

**功能修改与优化**  
- bat 换成兼容更强的安装包- 目前 -py3(7/8/9/10) 选项调用 pyenv 进行 python3 版本的切换,无需重复安装- 目前 -oraclejdk(8/11) 选项调用 jenv 进行 java 版本的切换,无需重复安装  

**错误修复**  
- 修改一些拼写错误

#### [v1.6.0] - 2022-03-11

**兼容性**  
- 支持 linux arm 架构  
- 支持 kali 2022.1  

**功能添加**  
- -k 选项添加 netspy  
- -f 选项添加 duf/procs/ncdu/exa/htop/bat/fd  

**错误修复**  
- 修复更改py版本时没有更改环境变量的问题

#### [v1.5.9] - 2021-12-10

**功能添加**  
- k 选项添加 htpwdScan,WebCrack,ysomap,sttr  

**功能修改与优化**  
- git clone 加入 --depth 1

#### [v1.5.8] - 2021-11-12

**功能修改与优化**  
- 兼容 Ubuntu 21.10 impish  
- 兼容 AlmaLinux  
- 兼容 Fedora 35  
- 兼容 CentOS 8 Stream  
- 兼容 VzLinux  
- 兼容 Rocky  
- python3 选项改为 -py3(7/8/9)  
- python2 选项改为 -py2

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
