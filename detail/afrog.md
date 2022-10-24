## afrog <https://github.com/zan8in/afrog>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-zan8in-orange)
![GitHub stars](https://img.shields.io/github/stars/zan8in/afrog.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.3.9-red)
![Time](https://img.shields.io/badge/Join-20220615-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## 什么是 afrog

afrog 是一款性能卓越、快速稳定、PoC 可定制的漏洞扫描工具，PoC 包含 CVE、CNVD、默认口令、信息泄露、指纹识别、未授权访问、任意文件读取、命令执行等多种漏洞类型，帮助网络安全从业者快速验证并及时修复漏洞。

## 特点

* [x] 开源
* [x] 快速、稳定、误报低
* [x] 详细的 html 漏洞报告
* [x] PoC 可定制化、稳定更新
* [x] 活跃的社区 [交流群](https://github.com/zan8in/afrog#%E4%BA%A4%E6%B5%81%E7%BE%A4)
* [x] 长期维护

## 示例

基本用法
```
# 扫描一个目标
afrog -t http://127.0.0.1

# 扫描多个目标
afrog -T urls.txt

# 指定漏扫报告文件
afrog -t http://127.0.0.1-o result.html
```

高级用法

```
# 测试 PoC 
afrog -t http://127.0.0.1 -P ./test/ 
afrog -t http://127.0.0.1 -P ./test/demo.yaml 

# 按 PoC 关键字扫描 
afrog -t http://127.0.0.1 -s tomcat,springboot,shiro 

# 按 Poc 漏洞等级扫描 
afrog -t http://127.0.0.1 -S high,critical 

# 在线更新 afrog-pocs 
afrog --up 

# 禁用指纹识别，直接漏扫 
afrog -t http://127.0.0.1 --nf
```

## 截图
控制台
![](https://github.com/zan8in/afrog/blob/main/images/scan-new.png)
html 报告
![](https://github.com/zan8in/afrog/blob/main/images/report-new.png)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.3.9] - 2022-10-18

**更新**  
- 新增 参数 --ss / --scan-stable(值越大扫描越稳定)  
- 新增 参数 --pp / --printpocs 打印 PoC 列表  
- 更新 指纹库 web_fingerprint_v3  
- 解决 控制台 URL 打印不完整 BUG  
- 解决 部分 PoC BUG

#### [v1.3.8] - 2022-09-15

**更新**  
- 升级到 Golang 1.19  
- 升级到最新 Fingerprint 指纹库  
- 修复程序卡进度 99% 问题  
- 修改 pocsizewaitgroup 默认值为 25  
- afrog-config.yaml 一经生成不会被覆盖  
- 修改 dial_timeout/read_timeout/write_timeout 等参数的默认值  
- 优化 PoC nacos-v1-auth-bypass/solr-log4j-rce.yaml/CVE-2021-26084  
- 累计 PoC 总数 684

#### [v1.3.7] - 2022-08-24

**更新**  
- 新增 socks/http(s) 代理  
- 优化并发机制，牺牲扫描速度，减少漏报  
- 修复自定义UA 失效问题  
- 优化部分 PoC 调低漏洞等级  
- 删除 PoC rsync-unauth

#### [v1.3.6] - 2022-07-24

**更新**  
- add Gitee 更新 afrog-pocs  
- add 自动识别 http(s)  
- add target 存活验证  
- add Console Print 实时显示指纹识别结果  
- update 更新 fingerprint 指纹库  
- fixed 解决 gbk 编码导致 PoC 漏报问题  
- bug 修复 GoPoC Console Print 不显示 target  
- delete tongda-insert-sql-inject poc  
- poc 新增 PoC 33 个，共 656 个

#### [v1.3.5] - 2022-07-10

**新增**  
- 支持 go 语言 PoC 开发  
- 新增 夏日清爽皮肤 漏洞报告模板  
- console print 漏洞会显示完整 URL  
- 新增 72 个 PoC，共 626 个 PoC  

**BUG**  
- 修复 tongda-insert-sql-inject.yaml 误报 BUG  
- 修复 landray-oa-syssearchmain-rce.yaml 误报 BUG

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
