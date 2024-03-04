## afrog <https://github.com/zan8in/afrog>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-zan8in-orange)
![GitHub stars](https://img.shields.io/github/stars/zan8in/afrog.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V3.0.1-red)
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

- 2023-07-10 发布视频[《404星链计划-afrog：快速稳定的漏洞扫描工具》](https://www.bilibili.com/video/BV1Pz4y177PU/)

## 最近更新

#### [v3.0.1] - 2024-02-27

**更新**  
- 新增 -oob 参数，指定扫描使用的反连平台，默认 ceyeio  
- 新增 oob 功能，代替旧版 reverse(将废弃)  

**注意事项**  
- 历史 PoC 的 newReverse() 方法均已升级为新版的 oob() 方法。为确保兼容性和功能完整性，建议用户尽快升级至 3.0.1

#### [v2.9.8] - 2024-01-06

**更新**  
- 新增引入 ysoserial 函数，用于生成 Java 反序列化 payload  
- 新增引入 aesCBC 函数

#### [v2.9.7] - 2024-01-03

**更新**  
- 优化调整反连平台优先级逻辑，确保自建Eye反连平台具有最高优先权  
- 优化花里胡哨的进度条，看起来炫，实际并没什么用

#### [v2.9.6] - 2023-12-22

**更新**  
- 优化进行TCP PoC验证时，新增返回十六进制数据包类型的功能  
- PoC总数：1266

#### [v2.9.5] - 2023-12-06

**更新**  
- 新增 -cyberspace/-cs 网络测绘空间搜索功能  
- 优化 PoC GitLab public snippets 漏洞等级由 INFO 改为 HIGH

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
