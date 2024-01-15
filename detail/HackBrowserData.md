## HackBrowserData <https://github.com/moonD4rk/HackBrowserData>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-moonD4rk-orange)
![GitHub stars](https://img.shields.io/github/stars/moonD4rk/HackBrowserData.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.4.5-red)
![Time](https://img.shields.io/badge/Join-20201221-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

<div align="center">
<img src="https://github.com/moonD4rk/HackBrowserData/raw/master/LOGO.png" alt="hack-browser-data logo" />
</div>


# HackBrowserData

`HackBrowserData` 是一个浏览器数据（密码|历史记录|Cookie|书签|信用卡|下载记录|localStorage|浏览器插件）的导出工具，支持全平台主流浏览器。


> 免责声明：此工具仅限于安全研究，用户承担因使用此工具而导致的所有法律和相关责任！作者不承担任何法律责任！

## 各平台浏览器支持情况

### Windows

| 浏览器                | 密码  | Cookie | 书签  | 历史记录 |
|:-------------------|:---:|:------:|:---:|:----:|
| Google Chrome      |  ✅  |   ✅    |  ✅  |  ✅   |
| Google Chrome Beta |  ✅  |   ✅    |  ✅  |  ✅   |
| Chromium           |  ✅  |   ✅    |  ✅  |  ✅   |
| Microsoft Edge     |  ✅  |   ✅    |  ✅  |  ✅   |
| 360 极速浏览器          |  ✅  |   ✅    |  ✅  |  ✅   |
| QQ                 |  ✅  |   ✅    |  ✅  |  ✅   |
| Brave              |  ✅  |   ✅    |  ✅  |  ✅   |
| Opera              |  ✅  |   ✅    |  ✅  |  ✅   |
| OperaGX            |  ✅  |   ✅    |  ✅  |  ✅   |
| Vivaldi            |  ✅  |   ✅    |  ✅  |  ✅   |
| Yandex             |  ✅  |   ✅    |  ✅  |  ✅   |
| CocCoc             |  ✅  |   ✅    |  ✅  |  ✅   |
| Firefox            |  ✅  |   ✅    |  ✅  |  ✅   |
| Firefox Beta       |  ✅  |   ✅    |  ✅  |  ✅   |
| Firefox Dev        |  ✅  |   ✅    |  ✅  |  ✅   |
| Firefox ESR        |  ✅  |   ✅    |  ✅  |  ✅   |
| Firefox Nightly    |  ✅  |   ✅    |  ✅  |  ✅   |
| IE 浏览器             |  ❌  |   ❌    |  ❌  |  ❌   |

### MacOS

由于 MacOS 的安全性设置，基于 `Chromium` 内核浏览器解密时**需要当前用户密码**

| 浏览器                | 密码 | Cookie | 书签 | 历史记录 |
|:-------------------|:--:|:------:|:--:|:----:|
| Google Chrome      | ✅  |   ✅    | ✅  |  ✅   |
| Google Chrome Beta | ✅  |   ✅    | ✅  |  ✅   |
| Chromium           | ✅  |   ✅    | ✅  |  ✅   |
| Microsoft Edge     | ✅  |   ✅    | ✅  |  ✅   |
| Brave              | ✅  |   ✅    | ✅  |  ✅   |
| Opera              | ✅  |   ✅    | ✅  |  ✅   |
| OperaGX            | ✅  |   ✅    | ✅  |  ✅   |
| Vivaldi            | ✅  |   ✅    | ✅  |  ✅   |
| CocCoc             | ✅  |   ✅    | ✅  |  ✅   |
| Yandex             | ✅  |   ✅    | ✅  |  ✅   |
| Arc                | ✅  |   ✅    | ✅  |  ✅   |
| Firefox            | ✅  |   ✅    | ✅  |  ✅   |
| Firefox Beta       | ✅  |   ✅    | ✅  |  ✅   |
| Firefox Dev        | ✅  |   ✅    | ✅  |  ✅   |
| Firefox ESR        | ✅  |   ✅    | ✅  |  ✅   |
| Firefox Nightly    | ✅  |   ✅    | ✅  |  ✅   |
| Safari             | ❌  |   ❌    | ❌  |  ❌   |

### Linux

| 浏览器                | 密码  | Cookie | 书签  | 历史记录 |
|:-------------------|:---:|:------:|:---:|:----:|
| Google Chrome      |  ✅  |   ✅    |  ✅  |  ✅   |
| Google Chrome Beta |  ✅  |   ✅    |  ✅  |  ✅   |
| Chromium           |  ✅  |   ✅    |  ✅  |  ✅   |
| Microsoft Edge     |  ✅  |   ✅    |  ✅  |  ✅   |
| Brave              |  ✅  |   ✅    |  ✅  |  ✅   |
| Opera              |  ✅  |   ✅    |  ✅  |  ✅   |
| Vivaldi            |  ✅  |   ✅    |  ✅  |  ✅   |
| Chromium           |  ✅  |   ✅    |  ✅  |  ✅   |
| Firefox            |  ✅  |   ✅    |  ✅  |  ✅   |
| Firefox Beta       |  ✅  |   ✅    |  ✅  |  ✅   |
| Firefox Dev        |  ✅  |   ✅    |  ✅  |  ✅   |
| Firefox ESR        |  ✅  |   ✅    |  ✅  |  ✅   |
| Firefox Nightly    |  ✅  |   ✅    |  ✅  |  ✅   |

## 安装运行
### 安装

可下载已编译好，可直接运行的 [二进制文件](https://github.com/moonD4rk/HackBrowserData/releases)

> 某些情况下，这款安全工具会被 Windows Defender 或其他杀毒软件当作病毒导致无法执行。代码已经全部开源，可自行编译。

### 从源码编译

仅支持 `go 1.18+` 以后版本，一些函数使用到了泛型

``` bash
$ git clone https://github.com/moonD4rk/HackBrowserData

$ cd HackBrowserData/cmd/hack-browser-data

$ CGO_ENABLED=1 go build
```

### 跨平台编译

由于用到了 `go-sqlite3` 库，在跨平台编译时需提前安装支持目标平台的 `GCC` 工具，下面以 `MacOS` 下分别编译 `Windows` 和 `Linux` 程序为例：

#### Windows

``` shell
brew install mingw-w64

CGO_ENABLED=1 GOOS=windows GOARCH=amd64 CC=x86_64-w64-mingw32-gcc go build
```

#### Linux

``` shell
brew install FiloSottile/musl-cross/musl-cross

CC=x86_64-linux-musl-gcc CXX=x86_64-linux-musl-g++ GOARCH=amd64 GOOS=linux CGO_ENABLED=1 go build -ldflags "-linkmode external -extldflags -static"
```

### 运行
双击直接运行，也可以使用命令行调用相应的命令。

```
PS C:\test> .\hack-browser-data.exe -h
NAME:
   hack-browser-data - Export password|bookmark|cookie|history|credit card|download|localStorage|extension from browser

USAGE:
   [hack-browser-data -b chrome -f json -dir results -cc]
   Export all browingdata(password/cookie/history/bookmark) from browser
   Github Link: https://github.com/moonD4rk/HackBrowserData

VERSION:
   0.5.0

GLOBAL OPTIONS:
   --verbose, --vv                   verbose (default: false)
   --compress, --zip                 compress result to zip (default: false)
   --browser value, -b value         available browsers: all|brave|chrome|chrome-beta|chromium|coccoc|edge|firefox|opera|opera-gx|vivaldi|yandex (default: "all")
   --results-dir value, --dir value  export dir (default: "results")
   --format value, -f value          file name csv|json (default: "csv")
   --profile-path value, -p value    custom profile dir path, get with chrome://version
   --full-export, --full             is export full browsing data (default: true)
   --help, -h                        show help
   --version, -v                     print the version


PS C:\test> .\hack-browser-data.exe -b all -f json --dir results -zip
[NOTICE] [browser.go:46,pickChromium] find browser Chrome success  
[NOTICE] [browser.go:46,pickChromium] find browser Microsoft Edge success  
[NOTICE] [browsingdata.go:59,Output] output to file results/microsoft_edge_download.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/microsoft_edge_password.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/microsoft_edge_creditcard.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/microsoft_edge_bookmark.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/microsoft_edge_cookie.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/microsoft_edge_history.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_history.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_download.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_password.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_creditcard.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_bookmark.json success  
[NOTICE] [browsingdata.go:59,Output] output to file results/chrome_cookie.json success  

```

### 基于此工具的一些其他项目
[Sharp-HackBrowserData](https://github.com/S3cur3Th1sSh1t/Sharp-HackBrowserData)

[Reflective-HackBrowserData](https://github.com/idiotc4t/Reflective-HackBrowserData)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2022-09-08 发布演示视频[404星链计划开源安全工具演示——HackBrowserData](https://www.bilibili.com/video/BV1eU4y1z7si)

## 最近更新

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

#### [v0.4.1] - 2022-04-20

**更新**  
- 支持所有浏览器导出 local storage
- 修复 firefox ans1 数据结构  
- 修复 windows 平台上 chromium 密钥查找失败的问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
