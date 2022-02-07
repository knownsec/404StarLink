## ksubdomain <https://github.com/boy-hack/ksubdomain>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-w8ay-orange)
![GitHub stars](https://img.shields.io/github/stars/boy-hack/ksubdomain.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.2-red)
![Time](https://img.shields.io/badge/Join-20200821-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


ksubdomain是一款基于无状态的子域名爆破工具，类似无状态端口扫描，支持在Windows/Linux/Mac上进行快速的DNS爆破，在Mac和Windows上理论最大发包速度在30w/s,linux上为160w/s。

hacking8信息流的src资产收集 https://i.hacking8.com/src/ 用的是ksubdomain

## Useage
```bash
w8ay@MacBook-Pro  ~/programs/ksubdomain   main ●  ./ksubdomain

NAME:
   KSubdomain - 无状态子域名爆破工具

USAGE:
   ksubdomain [global options] command [command options] [arguments...]

VERSION:
   1.4

COMMANDS:
   enum, e    枚举域名
   verify, v  验证模式
   test       测试本地网卡的最大发送速度
   help, h    Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --help, -h     show help (default: false)
   --version, -v  print the version (default: false)

```

### 模式
**验证模式**

提供完整的域名列表，ksubdomain负责快速从dns服务器获取结果 
```
./ksubdomain v -f dict.txt
或
echo "www.hacking8.com"|./ksubdomain v --stdin
```
**枚举模式**

只提供一级域名，指定域名字典或使用ksubdomain内置字典，枚举所有二级域名
```
./ksubdomain e -f dict.txt
或
echo "baidu.com"|./ksubdomain e --stdin
```


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2020-09-02 发布文章[《ksubdomain 无状态域名爆破工具》](https://paper.seebug.org/1325/)
- 2019-10-12 发布文章[《从 Masscan, Zmap 源码分析到开发实践》](https://paper.seebug.org/1052/)

## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
