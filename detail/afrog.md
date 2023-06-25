## afrog <https://github.com/zan8in/afrog>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-zan8in-orange)
![GitHub stars](https://img.shields.io/github/stars/zan8in/afrog.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.6.0-red)
![Time](https://img.shields.io/badge/Join-20220615-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## What is afrog

afrog is a high-performance vulnerability scanner that is fast and stable. It supports user-defined PoC and comes with several built-in types, such as CVE, CNVD, default passwords, information disclosure, fingerprint identification, unauthorized access, arbitrary file reading, and command execution. With afrog, network security professionals can quickly validate and remediate vulnerabilities, which helps to enhance their security defense capabilities.

## Features

* [x] Open source
* [x] Fast, stable, with low false positives
* [x] Detailed HTML vulnerability reports
* [x] Customizable and stably updatable PoCs
* [x] Active community exchange group

## Installation

### Prerequisites

- [Go](https://go.dev/) version 1.19 or higher.

you can install it with:

**Binary**
```sh
$ https://github.com/zan8in/afrog/releases
```

**Github**
```sh
$ git clone https://github.com/zan8in/afrog.git
$ cd afrog
$ go build cmd/afrog/main.go
$ ./afrog -h
```

**Go**
```sh
$ go install -v https://github.com/zan8in/afrog/cmd/afrog@latest
```

## Running afrog

By default, afrog scans all built-in PoCs, and if it finds any vulnerabilities, it automatically creates an HTML report with the date of the scan as the filename.

```sh
afrog -t https://example.com
```

**Warning occurs when running afrog**

If you see an error message saying:
```
[ERR] ceye reverse service not set: /home/afrog/.config/afrog/afrog-config.yaml
```
it means you need to modify the [configuration file](#configuration-file).

To execute a custom PoC directory, you can use the following command:

```sh
afrog -t https://example.com -P mypocs/
```

Use the command `-s keyword` to perform a fuzzy search on all PoCs and scan the search results. Multiple keywords can be used, separated by commas. For example: `-s weblogic,jboss`.

```sh
afrog -t https://example.com -s weblogic,jboss
```

Use the command `-S keyword` to scan vulnerabilities based on their severity level. Severity levels include: `info`, `low`, `medium`, `high`, and `critical`. For example, to only scan high and critical vulnerabilities, use the command `-S high,critical`.

```sh
afrog -t https://example.com -S high,critical
```

You can scan multiple URLs at the same time as well.

```sh
afrog -T urls.txt
```

## Configuration file

The first time you start afrog, it will automatically create a configuration file called `afrog-config.yaml`, which will be saved in the current user directory under `$HOME/.config/afrog/afrog-config.yaml`.

Here is an example config file:

```yaml
reverse:
  ceye:
    api-key: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    domain: "xxxxxx.ceye.io"
```

`reverse` is a reverse connection platform used to verify command execution vulnerabilities that cannot be echoed back. Currently, only ceye can be used for verification. To obtain ceye, follow these steps:

- Go to the [ceye.io](http://ceye.io/) website and register an account.
- Log in and go to the personal settings page.
- Copy the `domain` and `api-key` and correctly configure them in the `afrog-config.yaml` file.


## Json Output (For developers)

### Json
Optional command: `-json` `-j`, Save the scan results to a JSON file. The JSON file includes the following contents by default: `target`, `fulltarget`, `id`, and `info`. The info field includes the following sub-fields: `name`, `author`, `severity`, `description`, and `reference`. If you want to save both `request` and `response` contents, please use the [-json-all](#jsonall) command parameter.

```sh
afrog  -t https://example.com -json result.json
afrog  -t https://example.com -j result.json
```

::: warning
The content of the JSON file is updated in real time. However, there is an important note to keep in mind: before the scan is completed, if developers want to parse the file content, they need to add a '`]`' symbol to the end of the file by themselves, otherwise it will cause parsing errors. Of course, if you wait for the scan to complete before parsing the file, this issue will not occur.
:::


### JsonAll

Optional command: `-json-all` `-ja`, The only difference between the `-json-all` and `-json` commands is that `-json-all` writes all vulnerability results, including `request` and `response`, to a JSON file.

```sh
afrog -t https://example.com -json-all result.json
afrog -t https://example.com -ja result.json
```


## Screenshot

![](https://github.com/zan8in/afrog/blob/main/images/1.png)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v2.6.0] - 2023-06-24

**新增**  
- 新增 -append-poc / -ap 功能，允许指定一个或多个PoC文件或目录  
- rawhttp 支持 HTTP/socks5 代理  
- 庆祝！afrog PoC 的总数突破了1000个！目前总数为1018个

#### [v2.5.3] - 2023-06-14

**新增**  
- -target/-t 现在支持多个 URL  
- 添加 JNDI 反连功能  
- 添加 afrog 调用库和演示示例

#### [v2.5.2] - 2023-06-07

**新增**  
- 命令 -mrbs 动态设置 http 响应 body 的最大值(默认2m)  
- 删除 PoC shiro-key-detect

#### [v2.5.1] - 2023-05-22

**新增**  
- 使用 YAML 编写 TCP/UDP 的 POC 文件  
- 使用 YAML 调用 Go 语言的 POC 文件  
- Shiro Key 检测脚本默认检测 20 个 Key  

**优化**  
- 解决 -update 程序更新时的路径错误问题  
- 改进控制台提示信息  
- 禁用 -up 命令，改为自动执行  
- 将反连平台未配置的提示等级改为 Info  
- 默认情况下不会监视目标访问(使用-monitor-targets/-mt命令进行启用)  
- 删除重复 PoC: hikvision-applyct-fastjson-rce

#### [v2.3.2] - 2023-05-14

**新增**  
- 使用命令参数 -json 或 -j，将漏洞结果写入 JSON 文件，不包括 request 和 response  
- 使用命令参数 -json-all 或 -ja，将漏洞结果写入 JSON 文件，包括 request 和 response  
- 使用 disable-output-html 命令可以禁止生成 HTML 报告，该命令的优先级高于 -o 命令  
- PoC 脚本 info 信息增加 affected、solutions、created 三个字段  

**优化**  
- 已移除重复的PoC: springboot-env-unauth  
- 执行更新操作时，-up 命令提示不够友好  
- 按照从低到高的安全风险级别顺序进行扫描  
- 优化 url.path 编码问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
