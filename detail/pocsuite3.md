## pocsuite3 <https://github.com/knownsec/pocsuite3>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-knownsec404-orange)
![GitHub stars](https://img.shields.io/github/stars/knownsec/pocsuite3.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.9.5-red)
![Time](https://img.shields.io/badge/Join-20200821-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


## Legal Disclaimer
Usage of pocsuite3 for attacking targets without prior mutual consent is illegal.
pocsuite3 is for security testing purposes only

## 法律免责声明
未经事先双方同意，使用 pocsuite3 攻击目标是非法的。
pocsuite3 仅用于安全测试目的

## Overview

pocsuite3 is an open-sourced remote vulnerability testing and proof-of-concept development framework developed by the [**Knownsec 404 Team**](http://www.knownsec.com/). 
It comes with a powerful proof-of-concept engine, many nice features for the ultimate penetration testers and security researchers.

## Features
* PoC scripts can running with `verify`, `attack`, `shell` mode in different way
* Plugin ecosystem
* Dynamic loading PoC script from any where (local file, redis, database, Seebug ...)
* Load multi-target from any where (CIDR, local file, redis, database, Zoomeye, Shodan ...)
* Results can be easily exported
* Dynamic patch and hook requests 
* Both command line tool and python package import to use
* IPV6 support
* Global HTTP/HTTPS/SOCKS proxy support
* Simple spider API for PoC script to use
* Integrate with [Seebug](https://www.seebug.org) (for load PoC from Seebug website)
* Integrate with [ZoomEye](https://www.zoomeye.org) (for load target from ZoomEye `Dork`)
* Integrate with [Shodan](https://www.shodan.io) (for load target from Shodan `Dork`)
* Integrate with [Ceye](http://ceye.io/) (for verify blind DNS and HTTP request)
* Integrate with [Interactsh](https://github.com/projectdiscovery/interactsh) (for verify blind DNS and HTTP request)
* Integrate with Fofa (for load target from Fofa `Dork`)
* Friendly debug PoC scripts with IDEs
* More ...

## Screenshots

### pocsuite3 console mode
[![asciicast](https://asciinema.org/a/219356.png)](https://asciinema.org/a/219356)

### pocsuite3 shell mode
[![asciicast](https://asciinema.org/a/203101.png)](https://asciinema.org/a/203101)

### pocsuite3 load PoC from Seebug 
[![asciicast](https://asciinema.org/a/207350.png)](https://asciinema.org/a/207350)

### pocsuite3 load multi-target from ZoomEye
[![asciicast](https://asciinema.org/a/133344.png)](https://asciinema.org/a/133344)

### pocsuite3 load multi-target from Shodan
[![asciicast](https://asciinema.org/a/207349.png)](https://asciinema.org/a/207349)

## Requirements

- Python 3.6+
- Works on Linux, Windows, Mac OSX, BSD, etc.

## Installation

Paste at a terminal prompt:

### Python pip

``` bash
pip3 install pocsuite3

# use other pypi mirror
pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple pocsuite3
```

### MacOS

``` bash
brew update
brew info pocsuite3
brew install pocsuite3
```

### [Debian](https://tracker.debian.org/pkg/pocsuite3), [Ubuntu](https://launchpad.net/ubuntu/+source/pocsuite3), [Kali](http://pkg.kali.org/pkg/pocsuite3)

``` bash
sudo apt update
sudo apt install pocsuite3
```

### ArchLinux

``` bash
yay pocsuite3
```

###

Or click [here](https://github.com/knownsec/pocsuite3/archive/master.zip) to download the latest source zip package and extract

``` bash
$ wget https://github.com/knownsec/pocsuite3/archive/master.zip
$ unzip master.zip
$ cd pocsuite3-master
$ pip3 install -r requirements.txt
$ python3 setup.py install
```


The latest version of this software is available at: https://pocsuite.org

## Documentation

Documentation is available in the [```docs```](https://github.com/knownsec/pocsuite3/blob/master/docs) directory.

## Usage

```
cli mode

	# basic usage, use -v to set the log level
	pocsuite -u http://example.com -r example.py -v 2

	# run poc with shell mode
	pocsuite -u http://example.com -r example.py -v 2 --shell

	# search for the target of redis service from ZoomEye and perform batch detection of vulnerabilities. The thread is set to 20
	pocsuite -r redis.py --dork service:redis --threads 20

	# load all poc in the poc directory and save the result as html
	pocsuite -u http://example.com --plugins poc_from_pocs,html_report

	# load the target from the file, and use the poc under the poc directory to scan
	pocsuite -f batch.txt --plugins poc_from_pocs,html_report

	# load CIDR target
	pocsuite -u 10.0.0.0/24 -r example.py --plugins target_from_cidr

	# the custom parameters `command` is implemented in ecshop poc, which can be set from command line options
	pocsuite -u http://example.com -r ecshop_rce.py --attack --command "whoami"

console mode
    poc-console
```


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.9.5] - 2022-06-22

**更新**  
- 重构 --ppt 参数，优化 url 马赛克功能  
- 优化 poc 模板  
- 优化命令行默认提示信息  
- 调整默认超时为 10 秒  
- 调整默认线程数为 150  
- 目标 url 目前支持 CIDR，用户可使用 -p 指定端口  
- 支持本地模式，该模式化下 poc 不需要指定目标，比如本地提权漏洞  
- 修复部分 bugs

#### [v1.9.4] - 2022-06-07

**更新**  
- 支持 poc 模板生成(--new)  
- 支持自定义 interactsh 服务器设置  
- 修改 ZoomEye/Seebug/CEYE 认证方式为 APIKEY  
- poc 基类添加 check 方法，支持蜜罐识别和 http/https 协议自动纠正- 重构 --update 参数，优化框架更新流程  
- 支持对框架版本进行检测，提高 poc 兼容性

#### [v1.9.3] - 2022-05-25

**更新**  
- 增加奇安信网络空间搜索引擎数据支持  
- 在 POCBase 类中新增 self.rhost & self.rport 字段

#### [v1.9.1] - 2022-03-17

**更新**  
- 提供hook版的requests库，poc中可以自行加载  
- 重构shell模式，添加键盘中断句柄  
- 修复部分bug

#### [v1.9.0] - 2022-03-05

**修复**  
- 修复 urllib3 解析 URI 的问题  
- 禁用了 URL 编码

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
