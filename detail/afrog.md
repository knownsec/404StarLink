## afrog <https://github.com/zan8in/afrog>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-zan8in-orange)
![GitHub stars](https://img.shields.io/github/stars/zan8in/afrog.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1.1-red)
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

#### [v2.0.0] - 2022-11-10

**更新**  
- 修复 afrog 后台执行命令失败 BUG  
- 优化 afrog 稳定性，完善 URL 存活验证和扫描进度检查  
- 优化 afrog 用户体验，控制台进度显示新增 hosts、closed、time  
- 修复 target 黑名单逻辑判断不严谨导致的严重漏洞

#### [v1.3.9] - 2022-10-18

**更新**  
- 新增 参数 --ss / --scan-stable(值越大扫描越稳定)  
- 新增 参数 --pp / --printpocs 打印 PoC 列表  
- 更新 指纹库 web_fingerprint_v3  
- 解决 控制台 URL 打印不完整 BUG  
- 解决 部分 PoC BUG

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
