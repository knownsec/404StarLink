## HackBrowserData <https://github.com/moonD4rk/HackBrowserData>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-moonD4rk-orange)
![GitHub stars](https://img.shields.io/github/stars/moonD4rk/HackBrowserData.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.4.6-red)
![Time](https://img.shields.io/badge/Join-20201221-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

# HackBrowserData

`HackBrowserData` is a command-line tool for decrypting and exporting browser data (passwords, history, cookies, bookmarks, credit cards, download history, localStorage and extensions) from the browser. It supports the most popular browsers on the market and runs on Windows, macOS and Linux.

> Disclaimer: This tool is only intended for security research. Users are responsible for all legal and related liabilities resulting from the use of this tool. The original author does not assume any legal responsibility.

## Supported Browser

### Windows
| Browser            | Password | Cookie | Bookmark | History |
|:-------------------|:--------:|:------:|:--------:|:-------:|
| Google Chrome      |    ✅     |   ✅    |    ✅     |    ✅    |
| Google Chrome Beta |    ✅     |   ✅    |    ✅     |    ✅    |
| Chromium           |    ✅     |   ✅    |    ✅     |    ✅    |
| Microsoft Edge     |    ✅     |   ✅    |    ✅     |    ✅    |
| 360 Speed          |    ✅     |   ✅    |    ✅     |    ✅    |
| QQ                 |    ✅     |   ✅    |    ✅     |    ✅    |
| Brave              |    ✅     |   ✅    |    ✅     |    ✅    |
| Opera              |    ✅     |   ✅    |    ✅     |    ✅    |
| OperaGX            |    ✅     |   ✅    |    ✅     |    ✅    |
| Vivaldi            |    ✅     |   ✅    |    ✅     |    ✅    |
| Yandex             |    ✅     |   ✅    |    ✅     |    ✅    |
| CocCoc             |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox            |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox Beta       |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox Dev        |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox ESR        |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox Nightly    |    ✅     |   ✅    |    ✅     |    ✅    |
| Internet Explorer  |    ❌     |   ❌    |    ❌     |    ❌    |


### MacOS

Based on Apple's security policy, some browsers **require a current user password** to decrypt.

| Browser            | Password | Cookie | Bookmark | History |
|:-------------------|:--------:|:------:|:--------:|:-------:|
| Google Chrome      |    ✅     |   ✅    |    ✅     |    ✅    |
| Google Chrome Beta |    ✅     |   ✅    |    ✅     |    ✅    |
| Chromium           |    ✅     |   ✅    |    ✅     |    ✅    |
| Microsoft Edge     |    ✅     |   ✅    |    ✅     |    ✅    |
| Brave              |    ✅     |   ✅    |    ✅     |    ✅    |
| Opera              |    ✅     |   ✅    |    ✅     |    ✅    |
| OperaGX            |    ✅     |   ✅    |    ✅     |    ✅    |
| Vivaldi            |    ✅     |   ✅    |    ✅     |    ✅    |
| CocCoc             |    ✅     |   ✅    |    ✅     |    ✅    |
| Yandex             |    ✅     |   ✅    |    ✅     |    ✅    |
| Arc                |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox            |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox Beta       |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox Dev        |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox ESR        |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox Nightly    |    ✅     |   ✅    |    ✅     |    ✅    |
| Safari             |    ❌     |   ❌    |    ❌     |    ❌    |

### Linux

| Browser            | Password | Cookie | Bookmark | History |
|:-------------------|:--------:|:------:|:--------:|:-------:|
| Google Chrome      |    ✅     |   ✅    |    ✅     |    ✅    |
| Google Chrome Beta |    ✅     |   ✅    |    ✅     |    ✅    |
| Chromium           |    ✅     |   ✅    |    ✅     |    ✅    |
| Microsoft Edge Dev |    ✅     |   ✅    |    ✅     |    ✅    |
| Brave              |    ✅     |   ✅    |    ✅     |    ✅    |
| Opera              |    ✅     |   ✅    |    ✅     |    ✅    |
| Vivaldi            |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox            |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox Beta       |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox Dev        |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox ESR        |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox Nightly    |    ✅     |   ✅    |    ✅     |    ✅    |


## Getting started

### Install

Installation of `HackBrowserData` is dead-simple, just download [the release for your system](https://github.com/moonD4rk/HackBrowserData/releases) and run the binary.

> In some situations, this security tool will be treated as a virus by Windows Defender or other antivirus software and can not be executed. The code is all open source, you can modify and compile by yourself.

### Building from source

only support `go 1.21+` with go generics and `log/slog` standard library.

```bash
$ git clone https://github.com/moonD4rk/HackBrowserData

$ cd HackBrowserData/cmd/hack-browser-data

$ go build
```

### Cross compile

Here's an example of use `macOS` building for `Windows` and `Linux`

#### For Windows

```shell
GOOS=windows GOARCH=amd64 go build
```

#### For Linux

````shell
GOOS=linux GOARCH=amd64 go build
````

### Run

You can double-click to run, or use command line.

```powershell
PS C:\Users\moond4rk\Desktop> .\hack-browser-data.exe -h
NAME:
   hack-browser-data - Export passwords|bookmarks|cookies|history|credit cards|download history|localStorage|extensions from browser
USAGE:
   [hack-browser-data -b chrome -f json --dir results --zip]
   Export all browsing data (passwords/cookies/history/bookmarks) from browser
   Github Link: https://github.com/moonD4rk/HackBrowserData
VERSION:
   0.4.6

GLOBAL OPTIONS:
   --verbose, --vv                   verbose (default: false)
   --compress, --zip                 compress result to zip (default: false)
   --browser value, -b value         available browsers: all|360|brave|chrome|chrome-beta|chromium|coccoc|dc|edge|firefox|opera|opera-gx|qq|sogou|vivaldi|yandex (default: "all")
   --results-dir value, --dir value  export dir (default: "results")
   --format value, -f value          output format: csv|json (default: "csv")
   --profile-path value, -p value    custom profile dir path, get with chrome://version
   --full-export, --full             is export full browsing data (default: true)
   --help, -h                        show help
   --version, -v                     print the version

```

For example, the following is an automatic scan of the browser on the current computer, outputting the decryption results in `JSON` format and compressing as `zip`.

```powershell
PS C:\Users\moond4rk\Desktop> .\hack-browser-data.exe -b all -f json --dir results --zip

PS C:\Users\moond4rk\Desktop> ls -l .\results\
    Directory: C:\Users\moond4rk\Desktop\results
    
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         7/15/2024  10:55 PM          44982 results.zip
```


### Run with custom browser profile folder

If you want to export data from a custom browser profile folder, you can use the `-p` parameter to specify the path of the browser profile folder. PS: use double quotes to wrap the path.
```powershell
PS C:\Users\moond4rk\Desktop> .\hack-browser-data.exe -b chrome -p "C:\Users\User\AppData\Local\Microsoft\Edge\User Data\Default"

[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_creditcard.csv success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_bookmark.csv success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_cookie.csv success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_history.csv success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_download.csv success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_password.csv success  
```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2022-09-08 发布演示视频[404星链计划开源安全工具演示——HackBrowserData](https://www.bilibili.com/video/BV1eU4y1z7si)

## 最近更新

#### [v0.4.6] - 2024-07-16

**更新**  
- 重构项目并更新 repo deploy  
- 重构 logger 到标准库  
- 移除 CGO go-sqlite3 改用纯 go 驱动  
- 优化加解密模块  
- 重构获取浏览器数据的逻辑  
- 跳过 chromium 快照目录以找到正确的密码数据库  
- 改进浏览浏览器配置文件目录时的错误处理  
- 优化 GitHub 操作和依赖项更新

#### [v0.4.5] - 2024-01-09

**新增**  
- 添加搜狗和dc浏览器  
- 格式化项目布局  
- 添加完全导出浏览数据选项  
- 支持 macOS 的 Arc 浏览器  
- 改进扩展解析  

**修复**  
- 修复日志错误并删除已弃用的 linter  
- 修复运行二进制文件失败时的句柄错误  
- 修复数据丢失导致标题为空的问题  
- 修复命令行使用提示不完整的bug  
- 修复错误的日志调用者跳过级别  
- 修复 Firefox 文件遍历中的错误  
- 解密主密钥失败时发出的警告  
- 改进浏览数据和文件复制功能中的错误处理  

**优化**  
- 优化 JSON 缩进输出格式  
- 优化添加提供商软件文件夹和 linter 检查

#### [v0.4.4] - 2022-08-16

**更新**  
- 修复 chrome 在 windows 上获取 cookie 内容失败的问题  
- 在 CI 中添加了更多检查  
- 优化  golangci-lint 代码  
- 修复压缩结果时无法访问文件的问题

#### [v0.4.3] - 2022-06-05

**更新**  
- 新增支持从浏览器导出多个用户  
- 修复当过滤结果为空并导出到 csv 时，对其进行 utf8 编码  
- 修复 Windows 下 Chrome 和 OperaGx 的配置文件夹  
- 修复拼写错误

#### [v0.4.2] - 2022-05-01

**更新**  
- 新增导出扩展
- 新增设置控制台 log 日志的色彩  
- 文档添加 HackBrowserData 的 logo

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
