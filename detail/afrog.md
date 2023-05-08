## afrog <https://github.com/zan8in/afrog>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-zan8in-orange)
![GitHub stars](https://img.shields.io/github/stars/zan8in/afrog.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.3.1-red)
![Time](https://img.shields.io/badge/Join-20220615-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## What is afrog

afrog is an excellent performance, fast and stable, PoC customizable vulnerability scanning (hole digging) tool. PoC involves CVE, CNVD, default password, information leakage, fingerprint identification, unauthorized access, arbitrary file reading, command execution, etc. It helps network security practitioners quickly verify and fix vulnerabilities in a timely manner.

## Features

* [x] Open Source
* [x] Fast, stable, low false positives
* [x] Detailed html vulnerability report
* [x] PoC can be customized and updated stably
* [x] Active community exchange group

## Example

Basic usage
```
# Scan a target
afrog -t http://127.0.0.1

# Scan multiple targets
afrog -T urls.txt

# Specify a scan report file
afrog -t http://127.0.0.1 -o result.html
```

Advanced usage

```
# Test PoC 
afrog -t http://127.0.0.1 -P ./test/ 
afrog -t http://127.0.0.1 -P ./test/demo.yaml 

# Scan by PoC Keywords 
afrog -t http://127.0.0.1 -s tomcat,springboot,shiro 

# Scan by PoC Vulnerability Severity Level 
afrog -t http://127.0.0.1 -S high,critical 

# Online update afrog-pocs 
afrog -up 

# Disable fingerprint recognition 
afrog -t http://127.0.0.1 -nf
```

## Screenshot

![](https://github.com/zan8in/afrog/raw/main/images/scan-new.png)

![](https://github.com/zan8in/afrog/raw/main/images/report-new.png)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v2.3.1] - 2023-05-05

**BUG**  
- 解决`版本检查`导致内网无法使用问题  

**新增**  
- 命令 -disable-update-check，-duc 禁用自动更新检查  

**修改**  
- 现在 update-poc 会自动执行，禁用这个功能，请使用 -duc 命令

#### [v2.3.0] - 2023-05-02

**新增**  
- 命令 `poc-detail/pd`，查看 poc 详情  
- 命令 `monitor-targets/mt`，在扫描中实时监控目标存活  

**优化**  
- 命令 `poc-list/pl`，查看 poc 列表

#### [v2.2.3] - 2023-04-22

**优化**  
- 可自定义 html report 报告生成目录  

**PoC**  
- 新增 22 PoC

#### [v2.2.2] - 2023-04-05

**修复**  
- 修复 afrog html 报告 XSS 漏洞  

**优化**  
- 简化 URL 黑名单机制  
- 优化 http/s 检测功能  
- 优化 文件上传 (所有) PoC  
- 优化 RCE (所有) PoC  

**删除**  
- 去掉 Fingerprint 指纹识别及命令参数 (替代工具 pyxis)  
- 去掉不常用命令参数  

**PoC**  
- 新增 52 PoC  
- 验证和优化 n 多个 PoC  
- 删除 PoC csz-cms-multiple-blind-sql-injection  
- 删除 PoC phpstudy-nginx-wrong-resolve  
- 内置几个 private PoC

#### [v2.2.1] - 2023-02-04

**更新**  
- 将多个 panel 指纹探测合并到文件 panel-detect.yaml，大幅减少 http 请求  
- 精简控制台日期打印，2023-01-01 改为 01-01  
- 精简 afrog-config 配置信息  

**修复**  
- 解决：-fc 命令配置无效问题  
- 提示：配置 -c 命令能明显提高扫描速度

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
