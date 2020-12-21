# Contents

* [甲方工具向](#%E7%94%B2%E6%96%B9%E5%B7%A5%E5%85%B7%E5%90%91)
  * [Threat identification 威胁识别](#threat-identification-%E5%A8%81%E8%83%81%E8%AF%86%E5%88%AB)
  * [Mitigation measures 缓解措施](#mitigation-measures-%E7%BC%93%E8%A7%A3%E6%8E%AA%E6%96%BD)
    * [Juggler](#juggler)
  * [Security inspection 安全检测](#security-inspection-%E5%AE%89%E5%85%A8%E6%A3%80%E6%B5%8B)
  * [Security Monitor 安全监控](#security-monitor-%E5%AE%89%E5%85%A8%E7%9B%91%E6%8E%A7)
    * [gshark](#gshark-)
* [乙方工具向](#%E4%B9%99%E6%96%B9%E5%B7%A5%E5%85%B7%E5%90%91)
  * [Reconnaissance 信息收集](#reconnaissance-%E4%BF%A1%E6%81%AF%E6%94%B6%E9%9B%86)
  * [Vulnerability Assessment 漏洞探测](#vulnerability-assessment-%E6%BC%8F%E6%B4%9E%E6%8E%A2%E6%B5%8B)
    * [Kunpeng](#kunpeng)
    * [myscan](#myscan)
  * [Penetration Test 攻击与利用](#penetration-test-%E6%94%BB%E5%87%BB%E4%B8%8E%E5%88%A9%E7%94%A8)
    * [Redis Rogue Server](#redis-rogue-server)
  * [Information analysis 信息分析](#information-analysis-%E4%BF%A1%E6%81%AF%E5%88%86%E6%9E%90)
    * [java\-object\-searcher](#java-object-searcher)
    * [HackBrowserData](#hackbrowserdata-)
    * [frida\-skeleton](#frida-skeleton-)
    * [MySQLMonitor &amp; FileMonitor](#mysqlmonitor--filemonitor-)
  * [Back\-penetration, intranet tools  后渗透、内网工具](#back-penetration-intranet-tools--%E5%90%8E%E6%B8%97%E9%80%8F%E5%86%85%E7%BD%91%E5%B7%A5%E5%85%B7)
    * [antSword](#antsword)
  * [Others 其他相关](#others-%E5%85%B6%E4%BB%96%E7%9B%B8%E5%85%B3)

# 甲方工具向

这个分类下主要包含甲方工具向的工具，包括4个在甲方常见的安全链路。



## Threat identification 威胁识别

在攻击发生之前识别，如流量分析等 



## Mitigation measures 缓解措施

在攻击发生之中缓解威胁，如hids，waf等


### [Juggler](https://github.com/C4o/Juggler)

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85☆-yellow) ![](https://img.shields.io/badge/Language-Go-blue)

##### 项目链接：

https://github.com/C4o/Juggler

##### 项目简述：

一个也许能骗到黑客的系统。可以作为WAF等防护体系的一环。

##### 推荐评语：

该项目利用了渗透测试从业者在渗透测试中的惯性思维反影响攻击者，从而大幅度的影响了攻击者的渗透思路。可惜的是，该项目本身强依赖基础WAF，单靠Juggler很难提升防护本身的能力。


## Security inspection 安全检测

对目标的安全检测，主要集中在对不同链路的主动安全检测

## Security Monitor 安全监控

对某个安全链路的安全监控、管理平台

### [gshark](https://github.com/madneal/gshark) ![](https://img.shields.io/badge/-New-red)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Go-blue)

##### 项目链接：

https://github.com/madneal/gshark

##### 项目简述：
一款开源敏感信息监测系统，可以监测包括 github、gitlab（目前不太稳定，由于gitlab对于免费用户不提供代码全文检索API）、searchcode 多平台的敏感信息监测。。

##### 推荐评语：

开源敏感信息监控是一个无论从攻击者还是防御者看都绕不过的话题，该工具不但支持多种环境，优秀的底层以及易用的web界面都让他脱颖而出。

# 乙方工具向

这个分类下主要聚焦乙方安全从业人员的不同使用场景。

## Reconnaissance 信息收集

在渗透测试前置准备工作过程种涉及到的各类信息收集

## Vulnerability Assessment 漏洞探测

对目标的各类漏洞探测扫描

### [Kunpeng](https://github.com/opensec-cn/kunpeng)

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Go-blue)

##### 项目链接：

https://github.com/opensec-cn/kunpeng

##### 项目简述：

Kunpeng是一个Golang编写的开源POC检测框架，集成了包括数据库、中间件、web组件、cms等等的漏洞POC（[查看已收录POC列表](https://github.com/opensec-cn/kunpeng/blob/master/doc/plugin.md)），可检测弱口令、SQL注入、XSS、RCE等漏洞类型，以动态链接库的形式提供调用，通过此项目可快速开发漏洞检测类的系统，比攻击者快一步发现风险漏洞。

##### 推荐评语：

基于Golang开发的检测框架在使用过程中有着显而易见的优势，有经验的开发维护更是将这一点发挥到极致。

### [myscan](https://github.com/amcai/myscan)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85☆-yellow) ![](https://img.shields.io/badge/Language-Python-blue)

##### 项目链接：

https://github.com/amcai/myscan

##### 项目简述：

myscan是参考awvs的poc目录架构，pocsuite3、sqlmap等代码框架，以及搜集互联网上大量的poc，由python3开发而成的被动扫描工具。

##### 推荐评语：

被动扫描器+不断更新收集的poc+burp插件是很不错的渗透测试使用场景，不错的代码质量也是作为开源项目的保障。只是每次都需要启动redis对于日常使用来说还是有些不方便。

## Penetration Test 攻击与利用

在实际渗透测试过程中涉及到的工具

### [Redis Rogue Server](https://github.com/Dliv3/redis-rogue-server)

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85☆-yellow) ![](https://img.shields.io/badge/Language-Python-blue)

##### 项目链接：

[https://github.com/Dliv3/redis-rogue-server](https://github.com/Dliv3/redis-rogue-server)

##### 项目简述：

Redis 4.x/Redis 5.x RCE利用脚本. 项目最初来源于[https://github.com/n0b0dyCN/redis-rogue-server](https://github.com/n0b0dyCN/redis-rogue-server)

##### 推荐评语：

基于主从复制的Redis getshell方式出现之后，各种利用脚本也不断被开源出来，这个脚本是完善程度最高的。不但适配了5.0.8，且实现了主动连接模式和被动链接模式，非常实用。


## Information analysis 信息分析
对在渗透测试中获取到的各种信息做分析

### [java-object-searcher](https://github.com/c0ny1/java-object-searcher)

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Java-blue)

##### 项目链接：

https://github.com/c0ny1/java-object-searcher

##### 项目简述：

java内存对象搜索辅助工具，配合IDEA在Java应用运行时，对内存中的对象进行搜索。比如可以可以用挖掘request对象用于回显等场景。

##### 推荐评语：

当你知道某个或某种类型对象存在于内存并且你刚好需要它时，却往往因为它隐藏得太深而放弃寻找，这款<java内存对象搜索辅助工具>可能帮助你从成千上万对象构成的森林中解脱。

### [HackBrowserData](https://github.com/moonD4rk/HackBrowserData) ![](https://img.shields.io/badge/-New-red)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Go-blue)

##### 项目链接：

https://github.com/moonD4rk/HackBrowserData

##### 项目简述：
hack-browser-data 是一个解密浏览器数据（密码|历史记录|Cookies|书签）的导出工具，支持全平台主流浏览器的数据导出窃取。

##### 推荐评语：

这是一个你无论什么时候都有可能突然用上的工具，基于golang编写的项目也适用于各种不同场合。

### [frida-skeleton](https://github.com/Margular/frida-skeleton) ![](https://img.shields.io/badge/-New-red)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Python-blue)

##### 项目链接：

https://github.com/Margular/frida-skeleton

##### 项目简述：
frida-skeleton是基于frida的安卓hook框架，提供了很多frida自身不支持的功能，将hook安卓变成简单便捷，人人都会的事情

##### 推荐评语：

调试apk项目时不可避免地需要用到frida来做辅助工具，这个项目建立在frida的基础上进一步优化了使用的许多细节以及体验。

### [MySQLMonitor & FileMonitor](https://github.com/TheKingOfDuck/MySQLMonitor) ![](https://img.shields.io/badge/-New-red)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Language-Java|Python-blue)

##### 项目链接：

[https://github.com/TheKingOfDuck/MySQLMonitor](https://github.com/TheKingOfDuck/MySQLMonitor)

[https://github.com/TheKingOfDuck/FileMonitor](https://github.com/TheKingOfDuck/FileMonitor)

##### 项目简述：

MySQL实时监控工具(代码审计/黑盒/白盒审计辅助工具)
文件变化实时监控工具(代码审计/黑盒/白盒审计辅助工具)

##### 推荐评语：

这个项目可以说是很特别的一个小工具，很简单的实现方式却解决了很常见的场景，如果说开源项目最大的特点，那一定是特别的思路解决特别的痛点。

## Back-penetration, intranet tools  后渗透、内网工具

在渗透测试后涉及到的权限维持，或者内网渗透涉及到的工具

### [antSword](https://github.com/AntSwordProject/antSword)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Nodejs-blue)

##### 项目链接：

https://github.com/AntSwordProject/antSword

##### 项目简述：

中国蚁剑是一款开源的跨平台网站管理工具.

##### 推荐评语：

一个真正的安全从业人员，那他一定不应该错过蚁剑。一个成熟、稳定的开源项目。

## Others 其他相关

其他安全链路下的安全类工具

