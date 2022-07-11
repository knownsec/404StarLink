## afrog <https://github.com/zan8in/afrog>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-zan8in-orange)
![GitHub stars](https://img.shields.io/github/stars/zan8in/afrog.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.3.5-red)
![Time](https://img.shields.io/badge/Join-20220615-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## 什么是 afrog

afrog 是一款性能卓越、快速稳定、PoC 可定制的漏洞扫描工具，PoC 包含 CVE、CNVD、默认口令、信息泄露、指纹识别、未授权访问、任意文件读取、命令执行等多种漏洞类型，帮助网络安全从业者快速验证并及时修复漏洞。

## 特点

* [x] 基于 xray 内核，又不像 xray（[**afrog 模板语法**](https://github.com/zan8in/afrog/blob/main/pocs/afrog-pocs/README.md)）
* [x] 性能卓越，快速稳定
* [x] 实时显示，扫描进度
* [x] 输出 html 报告，方便查看 `request` 和 `response`
* [x] 启动程序，自动更新本地 PoC 库
* [x] 长期维护、更新 PoC（[**afrog-pocs**](https://github.com/zan8in/afrog/tree/main/pocs/afrog-pocs)）
* [x] 二次开发，参考 `cmd/afrog/main.go` 或加入 **[交流群](https://github.com/zan8in/afrog#%E4%BA%A4%E6%B5%81%E7%BE%A4)**

## 下载

### [下载地址](https://github.com/zan8in/afrog/releases)

## 使用指南

### [查看指南](https://github.com/zan8in/afrog/blob/main/GUIDE.md)

## 例子

扫描单个目标
```
afrog -t http://127.0.0.1 -o result.html
```
![](https://github.com/zan8in/afrog/raw/main/images/onescan.png)

扫描多个目标

```
afrog -T urls.txt -o result.html
```
例如：`urls.txt`
```
http://192.168.139.129:8080
http://127.0.0.1
```
![](https://github.com/zan8in/afrog/raw/main/images/twoscan.png)

测试单个 PoC 文件

```
afrog -t http://127.0.0.1 -P ./testing/poc-test.yaml -o result.html
```
![](https://github.com/zan8in/afrog/raw/main/images/threescan.png)

测试多个 PoC 文件

```
afrog -t http://127.0.0.1 -P ./testing/ -o result.html
```
![](https://github.com/zan8in/afrog/raw/main/images/fourscan.png)

输出 html 报告

![](https://github.com/zan8in/afrog/raw/main/images/2.png)

![](https://github.com/zan8in/afrog/raw/main/images/3.png)

## 如何贡献 PoC？

### [查看教程](https://github.com/zan8in/afrog/blob/main/CONTRIBUTION.md)

## PoC 列表
### [查看 PoC 列表](https://github.com/zan8in/afrog/blob/main/POCLIST.md)



<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

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
