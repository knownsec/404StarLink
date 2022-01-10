## ksubdomain <https://github.com/knownsec/ksubdomain>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-w7ay-orange)
![GitHub stars](https://img.shields.io/github/stars/knownsec/ksubdomain.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.7-red)
![Time](https://img.shields.io/badge/Join-20200821-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


ksubdomain是一款基于无状态子域名爆破工具，支持在Windows/Linux/Mac上使用，它会很快的进行DNS爆破，在Mac和Windows上理论最大发包速度在30w/s,linux上为160w/s的速度。
## 为什么这么快
ksubdomain的发送和接收是分离且不依赖系统，即使高并发发包，也不会占用系统描述符让系统网络阻塞。

可以用`--test`来测试本地最大发包数,但实际发包的多少和网络情况息息相关，ksubdomain将网络参数简化为了`-b`参数，输入你的网络下载速度如`-b 5m`，ksubdomain将会自动限制发包速度。
## 可靠性
类似masscan,这么大的发包速度意味着丢包也会非常严重，ksubdomain有丢包重发机制(这样意味着速度会减小，但比普通的DNS爆破快很多)，会保证每个包都收到DNS服务器的回复，漏报的可能性很小。

## 使用
从[releases](https://github.com/knownsec/ksubdomain/releases "releases")下载二进制文件。 

在linux下，还需要安装`libpcap-dev`,在Windows下需要安装`WinPcap`，mac下可以直接使用。
```
 _  __   _____       _         _                       _
| |/ /  / ____|     | |       | |                     (_)
| ' /  | (___  _   _| |__   __| | ___  _ __ ___   __ _ _ _ __
|  <    \___ \| | | | '_ \ / _| |/ _ \| '_   _ \ / _  | | '_ \
| . \   ____) | |_| | |_) | (_| | (_) | | | | | | (_| | | | | |
|_|\_\ |_____/ \__,_|_.__/ \__,_|\___/|_| |_| |_|\__,_|_|_| |_|

[INFO] Current Version: 0.7
Usage of ./cmd:
  -api
        使用网络接口
  -b string
        宽带的下行速度，可以5M,5K,5G (default "1M")
  -check-origin
        会从返回包检查DNS是否为设定的，防止其他包的干扰
  -csv
        输出excel文件
  -d string
        爆破域名
  -dl string
        从文件中读取爆破域名
  -e int
        默认网络设备ID,默认-1，如果有多个网络设备会在命令行中选择 (default -1)
  -f string
        字典路径,-d下文件为子域名字典，-verify下文件为需要验证的域名
  -filter-wild
        自动分析并过滤泛解析，最终输出文件，需要与'-o'搭配
  -full
        完整模式，使用网络接口和内置字典
  -l int
        爆破域名层级,默认爆破一级域名 (default 1)
  -list-network
        列出所有网络设备
  -o string
        输出文件路径
  -s string
        resolvers文件路径,默认使用内置DNS
  -sf string
        三级域名爆破字典文件(默认内置)
  -silent
        使用后屏幕将仅输出域名
  -skip-wild
        跳过泛解析的域名
  -summary
        在扫描完毕后整理域名归属asn以及IP段
  -test
        测试本地最大发包数
  -ttl
        导出格式中包含TTL选项
  -verify
        验证模式

```
### 常用命令
```
使用内置字典爆破
ksubdomain -d seebug.org

使用字典爆破域名
ksubdomain -d seebug.org -f subdomains.dict

字典里都是域名，可使用验证模式
ksubdomain -f dns.txt -verify

爆破三级域名
ksubdomain -d seebug.org -l 2

通过管道爆破
echo "seebug.org"|ksubdomain

通过管道验证域名
echo "paper.seebug.org"|ksubdomain -verify

仅使用网络API接口获取域名
ksubdomain -d seebug.org -api

完整模式,先使用网络API，在此基础使用内置字典进行爆破
ksubdomain -d seebug.org -full
```
[![asciicast](https://asciinema.org/a/356138.svg)](https://asciinema.org/a/356138)
## Summary整理
ksubdomain加入了整理的功能，当参数后面加上`-summary`。

例如`ksubdomain -d seebug.org -summary`之后，会根据域名归属的asn以及IP段自动整理输出，方便确认资产的范围。

![WX20200904-164515](https://github.com/knownsec/ksubdomain/raw/master/images/WX20200904-164515.png)


## 管道操作
借助知名的`subfinder`，`httpx`等工具，可以用管道结合在一起配合工作。达到收集域名，验证域名，http验证存活目的。
```bash
./subfinder -d baidu.com -silent|./ksubdomain -verify -silent|./httpx -title -content-length -status-code
```
- subfinder 通过各种搜索引擎获取域名
- ksubdomain 验证域名
- httpx http请求获得数据,验证存活
![image-20200902160128305](https://github.com/knownsec/ksubdomain/raw/master/images/image-20200902160128305.png)

## 编译
因为pcap包的特殊性，无法交叉编译，只能每个系统编译每个文件。
```bash
git clone https://github.com/knownsec/ksubdomain
cd ksubdomain
go mod download
cd cmd
go build ksubdomain.go
```

## Script编写
Ksubdomain 网络API引擎脚本使用`lua`，文件路径在`resources/scripts`  
![WX20200904-164515](https://github.com/knownsec/ksubdomain/raw/master/images/WX20210112-175029.png)
```lua 
name = "Sublist3rAPI" -- * 插件名称(必须)
type = "api" -- 插件类型(不必须)

local json = require("json")

function buildurl(domain)
    return "https://api.sublist3r.com/search.php?domain=" .. domain
end

-- 需要实现一个vertical函数，返回类型为一个域名的table，如果失败可以返回nil
function vertical(domain)
    local page, err = request({url=buildurl(domain)})
    if (err ~= nil and err ~= "") then
        return
    end
    local resp = json.decode(page)
    if (resp == nil or #resp == 0) then
        return
    end
    local a = {}
    for i, v in pairs(resp) do
        table.insert(a, v)
    end
    return a
end
```
在编写插件完毕后，打包文件
```bash
statik -src=resources
```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2020-09-02 发布文章[《ksubdomain 无状态域名爆破工具》](https://paper.seebug.org/1325/)
- 2019-10-12 发布文章[《从 Masscan, Zmap 源码分析到开发实践》](https://paper.seebug.org/1052/)

## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
