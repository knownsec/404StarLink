## afrog <https://github.com/zan8in/afrog>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-zan8in-orange)
![GitHub stars](https://img.shields.io/github/stars/zan8in/afrog.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.2.1-red)
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

#### [v2.2.1] - 2023-02-04

**更新**  
- 将多个 panel 指纹探测合并到文件 panel-detect.yaml，大幅减少 http 请求  
- 精简控制台日期打印，2023-01-01 改为 01-01  
- 精简 afrog-config 配置信息  

**修复**  
- 解决：-fc 命令配置无效问题  
- 提示：配置 -c 命令能明显提高扫描速度

#### [v2.2.0] - 2023-01-07

**更新**  
- 新增仅指纹扫描选项 `-onlyfinger`  
- 新增 CEL 函数，如 year/shortyear 等  
- 新增 PoC 验证属性，默认为 false  
- 新增规则属性表达式

#### [v2.1.1] - 2022-12-22

**更新**  
- 修复了指纹中误报率高的bug  
- 添加 -json 选项，用于 json 格式输出

#### [v2.1.0] - 2022-12-12

**更新**  
- 新增 -update 将 afrog 引擎更新到最新发布的版本  
- 新增 -proxy 使用 http/socks5 代理列表(逗号分隔或文件输入)  
- 新增 -rate-limit、concurrency、fingerprint-concurrency、max-host-error、retries、timeout 等参数  
- 修复 html 报告(返回多个请求记录)URL 不准确的 BUG  
- 优化 banner 展示界面(模仿 nuclei)  
- 屏蔽 GoPoc 功能(暂时)

#### [v2.0.1] - 2022-11-30

**更新**  
- 紧急发布修复 BUG 的小版本  
- 解决 afrog 线程池经常卡死 BUG

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
