## pocsuite3 <https://github.com/knownsec/pocsuite3>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-knownsec404-orange)
![GitHub stars](https://img.shields.io/github/stars/knownsec/pocsuite3.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.0.2-red)
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
* IPv6 support
* Global HTTP/HTTPS/SOCKS proxy support
* Simple spider API for PoC script to use
* Integrate with [Seebug](https://www.seebug.org) (for load PoC from Seebug website)
* Integrate with [ZoomEye](https://www.zoomeye.org), [Shodan](https://www.shodan.io), etc.  (for load target use `Dork`)
* Integrate with [Ceye](http://ceye.io/), [Interactsh](https://github.com/projectdiscovery/interactsh) (for verify blind DNS and HTTP request)
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

- Python 3.7+
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

### Docker

```
docker run -it pocsuite3/pocsuite3
```

### ArchLinux

``` bash
yay pocsuite3
```

###

Or click [here](https://github.com/knownsec/pocsuite3/archive/master.zip) to download the latest source zip package and extract

``` bash
wget https://github.com/knownsec/pocsuite3/archive/master.zip
unzip master.zip
cd pocsuite3-master
pip3 install -r requirements.txt
python3 setup.py install
```


The latest version of this software is available at: https://pocsuite.org

## Documentation

Documentation is available at: https://pocsuite.org

## Usage

```
cli mode

	# basic usage, use -v to set the log level
	pocsuite -u http://example.com -r example.py -v 2

	# run poc with shell mode
	pocsuite -u http://example.com -r example.py -v 2 --shell

	# search for the target of redis service from ZoomEye and perform batch detection of vulnerabilities. The threads is set to 20
	pocsuite -r redis.py --dork service:redis --threads 20

	# load all poc in the poc directory and save the result as html
	pocsuite -u http://example.com --plugins poc_from_pocs,html_report

	# load the target from the file, and use the poc under the poc directory to scan
	pocsuite -f batch.txt --plugins poc_from_pocs,html_report

	# load CIDR target
	pocsuite -u 10.0.0.0/24 -r example.py

	# the custom parameters `command` is implemented in ecshop poc, which can be set from command line options
	pocsuite -u http://example.com -r ecshop_rce.py --attack --command "whoami"

console mode
    poc-console
```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2022-07-13 发布文章[《Pocsuite3 入门教程》](https://paper.seebug.org/1931/)

## 最近更新

#### [v2.0.2] - 2022-12-13

**更新**  
- 修复 _check 方法中 url 重定向的问题  
- 修复 console 模式下 use 命令使用绝对路径的问题  
- 修复 build_url 兼容 ipv6 的问题  
- 优化 nuclei DSL 表达式执行

#### [v2.0.1] - 2022-11-09

**更新**
  - 修复 words 匹配器表达式执行的问题  
- 修复模版中包含中文异常捕获的问题  
- 提高模版的鲁棒性  
- 支持 digest_username 和 digest_password，用于 http 认证  
- 支持 negative 反向匹配器

#### [v2.0.0] - 2022-11-03

**更新**  
- 支持 yaml 格式 poc，与 nuclei 的 poc 模版兼容  
- 修复 httpserver 模块在 macos 平台卡住的问题  
- 结合 http 状态码对 http/https 协议自动纠正

#### [v1.9.11] - 2022-09-08

**更新**  
- 用户可以在 PoC 中自定义协议和默认端口，方便对 url 格式化  
- 使用 -p 参数给目标添加额外端口，可同时提供协议  
- 使用 -s 参数可以 skip target 本身的端口，只使用 -p 提供的端口  
- poc-console 优化  
- 一些改进和 bug 修复

#### [v1.9.9] - 2022-08-24

**更新**  
- 新增根据 poc 协议字段自动修正 target 路径  
- 修复 windows 平台 poc-console 高亮显示的问题  
- 默认去除 target 路径末尾的 '/' 字符

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
