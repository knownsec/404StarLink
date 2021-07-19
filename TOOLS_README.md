# Contents

* [甲方工具向](#%E7%94%B2%E6%96%B9%E5%B7%A5%E5%85%B7%E5%90%91) 

  * [Threat identification 威胁识别](#threat-identification-%E5%A8%81%E8%83%81%E8%AF%86%E5%88%AB)

  * [Mitigation measures 缓解措施](#mitigation-measures-%E7%BC%93%E8%A7%A3%E6%8E%AA%E6%96%BD) 
	* [Elkeid](#elkeid-) 
	* [Juggler](#juggler) 
	* [OpenStar](#OpenStar)

  * [Security inspection 安全检测](#security-inspection-%E5%AE%89%E5%85%A8%E6%A3%80%E6%B5%8B) 
	* [linglong](#linglong-) 

  * [Security Monitor 安全监控](#security-monitor-%E5%AE%89%E5%85%A8%E7%9B%91%E6%8E%A7) 
    * [gshark](#gshark) 

* [乙方工具向](#%E4%B9%99%E6%96%B9%E5%B7%A5%E5%85%B7%E5%90%91) 

  * [Reconnaissance 信息收集](#reconnaissance-%E4%BF%A1%E6%81%AF%E6%94%B6%E9%9B%86) 
    * [HaE](#hae) 
    * [zsdevX/DarkEye](#zsdevxdarkeye) 
    * [Glass](#Glass) 
    * [AppInfoScanner](#AppInfoScanner) 
    * [ZoomEye-go](#zoomeye-go)

  * [Vulnerability Assessment 漏洞探测](#vulnerability-assessment-%E6%BC%8F%E6%B4%9E%E6%8E%A2%E6%B5%8B) 
    * [Kunpeng](#kunpeng) 
    * [myscan](#myscan) 
    * [Pocassist](#Pocassist)
    
  * [Penetration Test 攻击与利用](#penetration-test-%E6%94%BB%E5%87%BB%E4%B8%8E%E5%88%A9%E7%94%A8) 
    
    * [Redis Rogue Server](#redis-rogue-server) 
    * [CDK](#cdk)
    * [MysqlT &amp; WhetherMysqlSham](#mysqlt--whethermysqlsham-)
    * [Viper](#viper-)
    * [MDUT](#MDUT-)
    
  * [Information analysis 信息分析](#information-analysis-%E4%BF%A1%E6%81%AF%E5%88%86%E6%9E%90) 
    * [java\-object\-searcher](#java-object-searcher) 
    * [HackBrowserData](#hackbrowserdata) 
    * [frida\-skeleton](#frida-skeleton-) 
    * [MySQLMonitor &amp; FileMonitor](#mysqlmonitor--filemonitor) 
    * [CodeReviewTools](#codereviewtools-)
    
  * [Back\-penetration, intranet tools  后渗透、内网工具](#back-penetration-intranet-tools--%E5%90%8E%E6%B8%97%E9%80%8F%E5%86%85%E7%BD%91%E5%B7%A5%E5%85%B7) 
    
    * [antSword](#antsword) 
    * [ServerScan](#serverscan)
    * [Fscan](#fscan-)
    * [As-Exploits](#as-exploits-)
    * [Platypus](#platypus-)
    * [Stowaway](#stowaway-)
    
  * [Others 其他相关](#others-%E5%85%B6%E4%BB%96%E7%9B%B8%E5%85%B3) 
    * [passive-scan-client](#passive-scan-client) 
    * [f8x](#f8x)

# 甲方工具向

这个分类下主要包含甲方工具向的工具，包括4个在甲方常见的安全链路。



## Threat identification 威胁识别

在攻击发生之前识别，如流量分析等 



## Mitigation measures 缓解措施

在攻击发生之中缓解威胁，如hids，waf等

### [Elkeid](https://github.com/bytedance/Elkeid)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%e2%98%85-green)![](https://img.shields.io/badge/Author-bytedance-orange) ![](https://img.shields.io/badge/Language-C/Golang-blue) [![GitHub stars](https://img.shields.io/github/stars/bytedance/Elkeid.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/bytedance/Elkeid

##### 项目简述：
Elkeid是一个云原生的基于主机的入侵检测解决方案。

Elkeid 包含两大部分：

Elkeid Agent与Elkeid Driver作为数据采集层，它在Linux系统的内核和用户空间上均可使用，从而提供了具有更好性能的且更丰富的数据。
Elkeid Server可以提供百万级Agent的接入能力，采集Agent数据，支持控制与策略下发。包含实时、离线计算模块，对采集上来的数据进行分析和检测。又有自带的服务发现和管理系统，方便对整个后台管理和操作。

##### 推荐评语：

一个成熟的HIDS应该包含稳定、兼容好、性能优等各种优点，如果它还开源，那你还有什么理由不选择它呢~

### [Juggler](https://github.com/C4o/Juggler) 

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Author-C4o-orange) ![](https://img.shields.io/badge/Language-Go-blue) [![GitHub stars](https://img.shields.io/github/stars/C4o/Juggler.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/C4o/Juggler

##### 项目简述：

一个也许能骗到黑客的系统。可以作为WAF等防护体系的一环。

##### 推荐评语：

该项目利用了渗透测试从业者在渗透测试中的惯性思维反影响攻击者，从而大幅度的影响了攻击者的渗透思路。可惜的是，该项目本身强依赖基础WAF，单靠Juggler很难提升防护本身的能力。

### [OpenStar](https://github.com/starjun/openstar) ![](https://img.shields.io/badge/-New-red)
![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Lua-blue) ![](https://img.shields.io/badge/Author-starjun-orange) ![GitHub stars](https://img.shields.io/github/stars/starjun/openstar.svg?style=flat&logo=github)
##### 项目链接：
https://github.com/starjun/openstar

##### 项目简述：
OpenStar 是一个基于 OpenResty 的高性能 Web 应用防火墙，支持复杂规则编写。提供了常规的 HTTP 字段规则配置，还提供了 IP 黑白名单、访问频次等配置，对于 CC 防护更提供的特定的规则算法，并且支持搭建集群进行防护。

##### 推荐评语：
通过 OpenStar 简洁的配置文件可定制化配置一台支持复杂规则的 Web 应用防火墙


## Security inspection 安全检测

对目标的安全检测，主要集中在对不同链路的主动安全检测

### [linglong](https://github.com/awake1t/linglong)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%e2%98%86-green) ![](https://img.shields.io/badge/Author-awake1t-orange) ![](https://img.shields.io/badge/Language-Go-blue) [![GitHub stars](https://img.shields.io/github/stars/awake1t/linglong.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/awake1t/linglong

##### 项目简述：
linglong是一款甲方资产巡航扫描系统。系统定位是发现资产，进行端口爆破。帮助企业更快发现弱口令问题。主要功能包括: 资产探测、端口爆破、定时任务、管理后台识别、报表展示.

##### 推荐评语：

一个定位为甲方的扫描系统最重要的一点就是保持维护力度以及系统本身的稳定。如果你需要这样一个系统，参考linglong会是不错的选择。

## Security Monitor 安全监控

对某个安全链路的安全监控、管理平台

### [gshark](https://github.com/madneal/gshark) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-madneal-orange) ![](https://img.shields.io/badge/Language-Go-blue) [![GitHub stars](https://img.shields.io/github/stars/madneal/gshark.svg?style=flat&logo=github)]()

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

### [HaE](https://github.com/gh0stkey/HaE)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Author-gh0stkey-orange) ![](https://img.shields.io/badge/Language-Java-blue) [![GitHub stars](https://img.shields.io/github/stars/gh0stkey/HaE.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/gh0stkey/HaE

##### 项目简述：
HaE是一款可以快速挖掘目标指纹和关键信息的Burp插件

##### 推荐评语：

如果说为了挖掘资产和敏感信息用专用的工具太过繁重，那选择一个burp插件不失为一个好的选择，作者整理的大量指纹也是项目的一个很大的亮点。


### [zsdevX/DarkEye](https://github.com/zsdevX/DarkEye)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%e2%98%86-green) ![](https://img.shields.io/badge/Author-zsdevX-orange) ![](https://img.shields.io/badge/Language-Go-blue) [![GitHub stars](https://img.shields.io/github/stars/zsdevX/DarkEye.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/zsdevX/DarkEye

##### 项目简述：
基于go完成的渗透测试信息收集利器

##### 推荐评语：

信息收集作为渗透测试的前置步骤一直以来都繁琐复杂，这个工具很好的集成了多个功能以及api来完成这一步，且内置图形界面的工具会让使用者的体验大大提升。


### [Glass](https://github.com/s7ckTeam/Glass)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Author-s7ckTeam-orange) ![](https://img.shields.io/badge/Language-Python-blue) [![GitHub stars](https://img.shields.io/github/stars/s7ckTeam/Glass.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/s7ckTeam/Glass

##### 项目简述：
Glass是一款针对资产列表的快速指纹识别工具，通过调用Fofa/ZoomEye/Shodan/360等api接口快速查询资产信息并识别重点资产的指纹，也可针对IP/IP段或资产列表进行快速的指纹识别。

##### 推荐评语：

如果从大量杂乱的信息收集结果中提取有用的系统是一个亘古不变的话题，足够的指纹识别+多来源的数据不失为一个有效的手段。

### [AppInfoScanner](https://github.com/kelvinBen/AppInfoScanner)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Author-kelvinBen-orange) ![](https://img.shields.io/badge/Language-Python-blue) [![GitHub stars](https://img.shields.io/github/stars/kelvinBen/AppInfoScanner.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/kelvinBen/AppInfoScanner

##### 项目简述：
一款适用于以HW行动/红队/渗透测试团队为场景的移动端(Android、iOS、WEB、H5、静态网站)信息收集扫描工具，可以帮助渗透测试工程师、攻击队成员、红队成员快速收集到移动端或者静态WEB站点中关键的资产信息并提供基本的信息输出,如：Title、Domain、CDN、指纹信息、状态信息等。

##### 推荐评语：

从移动端APP(Android,iOS)中收集信息是在渗透测试过程中很容易忽略的一个点，如果有一个合适的工具来完成它那么最合适不过了。

### [ZoomEye-go](https://github.com/gyyyy/ZoomEye-go) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85-yellow)  ![](https://img.shields.io/badge/Author-gyyyy-orange) ![](https://img.shields.io/badge/Language-Go-blue) [![GitHub stars](https://img.shields.io/github/stars/gyyyy/ZoomEye-go.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/gyyyy/ZoomEye-go

##### 项目简述：
ZoomEye-go 是一款基于 ZoomEye API 开发的 Golang 库，提供了 ZoomEye 命令行模式，同时也可以作为SDK集成到其他工具中。该库可以让技术人员更便捷地搜索、筛选、导出 ZoomEye 的数据。

##### 推荐评语：

ZoomEye-go是Golang版本的Zoomeye命令行工具，无论是直接下载release还是在使用Go编写的工具中引入都是不错的使用方案。

## Vulnerability Assessment 漏洞探测

对目标的各类漏洞探测扫描

### [Kunpeng](https://github.com/opensec-cn/kunpeng) 

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-opensec_cn-orange) ![](https://img.shields.io/badge/Language-Go-blue) [![GitHub stars](https://img.shields.io/github/stars/opensec-cn/kunpeng.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/opensec-cn/kunpeng

##### 项目简述：

Kunpeng是一个Golang编写的开源POC检测框架，集成了包括数据库、中间件、web组件、cms等等的漏洞POC（[查看已收录POC列表](https://github.com/opensec-cn/kunpeng/blob/master/doc/plugin.md) ），可检测弱口令、SQL注入、XSS、RCE等漏洞类型，以动态链接库的形式提供调用，通过此项目可快速开发漏洞检测类的系统，比攻击者快一步发现风险漏洞。

##### 推荐评语：

基于Golang开发的检测框架在使用过程中有着显而易见的优势，有经验的开发维护更是将这一点发挥到极致。

### [myscan](https://github.com/amcai/myscan) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Author-amcai-orange) ![](https://img.shields.io/badge/Language-Python-blue) [![GitHub stars](https://img.shields.io/github/stars/amcai/myscan.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/amcai/myscan

##### 项目简述：

myscan是参考awvs的poc目录架构，pocsuite3、sqlmap等代码框架，以及搜集互联网上大量的poc，由python3开发而成的被动扫描工具。

##### 推荐评语：

被动扫描器+不断更新收集的poc+burp插件是很不错的渗透测试使用场景，不错的代码质量也是作为开源项目的保障。只是每次都需要启动redis对于日常使用来说还是有些不方便。

### [Pocassist](https://github.com/jweny/pocassist) ![](https://img.shields.io/badge/-New-red)
![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%e2%98%86-green) ![](https://img.shields.io/badge/Language-Golang-blue) ![](https://img.shields.io/badge/Author-jweny-orange) ![GitHub stars](https://img.shields.io/github/stars/jweny/pocassist.svg?style=flat&logo=github)

##### 项目链接：
https://github.com/jweny/pocassist

##### 项目简述：
Pocassist 是一个 Golang 编写的全新开源漏洞测试框架，帮助安全人员专注于漏洞验证的逻辑的实现。

Pocassist 提供了简洁的 Web 图形化界面，用户可以在线编辑漏洞验证程序即可进行批量的测试；规则完全兼容 xray，可以直接使用现有开源的 PoC 库，同时也支持添加自定义规则。

##### 推荐评语：
一套可视化的漏洞测试框架可以极大的提高渗透测试工作效率


## Penetration Test 攻击与利用

在实际渗透测试过程中涉及到的工具

### [Redis Rogue Server](https://github.com/Dliv3/redis-rogue-server) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Author-Dliv3-orange) ![](https://img.shields.io/badge/Language-Python-blue) [![GitHub stars](https://img.shields.io/github/stars/Dliv3/redis-rogue-server.svg?style=flat&logo=github)]()

##### 项目链接：

[https://github.com/Dliv3/redis-rogue-server](https://github.com/Dliv3/redis-rogue-server) 

##### 项目简述：

Redis 4.x/Redis 5.x RCE利用脚本. 项目最初来源于[https://github.com/n0b0dyCN/redis-rogue-server](https://github.com/n0b0dyCN/redis-rogue-server) 

##### 推荐评语：

基于主从复制的Redis getshell方式出现之后，各种利用脚本也不断被开源出来，这个脚本是完善程度最高的。不但适配了5.0.8，且实现了主动连接模式和被动链接模式，非常实用。

### [CDK](https://github.com/cdk-team/CDK) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-cdkteam-orange) ![](https://img.shields.io/badge/Language-Go-blue) [![GitHub stars](https://img.shields.io/github/stars/cdk-team/CDK.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/cdk-team/CDK

##### 项目简述：
CDK是一款为容器环境定制的渗透测试工具，在已攻陷的容器内部提供零依赖的常用命令及PoC/EXP。集成Docker/K8s场景特有的逃逸、横向移动、持久化利用方式，插件化管理。

##### 推荐评语：

针对容器的渗透已经成了现代渗透中很重要的一环，而一款集成了各种场景以及漏洞的工具可以说是事半功倍了。

### [MysqlT](https://github.com/BeichenDream/MysqlT) & [WhetherMysqlSham](https://github.com/BeichenDream/WhetherMysqlSham) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%e2%98%86-yellow)  ![](https://img.shields.io/badge/Author-BeichenDream-orange) ![](https://img.shields.io/badge/Language-C%23-blue) [![GitHub stars](https://img.shields.io/github/stars/BeichenDream/MysqlT.svg?style=flat&logo=github)]()

##### 项目链接：

- https://github.com/BeichenDream/MysqlT
- https://github.com/BeichenDream/WhetherMysqlSham

##### 项目简述：
MysqlT: 伪造Myslq服务端,并利用Mysql逻辑漏洞来获取客户端的任意文件反击攻击者.
WhetherMysqlSham：检测目标Mysql数据库是不是蜜罐。

##### 推荐评语：

针对Mysql客户端攻击可以说大家已经很熟悉了，Mysqlt可以在利用的过程中节省很多麻烦，相应的反制工具设计思路也非常有趣。

### [Viper](https://github.com/FunnyWolf/Viper)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-JS/Python-blue) ![](https://img.shields.io/badge/Author-FunnyWolf-orange) [![GitHub stars](https://img.shields.io/github/stars/FunnyWolf/Viper.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/FunnyWolf/Viper

##### 项目简述：
VIPER是一款图形化内网渗透工具,将内网渗透过程中常用的战术及技术进行模块化及武器化。

##### 推荐评语：

一个好用的工具+靠谱的作者是一个开源项目成熟最关键的特点，在特殊的时期，你一定需要这样一个工具。

### [MDUT](https://github.com/SafeGroceryStore/MDUT) ![](https://img.shields.io/badge/-New-red)
![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%e2%98%86-green) ![](https://img.shields.io/badge/Language-Java-blue) ![](https://img.shields.io/badge/Author-Ch1ngg-orange) ![GitHub stars](https://img.shields.io/github/stars/SafeGroceryStore/MDUT.svg?style=flat&logo=github)

##### 项目链接：
https://github.com/SafeGroceryStore/MDUT

##### 项目简述：
MDUT 全称 Multiple Database Utilization Tools，旨在将常见的数据库利用手段集合在一个程序中，打破各种数据库利用工具需要各种环境导致使用相当不便的隔阂；MDUT 使用 Java 开发，支持跨平台使用。

##### 推荐评语：
不同数据库的所需环境和利用方式不同？不用担心，MDUT 已经为你准备好了。


## Information analysis 信息分析
对在渗透测试中获取到的各种信息做分析

### [java-object-searcher](https://github.com/c0ny1/java-object-searcher) 

![](https://img.shields.io/badge/Positivity-In-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Author-c0ny1-orange) ![](https://img.shields.io/badge/Language-Java-blue) [![GitHub stars](https://img.shields.io/github/stars/c0ny1/java-object-searcher.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/c0ny1/java-object-searcher

##### 项目简述：

java内存对象搜索辅助工具，配合IDEA在Java应用运行时，对内存中的对象进行搜索。比如可以可以用挖掘request对象用于回显等场景。

##### 推荐评语：

当你知道某个或某种类型对象存在于内存并且你刚好需要它时，却往往因为它隐藏得太深而放弃寻找，这款<java内存对象搜索辅助工具>可能帮助你从成千上万对象构成的森林中解脱。

### [HackBrowserData](https://github.com/moonD4rk/HackBrowserData) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-moonD4rk-orange) ![](https://img.shields.io/badge/Language-Go-blue) [![GitHub stars](https://img.shields.io/github/stars/moonD4rk/HackBrowserData.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/moonD4rk/HackBrowserData

##### 项目简述：
hack-browser-data 是一个解密浏览器数据（密码|历史记录|Cookies|书签）的导出工具，支持全平台主流浏览器的数据导出窃取。

##### 推荐评语：

这是一个你无论什么时候都有可能突然用上的工具，基于golang编写的项目也适用于各种不同场合。

### [frida-skeleton](https://github.com/Margular/frida-skeleton) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Author-Margular-orange) ![](https://img.shields.io/badge/Language-Python-blue) [![GitHub stars](https://img.shields.io/github/stars/Margular/frida-skeleton.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/Margular/frida-skeleton

##### 项目简述：
frida-skeleton是基于frida的安卓hook框架，提供了很多frida自身不支持的功能，将hook安卓变成简单便捷，人人都会的事情

##### 推荐评语：

调试apk项目时不可避免地需要用到frida来做辅助工具，这个项目建立在frida的基础上进一步优化了使用的许多细节以及体验。

### [MySQLMonitor & FileMonitor](https://github.com/TheKingOfDuck/MySQLMonitor) 

![](https://img.shields.io/badge/Positivity-IN-green) ![![](https://img.shields.io/badge/Author-madneal-orange) ](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Author-TheKingofDuck-orange) ![](https://img.shields.io/badge/Language-Java|Python-blue) [![GitHub stars](https://img.shields.io/github/stars/TheKingOfDuck/MySQLMonitor.svg?style=flat&logo=github)]()

##### 项目链接：

[https://github.com/TheKingOfDuck/MySQLMonitor](https://github.com/TheKingOfDuck/MySQLMonitor) 

[https://github.com/TheKingOfDuck/FileMonitor](https://github.com/TheKingOfDuck/FileMonitor) 

##### 项目简述：

MySQL实时监控工具(代码审计/黑盒/白盒审计辅助工具) 
文件变化实时监控工具(代码审计/黑盒/白盒审计辅助工具) 

##### 推荐评语：

这个项目可以说是很特别的一个小工具，很简单的实现方式却解决了很常见的场景，如果说开源项目最大的特点，那一定是特别的思路解决特别的痛点。

### [CodeReviewTools](https://github.com/Ppsoft1991/CodeReviewTools) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Author-Ppsoft1991-orange) ![](https://img.shields.io/badge/Language-Java-blue) [![GitHub stars](https://img.shields.io/github/stars/Ppsoft1991/CodeReviewTools.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/Ppsoft1991/CodeReviewTools

##### 项目简述：
CodeReviewTools是一个可以快速批量反编译jar包的工具，为审计Java代码做好第一步。

##### 推荐评语：

如果你从事过Java的代码审计，你总会遇到代码和jar包混用、大量的jar包需要反编译、知道class名却不知道具体位置等等各种场景，为什么不选择一个好用的工具来帮你呢？

## Back-penetration, intranet tools  后渗透、内网工具

在渗透测试后涉及到的权限维持，或者内网渗透涉及到的工具

### [antSword](https://github.com/AntSwordProject/antSword) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-AntSwordProject-orange) ![](https://img.shields.io/badge/Language-Nodejs-blue) [![GitHub stars](https://img.shields.io/github/stars/AntSwordProject/antSword.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/AntSwordProject/antSword

##### 项目简述：

中国蚁剑是一款开源的跨平台网站管理工具.

##### 推荐评语：

一个真正的安全从业人员，那他一定不应该错过蚁剑。一个成熟、稳定的开源项目。

### [ServerScan](https://github.com/Adminisme/ServerScan)   

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-Trim-orange) ![](https://img.shields.io/badge/Language-Go-blue) [![GitHub stars](https://img.shields.io/github/stars/Adminisme/ServerScan.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/Adminisme/ServerScan

##### 项目简述：
一款使用Golang开发且适用于攻防演习内网横向信息收集的高并发网络扫描、服务探测工具。

##### 推荐评语：

网络扫描、服务探测工具并不稀奇。但专注于在内网环境的时候可用的工具就变少了很多，往往都需要用回nmap。这个工具依托于开发者诸多的实战经验，不但支持cs且在多种环境下都使用自如，实用体验极佳。

### [fscan](https://github.com/shadow1ng/fscan)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-shadow1ng-orange) ![](https://img.shields.io/badge/Language-Golang-blue) [![GitHub stars](https://img.shields.io/github/stars/shadow1ng/fscan.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/shadow1ng/fscan

##### 项目简述：
一款内网综合扫描工具，方便一键自动化、全方位漏扫扫描。

支持主机存活探测、端口扫描、常见服务的爆破、ms17010、redis批量写公钥、计划任务反弹shell、读取win网卡信息、web指纹识别、web漏洞扫描、netbios探测、域控识别等功能。

##### 推荐评语：

作为内网扫描工具，除了基本的信息搜集，还提供了一些对内网渗透很有帮助的漏洞扫描是不错的思路~

### [As-Exploits](https://github.com/yzddmr6/As-Exploits)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%e2%98%86-green) ![](https://img.shields.io/badge/Author-yzddmr6-orange) ![](https://img.shields.io/badge/Language-JavaScript-blue) [![GitHub stars](https://img.shields.io/github/stars/yzddmr6/As-Exploits.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/yzddmr6/As-Exploits

##### 项目简述：
中国蚁剑后渗透框架

##### 推荐评语：

你究竟需要一个什么样的工具来完成后渗透呢，我想一定是As-Exploits这样的~

### [Platypus](https://github.com/WangYihang/Platypus) ![](https://img.shields.io/badge/-New-red)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Golang-blue) ![](https://img.shields.io/badge/Author-WangYihang-orange) ![GitHub stars](https://img.shields.io/github/stars/WangYihang/Platypus.svg?style=flat&logo=github)

##### 项目链接：
https://github.com/WangYihang/Platypus

##### 项目简述：
Platypus 是一个基于终端与 Web UI 交互式的反弹 Shell 会话管理工具

在实际的渗透测试中，为了解决 Netcat/Socat 等工具在文件传输、多会话管理方面的不足。该工具在多会话管理的基础上增加了在渗透测试中更加有用的功能，可以更方便灵活地对反弹 Shell 会话进行管理。

##### 推荐评语：
在渗透测试中，使用 Platypus 来帮助你统一、便捷地管理多个会话，除此之外Platypus 还提供了 web 图形化界面。

### [Stowaway](https://github.com/ph4ntonn/Stowaway) ![](https://img.shields.io/badge/-New-red)
![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Golang-blue) ![](https://img.shields.io/badge/Author-ph4ntonn-orange) ![GitHub stars](https://img.shields.io/github/stars/ph4ntonn/Stowaway.svg?style=flat&logo=github)

##### 项目链接：
https://github.com/ph4ntonn/Stowaway

##### 项目简述：
Stowaway 是一款多级代理工具，可将外部流量通过多个节点代理至内网，突破内网访问限制

Stowaway 可以方便渗透测试人员通过多级跳跃，从外部dmz等一系列区域逐步深入核心网络；Stowaway 除了流量转发功能，还提供了端口复用、ssh隧道，流量伪装等专为渗透测试人员所用的功能。

##### 推荐评语：
还在为复杂的内网出网而苦恼吗？Stowaway 可以帮助你创建一条顺畅稳定的通信链路。

## Others 其他相关

其他安全链路下的安全类工具

### [passive-scan-client](https://github.com/c0ny1/passive-scan-client)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Author-c0ny1-orange) ![](https://img.shields.io/badge/Language-Java-blue) [![GitHub stars](https://img.shields.io/github/stars/c0ny1/passive-scan-client.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/c0ny1/passive-scan-client

##### 项目简述：
Passive Scan Client是一款可以将经过筛选的流量转发到指定代理的Burp被动扫描流量转发插件

### [f8x](https://github.com/ffffffff0x/f8x)   

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Author-ffffffff0x-orange) ![](https://img.shields.io/badge/Language-Bash-blue) [![GitHub stars](https://img.shields.io/github/stars/ffffffff0x/f8x.svg?style=flat&logo=github)]()

##### 项目链接：

https://github.com/ffffffff0x/f8x

##### 项目简述：
一款红/蓝队环境自动化部署工具,支持多种场景,渗透,开发,代理环境,服务可选项等。

##### 推荐评语：

快速、针对、便携、无需环境依赖，这个工具解决了在红/蓝队场景下对环境最大的几个痛点，不得不说，这一定是深度从业者才能做的出来的好工具。