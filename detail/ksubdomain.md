## ksubdomain <https://github.com/boy-hack/ksubdomain>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-w8ay-orange)
![GitHub stars](https://img.shields.io/github/stars/boy-hack/ksubdomain.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.8.1-red)
![Time](https://img.shields.io/badge/Join-20200821-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


ksubdomain是一款基于无状态的子域名爆破工具，类似无状态端口扫描，支持在Windows/Linux/Mac上进行快速的DNS爆破，拥有重发机制不用担心漏包。

hacking8信息流的src资产收集 https://i.hacking8.com/src/ 用的是ksubdomain

![](https://github.com/boy-hack/ksubdomain/raw/main/image.gif)
## 安装
1. 下载二进制 https://github.com/boy-hack/ksubdomain/releases
2. 安装libpcap环境
   - Windows
     下载`winpcap`驱动:https://www.winpcap.org/install/default.htm
   - Linux
     已经静态编译打包libpcap，无需其他操作
   - MacOS
     自带libpcap,无需其他操作
3. 执行!

## Useage
```bash
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
提供完整的域名列表，ksubdomain负责快速获取结果

```bash
./ksubdomain verify -h

NAME:
   cmd verify - 验证模式

USAGE:
   cmd verify [command options] [arguments...]

OPTIONS:
   --filename value, -f value   验证域名文件路径
   --band value, -b value       宽带的下行速度，可以5M,5K,5G (default: "2m")
   --resolvers value, -r value  dns服务器文件路径，一行一个dns地址
   --output value, -o value     输出文件名
   --silent                     使用后屏幕将仅输出域名 (default: false)
   --retry value                重试次数,当为-1时将一直重试 (default: 3)
   --timeout value              超时时间 (default: 6)
   --stdin                      接受stdin输入 (default: false)
   --only-domain, --od          只打印域名，不显示ip (default: false)
   --not-print, --np            不打印域名结果 (default: false)
   --help, -h                   show help (default: false)
```

```
从文件读取 
./ksubdomain v -f dict.txt

从stdin读取
echo "www.hacking8.com"|./ksubdomain v --stdin
```

**枚举模式**
只提供一级域名，指定域名字典或使用ksubdomain内置字典，枚举所有二级域名

```bash
./ksubdomain enum -h

NAME:
   cmd enum - 枚举域名

USAGE:
   cmd enum [command options] [arguments...]

OPTIONS:
   --band value, -b value          宽带的下行速度，可以5M,5K,5G (default: "2m")
   --resolvers value, -r value     dns服务器文件路径，一行一个dns地址
   --output value, -o value        输出文件名
   --silent                        使用后屏幕将仅输出域名 (default: false)
   --retry value                   重试次数,当为-1时将一直重试 (default: 3)
   --timeout value                 超时时间 (default: 6)
   --stdin                         接受stdin输入 (default: false)
   --only-domain, --od             只打印域名，不显示ip (default: false)
   --not-print, --np               不打印域名结果 (default: false)
   --domain value, -d value        爆破的域名
   --domainList value, --dl value  从文件中指定域名
   --filename value, -f value      字典路径
   --skip-wild                     跳过泛解析域名 (default: false)
   --level value, -l value         枚举几级域名，默认为2，二级域名 (default: 2)
   --level-dict value, --ld value  枚举多级域名的字典文件，当level大于2时候使用，不填则会默认
   --help, -h                      show help (default: false)
```

```
./ksubdomain e -d baidu.com

从stdin获取
echo "baidu.com"|./ksubdomain e --stdin
```

## 特性和Tips

- 无状态爆破，有失败重发机制，速度极快
- 中文帮助，-h会看到中文帮助
- 两种模式，枚举模式和验证模式，枚举模式内置10w字典
- 将网络参数简化为了-b参数，输入你的网络下载速度如-b 5m，将会自动限制网卡发包速度。
- 可以使用./ksubdomain test来测试本地最大发包数
- 获取网卡改为了全自动并可以根据配置文件读取。
- 会有一个时时的进度条，依次显示成功/发送/队列/接收/失败/耗时 信息。
- 不同规模的数据，调整 --retry --timeout参数即可获得最优效果
- 当--retry为-1，将会一直重试直到所有成功。

## 与massdns、dnsx对比

使用100w字典，在4H5M的网络环境下测试

|          | ksubdomain                                                   | massdns                                                      | dnsx                                                         |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 支持系统 | Windows/Linux/Darwin                                         | Windows/Linux/Darwin                                         | Windows/Linux/Darwin                                         |
| 功能 | 支持验证和枚举 | 只能验证 | 只能验证 |
| 发包方式 | pcap网卡发包                                                 | epoll,pcap,socket                                            | socket                                                       |
| 命令行 | time ./ksubdomain v -b 5m -f d2.txt -o ksubdomain.txt -r dns.txt --retry 3 --np | time ./massdns -r dns.txt -t AAAA -w massdns.txt d2.txt --root -o L | time ./dnsx -a -o dnsx.txt -r dns.txt -l d2.txt -retry 3 -t 5000 |
| 备注   | 加了--np 防止打印过多                                        |                                                              |                                                              |
| 结果   | 耗时:1m28.273s<br />成功个数:1397                            | 耗时:3m29.337s<br />成功个数:1396                            | 耗时:5m26.780s <br />成功个数:1396                           |

ksubdomain只需要1分半，速度远远比massdns、dnsx快~


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2020-09-02 发布文章[《ksubdomain 无状态域名爆破工具》](https://paper.seebug.org/1325/)
- 2019-10-12 发布文章[《从 Masscan, Zmap 源码分析到开发实践》](https://paper.seebug.org/1052/)

## 最近更新

#### [v1.8.1] - 2022-02-13

**重构**  
- 优化了代码结构，优化了go协程组织方式，代码易懂，解决了一些冲突问题  
- 设计了一种新的算法，用来快速发包并且大大减少失败率  
- 获取网卡改为了全自动并可以根据配置文件读取  
- 增加有一个实时的进度条，依次显示成功/发送/队列/接收/失败/耗时信息

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
