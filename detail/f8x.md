## f8x <https://github.com/ffffffff0x/f8x>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Bash-blue)
![Author](https://img.shields.io/badge/Author-ffffffff0x-orange)
![GitHub stars](https://img.shields.io/github/stars/ffffffff0x/f8x.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.9-red)
![Time](https://img.shields.io/badge/Join-20210223-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


一款红/蓝队环境自动化部署工具,支持多种场景,渗透,开发,代理环境,服务可选项等。

大多数场景下，在不同的云购买一些 vps 服务器用于部署红 / 蓝队设施，不能做到开箱即用，使用此工具可以快速部署所需要的各类服务。同时兼顾到本地 VM 虚拟机的需求，可以选择走 socket 代理进行安装部署，Proxychains-ng 也会自动安装，只需做好 Proxychains-ng 配置即可。

## 开始

**下载**

- 访问 [releases](https://github.com/ffffffff0x/f8x/releases) 下载

- 在网络不佳的情况下通过 CF Workers 加速下载
  - wget : `wget -O f8x https://f8x.io/`
  - curl : `curl -o f8x https://f8x.io/`

**使用**
```bash
bash f8x -h
```

如果你希望方便点使用可以直接加到环境变量中
- wget : `wget -O f8x https://f8x.io/ && mv --force f8x /usr/local/bin/f8x && chmod +x /usr/local/bin/f8x`
  - `f8x -help`
- curl : `curl -o f8x https://f8x.io/ && mv --force f8x /usr/local/bin/f8x && chmod +x /usr/local/bin/f8x`
  - `f8x -help`

**系统依赖**

f8x 基本上不需要任何依赖,或者说它就是为了帮助你安装各种依赖而生的😁

**f8x-ctf**

该脚本用于部署 CTF 环境,支持 (Web、Misc、Crypto、Pwn、Iot) 分类

- wget : `wget -O f8x-ctf https://f8x.io/ctf`
  - `bash f8x-ctf -help`
- curl : `curl -o f8x-ctf https://f8x.io/ctf`
  - `bash f8x-ctf -help`

**f8x-dev**

部分开发环境安装独立到该脚本,如 tomcat、redis 不同版本的部署

- wget : `wget -O f8x-dev https://f8x.io/dev`
  - `bash f8x-dev -help`
- curl : `curl -o f8x-dev https://f8x.io/dev`
  - `bash f8x-dev -help`

## 支持选项

目前 f8x 支持以下部署选项

**1. 批量化安装**
- 使用 -b 选项安装基本环境        (gcc、make、git、vim、telnet、jq、unzip 等基本工具)
- 使用 -p 选项安装代理环境        (警告:国外云服务器上不要用,会降速)
- 使用 -d 选项安装开发环境        (python3、pip3、Go、Docker、Docker-Compose、SDKMAN)
- 使用 -k 选项安装渗透环境        (hashcat、ffuf、OneForAll、ksubdomain、impacket 等渗透工具)
  - -k -a 信息收集、扫描、爆破、抓取
  - -k -b 漏洞利用
  - -k -c 后渗透、C2
  - -k -d 其他
  - -k -e 功能重叠或长期不维护
- 使用 -s 选项安装蓝队环境        (Fail2Ban、chkrootkit、rkhunter、河马webshell查杀工具)
- 使用 -f 选项安装其他工具        (Bash_Insulter、vlmcsd、AdguardTeam、trash-cli 等辅助工具)
- 使用 -cloud 选项安装云应用      (Terraform、Serverless Framework、wrangler)
- 使用 -all 选项全自动化部署      (默认不走代理,兼容 CentOS7/8,Debain10/9,Ubuntu20/18,Fedora33)

**2. 开发环境**

- 使用 -lua 选项安装 lua 环境
- 使用 -nn 选项安装 npm & NodeJs 环境
- 使用 -oraclejdk 选项安装 oraclejdk 环境
- 使用 -openjdk 选项安装 openjdk 环境
- 使用 -python3 选项安装 python3 环境
- 使用 -python2 选项安装 python2 环境
- 使用 -pip2-f 选项强制安装 pip2 环境          (建议在 -python2 选项失败的情况下运行)
- 使用 -perl 选项安装 perl 环境
- 使用 -ruby 选项安装 ruby 环境
- 使用 -rust 选项安装 rust 环境
- 使用 -chromium 选项安装 Chromium 环境        (用于配合 -k 选项中的 rad、crawlergo)

**3. 蓝队服务**

- 使用 -binwalk 选项安装 binwalk 环境
- 使用 -binwalk-f 选项强制安装 binwalk 环境    (建议在 -binwalk 选项失败的情况下运行)
- 使用 -clamav 选项安装 ClamAV 工具
- 使用 -hfish 选项安装 HFish 蜜罐
- 使用 -lt 选项部署 LogonTracer 环境           (非超高配置机器不要部署,这个应用太吃配置了)
- 使用 -suricata 选项部署 Suricata 环境
- 使用 -vol 选项安装 volatility 取证工具
- 使用 -vol3 选项安装 volatility3 取证工具

**4. 红队服务**

- 使用 -aircrack 选项部署 aircrack-ng 环境
- 使用 -bypass 选项部署 Bypass 环境
- 使用 -cs 选项部署 CobaltStrike 环境
- 使用 -frp 选项部署 frp 环境
- 使用 -goby 选项部署 Goby 环境                (需要图形化环境)
- 使用 -nps 选项部署 nps 环境

**5. 基于 Docker 的环境部署**

- 使用 -arl 选项部署 ARL 环境(872 MB)
- 使用 -awvs14 选项部署 AWVS13 环境(1.04 GB)
- 使用 -mobsf 选项部署 MobSF 环境(1.54 GB)
- 使用 -nodejsscan 选项部署 nodejsscan 环境(873 MB)
- 使用 -viper 选项部署 Viper 环境(2.1 GB)
- 使用 -vulhub 选项部署 vulhub 环境(210 MB)
- 使用 -vulfocus 选项部署 vulfocus 环境(1.04 GB)

**6. 杂项服务**

- 使用 -asciinema 选项安装 asciinema 截图工具
- 使用 -bt 选项部署宝塔服务
- 使用 -clash 选项安装 clash 工具
- 使用 -music 选项部署 UnblockNeteaseMusic 服务
- 使用 -nginx 选项配置 nginx 服务
- 使用 -ssh 选项配置 ssh 环境                  (RedHat 系默认可用,无需重复安装)
- 使用 -ssr 选项部署 ssr 工具
- 使用 -zsh 选项部署 zsh 工具

**7. 其他**

- 使用 -clear 选项清理系统使用痕迹
- 使用 -info 选项查看系统各项信息
- 使用 -optimize 选项改善设备选项,优化性能
- 使用 -remove 选项卸载国内 vps 云监控
- 使用 -rmlock 选项运行除锁模块
- 使用 -swap 选项配置 swap 分区
- 使用 -update 选项更新 f8x 工具
- 使用 -mock 选项单独调用某个模块

## 实际效果

**-h 查看帮助**

[](https://github.com/ffffffff0x/f8x/blob/main/assets/img/1.png)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-11-30 发布视频[《f8x：红/蓝队环境自动化部署工具》](https://mp.weixin.qq.com/s/9MMujhu4PwmRvg0k7hPPUg)

## 最近更新

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

#### [v1.5.6] - 2021-10-03

**功能修改**  
- 更新 crawlergo 的下载链接  
- 更改显示语言 #10 #11  
- 在安装 volatility3 时默认不会下载 Symbol Tables  
- 优化对已安装软件的检测,尽量避免重复安装  
- 修改一个重命名的bug  
- 移除 sharry 的安装选项  


<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
