## HackBrowserData <https://github.com/moonD4rk/HackBrowserData>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-moonD4rk-orange)
![GitHub stars](https://img.shields.io/github/stars/moonD4rk/HackBrowserData.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.3.7-red)
![Time](https://img.shields.io/badge/Join-20201221-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


# HackBrowserData

hack-browser-data 是一个浏览器数据（密码 | 历史记录 | Cookie | 书签 | 信用卡 | 下载记录）的导出工具，支持全平台主流浏览器。


> 特别声明：此工具仅限于安全研究，用户承担因使用此工具而导致的所有法律和相关责任！作者不承担任何法律责任！

## 各平台浏览器支持情况

### Windows

| 浏览器        | 密码 | Cookie | 书签 | 历史记录 |
| :------- | :------: | :----: | :------: | :-----: |
| Google Chrome|    ✅     |   ✅    |    ✅     |    ✅    |
| Google Chrome Beta|    ✅    |   ✅   |    ✅    |    ✅    |
| Chromium |    ✅    |    ✅    |    ✅    |    ✅    |
| Microsoft Edge|    ✅     |   ✅    |    ✅     |    ✅    |
| 360 极速浏览器    |    ✅     |   ✅    |    ✅     |    ✅    |
| QQ 浏览器|    ✅     |   ✅    |    ✅     |    ✅    |
| Brave 浏览器 |    ✅    |   ✅   |    ✅    |    ✅    |
| Opera 浏览器 |    ✅    |    ✅    |    ✅    |    ✅    |
| OperaGX 浏览器 |    ✅    |    ✅    |    ✅    |    ✅    |
| Vivaldi 浏览器 |    ✅    |    ✅    |    ✅    |    ✅    |
| Firefox |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox Beta |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox Dev |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox ESR |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox Nightly |    ✅    |   ✅   |    ✅    |    ✅    |
| IE 浏览器        |    ❌     |   ❌    |    ❌     |    ❌    |

### MacOS

由于 MacOS 的安全性设置，基于 `Chromium` 内核浏览器解密时**需要当前用户密码**

| 浏览器                   | 密码 | Cookie | 书签 | 历史记录 |
| :--------------------------- | :------: | :----: | :------: | :-----: |
| Google Chrome  |    ✅     |   ✅    |    ✅     |    ✅    |
| Google Chrome Beta |    ✅    |   ✅   |    ✅    |    ✅    |
| Chromium |    ✅    |    ✅    |    ✅    |    ✅    |
| Microsoft Edge |    ✅     |   ✅    |    ✅     |    ✅    |
| Brave |    ✅    |   ✅   |    ✅    |    ✅    |
| Opera |    ✅    |    ✅    |    ✅    |    ✅    |
| OperaGX |    ✅    |    ✅    |    ✅    |    ✅    |
| Vivaldi |    ✅    |    ✅    |    ✅    |    ✅    |
| Firefox |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox Beta |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox Dev |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox ESR |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox Nightly |    ✅    |   ✅   |    ✅    |    ✅    |
| Safari   |    ❌     |   ❌    |    ❌     |    ❌|

### Linux

| 浏览器    | 密码 | Cookie | 书签 | 历史记录 |
| :------------ | :------: | :----: | :------: | :-----: |
| Google Chrome |    ✅     |   ✅    |    ✅     |    ✅    |
| Google Chrome Beta |    ✅    |   ✅   |    ✅    |    ✅    |
| Chromium |    ✅    |    ✅    |    ✅    |    ✅    |
| Microsoft Edge |    ✅    |   ✅   |    ✅    |    ✅    |
| Brave |    ✅    |   ✅   |    ✅    |    ✅    |
| Opera |    ✅    |    ✅    |    ✅    |    ✅    |
| Vivaldi |    ✅    |    ✅    |    ✅    |    ✅    |
| Chromium |    ✅     |   ✅    |    ✅     |    ✅    |
| Firefox |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox Beta |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox Dev |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox ESR |    ✅    |   ✅   |    ✅    |    ✅    |
| Firefox Nightly |    ✅    |   ✅   |    ✅    |    ✅    |

## 安装运行
### 安装

可下载已编译好，可直接运行的 [二进制文件](https://github.com/moonD4rk/HackBrowserData/releases)

> 某些情况下，这款安全工具会被 Windows Defender 或其他杀毒软件当作病毒导致无法执行。代码已经全部开源，可自行编译。

### 从源码编译

支持版本 `go 1.14+`

``` bash
git clone https://github.com/moonD4rk/HackBrowserData

cd HackBrowserData

go get -v -t -d ./...

go build
```

### 跨平台编译

由于用到了 `go-sqlite3` 库，在跨平台编译时需提前安装支持目标平台的 `GCC` 工具，下面以 `MacOS` 下分别编译 `Windows` 和 `Linux` 程序为例：

#### Windows

``` shell
brew install mingw-w64

CGO_ENABLED=1 GOOS=windows GOARCH=amd64 CC="x86_64-w64-mingw32-gcc" go build
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
   hack-browser-data - Export passwords/cookies/history/bookmarks from browser

USAGE:
   [hack-browser-data -b chrome -f json -dir results -cc]
   Get all data(password/cookie/history/bookmark) from chrome

VERSION:
   0.3.6
GLOBAL OPTIONS:
   --verbose, --vv                     verbose (default: false)
   --compress, --cc                    compress result to zip (default: false)
   --browser value, -b value           available browsers: all|opera|firefox|chrome|edge (default: "all")
   --results-dir value, --dir value    export dir (default: "results")
   --format value, -f value            format, csv|json|console (default: "csv")
   --profile-dir-path value, -p value  custom profile dir path, get with chrome://version
   --key-file-path value, -k value     custom key file path
   --help, -h                          show help (default: false)
   --version, -v                       print the version (default: false)

PS C:\test>  .\hack-browser-data.exe -b all -f json --dir results --cc
[x]:  Get 44 cookies, filename is results/microsoft_edge_cookie.json
[x]:  Get 54 history, filename is results/microsoft_edge_history.json
[x]:  Get 1 passwords, filename is results/microsoft_edge_password.json
[x]:  Get 4 bookmarks, filename is results/microsoft_edge_bookmark.json
[x]:  Get 6 bookmarks, filename is results/360speed_bookmark.json
[x]:  Get 19 cookies, filename is results/360speed_cookie.json
[x]:  Get 18 history, filename is results/360speed_history.json
[x]:  Get 1 passwords, filename is results/360speed_password.json
[x]:  Get 12 history, filename is results/qq_history.json
[x]:  Get 1 passwords, filename is results/qq_password.json
[x]:  Get 12 bookmarks, filename is results/qq_bookmark.json
[x]:  Get 14 cookies, filename is results/qq_cookie.json
[x]:  Get 28 bookmarks, filename is results/firefox_bookmark.json
[x]:  Get 10 cookies, filename is results/firefox_cookie.json
[x]:  Get 33 history, filename is results/firefox_history.json
[x]:  Get 1 passwords, filename is results/firefox_password.json
[x]:  Get 1 passwords, filename is results/chrome_password.json
[x]:  Get 4 bookmarks, filename is results/chrome_bookmark.json
[x]:  Get 6 cookies, filename is results/chrome_cookie.json
[x]:  Get 6 history, filename is results/chrome_history.json
[x]:  Compress success, zip filename is results/archive.zip
```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v0.3.7] - 2021-12-13

**新功能**  
- 为macOS和Windows添加Yandex浏览器  
- 为macOS和Windows添加CocCoc浏览器  

**修复**  
- 优化中文版README内容  
- 为AES解密添加密文长度检查  
- 更新依赖组件github.com/tidwall/gjson至1.9.3  
- 升级go-sqlite3版本，移除编译警告

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
