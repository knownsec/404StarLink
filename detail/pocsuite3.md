## pocsuite3 <https://github.com/knownsec/pocsuite3>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-knownsec404-orange)
![GitHub stars](https://img.shields.io/github/stars/knownsec/pocsuite3.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.0.8-red)
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
* Dynamic loading PoC script from anywhere (local file, redis, database, Seebug ...)
* Load multi-target from anywhere (CIDR, local file, redis, database, Zoomeye, Shodan ...)
* Results can be easily exported
* Dynamic patch and hook requests 
* Both command line tool and python package import to use
* IPv6 support
* Global HTTP/HTTPS/SOCKS proxy support
* Simple spider API for PoC script to use
* YAML PoC support, compatible with [nuclei](https://github.com/projectdiscovery/nuclei)
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

### pocsuite3 load nuclei template
![](https://github.com/knownsec/pocsuite3/raw/master/asset/img/yaml_poc_showcase.png)

### build a docker vulnerability environment
**require Docker**

write dockerfile in poc
```python
class DemoPOC(POCBase):
    vulID = ''  # ssvid
    version = '1.0'
    author = ['']
    vulDate = '2029-5-8'
    createDate = '2019-5-8'
    updateDate = '2019-5-8'
    references = ['']
    name = 'Struts2 045 RCE CVE-2017'
    appPowerLink = ''
    appName = 'struts2'
    appVersion = ''
    vulType = ''
    desc = '''S2-045:影响版本Struts 2.3.20-2.3.28(除了2.3.20.3和2.3.24.3)'''
    samples = []
    category = POC_CATEGORY.EXPLOITS.WEBAPP
    dockerfile = '''FROM isxiangyang/struts2-all-vul-pocsuite:latest'''
```
#### only run vulnerable environments
```python
pocsuite -r pocs/Apache_Struts2/20170129_WEB_Apache_Struts2_045_RCE_CVE-2017-5638.py  --docker-start  --docker-port 127.0.0.1:8080:8080 --docker-env A=test --docker-port 8899:7890

,------.                        ,--. ,--.       ,----.   {2.0.6-cc19ae5}
|  .--. ',---. ,---.,---.,--.,--`--,-'  '-.,---.'.-.  |
|  '--' | .-. | .--(  .-'|  ||  ,--'-.  .-| .-. : .' <
|  | --'' '-' \ `--.-'  `'  ''  |  | |  | \   --/'-'  |
`--'     `---' `---`----' `----'`--' `--'  `----`----'   https://pocsuite.org
[*] starting at 15:34:12

[15:34:12] [INFO] loading PoC script 'pocs/Apache_Struts2/20170129_WEB_Apache_Struts2_045_RCE_CVE-2017-5638.py'
[15:34:12] [INFO] Image struts2_045_rce_cve-2017:pocsuite exists
[15:34:12] [INFO] Run container fa5b3b7bb2ea successful!
[15:34:12] [INFO] pocsusite got a total of 0 tasks
[15:34:12] [INFO] Scan completed,ready to print
```

#### run vulnerable environments and run poc 
```python
 pocsuite -r pocs/Apache_Struts2/20170129_WEB_Apache_Struts2_045_RCE_CVE-2017-5638.py -u http://127.0.0.1:8080/S2-032-showcase/fileupload/doUpload.action --docker-start  --docker-port 127.0.0.1:8080:8080 

,------.                        ,--. ,--.       ,----.   {2.0.6-cc19ae5}
|  .--. ',---. ,---.,---.,--.,--`--,-'  '-.,---.'.-.  |
|  '--' | .-. | .--(  .-'|  ||  ,--'-.  .-| .-. : .' <
|  | --'' '-' \ `--.-'  `'  ''  |  | |  | \   --/'-'  |
`--'     `---' `---`----' `----'`--' `--'  `----`----'   https://pocsuite.org
[*] starting at 15:38:46

[15:38:46] [INFO] loading PoC script 'pocs/Apache_Struts2/20170129_WEB_Apache_Struts2_045_RCE_CVE-2017-5638.py'
[15:38:46] [INFO] Image struts2_045_rce_cve-2017:pocsuite exists
[15:38:47] [INFO] Run container 1a6eae1e8953 successful!
[15:38:47] [INFO] pocsusite got a total of 1 tasks
[15:38:47] [INFO] running poc:'Struts2 045 RCE CVE-2017' target 'http://127.0.0.1:8080/S2-032-showcase/fileupload/doUpload.action'
[15:39:17] [+] URL : http://127.0.0.1:8080/S2-032-showcase/fileupload/doUpload.action
[15:39:17] [+] Headers : {'Server': 'Apache-Coyote/1.1', 'nyvkx': '788544', 'Set-Cookie': 'JSESSIONID=0A9892431B32A541B51D4721FA0D2728; Path=/S2-032-showcase/; HttpOnly', 'Content-Type': 'text/html;charset=ISO-8859-1', 'Transfer-Encoding': 'chunked', 'Date': 'Mon, 25 Dec 2023 07:39:17 GMT'}
[15:39:17] [INFO] Scan completed,ready to print

+------------------------------------------------------------------+--------------------------+--------+-----------+---------+---------+
| target-url                                                       |         poc-name         | poc-id | component | version |  status |
+------------------------------------------------------------------+--------------------------+--------+-----------+---------+---------+
| http://127.0.0.1:8080/S2-032-showcase/fileupload/doUpload.action | Struts2 045 RCE CVE-2017 |        |  struts2  |         | success |
+------------------------------------------------------------------+--------------------------+--------+-----------+---------+---------+
success : 1 / 1
```


#### Introduction to vulnerability environment construction
```shell
Docker Environment:
  Docker Environment options

  --docker-start        Run the docker for PoC
  --docker-port DOCKER_PORT
                        Publish a container's port(s) to the host
  --docker-volume DOCKER_VOLUME
                        Bind mount a volume
  --docker-env DOCKER_ENV
                        Set environment variables
  --docker-only         Only run docker environment

```
 - `--docker-start` Start environment parameters. If specified, docker images will be obtained from poc.
 - `--docker-port`  publish a container's port(s) to the host, like: `--docker-port [host port]:[container port]`,you can specify multiple
 - `--docker-volume` bind mount a volume,like `--docker-volume /host/path/:/container/path`,you can specify multiple
 - `--docker-env`  set environment variables `--docker-env VARIBLES=value`,you can specify multiple
 - `--docker-only` only start the docker environment

The usage is roughly the same as docker’s command line parameters.

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

- 2023-07-18 发布演示视频[404星链计划开源安全工具演示——pocsuite3](https://www.bilibili.com/video/BV1gz4y1E7j1/)
- 2022-07-13 发布文章[《Pocsuite3 入门教程》](https://paper.seebug.org/1931/)

## 最近更新

#### [v2.0.8] - 2024-02-09

**更新**  
- 修复 nuclei dsl 语法解析  
- 修复 -l 命令在 windows 兼容问题

#### [v2.0.7] - 2023-12-29

**更新**  
- 添加 http debug level 命令行参数 --http-debug  
- 修复一些 bug

#### [v2.0.6] - 2023-12-26

**更新**  
- 新增查看本地 poc 参数 -l  
- 根据poc搭建对应的漏洞环境，详情可以参考 pocs/Apache_Struct2

#### [v2.0.5] - 2023-07-27

**更新**  
- 修复 urllib3 更新导致 requests hook 失效的问题  
- 优化 DSL 表达式执行  
- 将 mmh3 设置为可选依赖  
- 优化检查更新

#### [v2.0.4] - 2023-04-29

**更新**  
- 兼容 nuclei v2.9.1 的模版协议名称变化

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
