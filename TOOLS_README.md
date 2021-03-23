# Contents

* [甲方工具向](#%E7%94%B2%E6%96%B9%E5%B7%A5%E5%85%B7%E5%90%91) 
  * [Threat identification 威胁识别](#threat-identification-%E5%A8%81%E8%83%81%E8%AF%86%E5%88%AB) 
  * [Mitigation measures 缓解措施](#mitigation-measures-%E7%BC%93%E8%A7%A3%E6%8E%AA%E6%96%BD) 
    * [Juggler](#juggler) 
  * [Security inspection 安全检测](#security-inspection-%E5%AE%89%E5%85%A8%E6%A3%80%E6%B5%8B) 
  	* [linglong](#linglong-) 
  * [Security Monitor 安全监控](#security-monitor-%E5%AE%89%E5%85%A8%E7%9B%91%E6%8E%A7) 
    * [gshark](#gshark-) 
* [乙方工具向](#%E4%B9%99%E6%96%B9%E5%B7%A5%E5%85%B7%E5%90%91) 
  * [Reconnaissance 信息收集](#reconnaissance-%E4%BF%A1%E6%81%AF%E6%94%B6%E9%9B%86) 
    * [HaE](#hae) 
    * [zsdevX/DarkEye](#zsdevxdarkeye) 
    * [Glass](#Glass) 
    * [AppInfoScanner](#AppInfoScanner) 
    * [ZoomEye-go](#zoomeye-go-)
  * [Vulnerability Assessment 漏洞探测](#vulnerability-assessment-%E6%BC%8F%E6%B4%9E%E6%8E%A2%E6%B5%8B) 
    * [Kunpeng](#kunpeng) 
    * [myscan](#myscan) 
    
  * [Penetration Test 攻击与利用](#penetration-test-%E6%94%BB%E5%87%BB%E4%B8%8E%E5%88%A9%E7%94%A8) 
    
    * [Redis Rogue Server](#redis-rogue-server) 
    * [CDK](#cdk-)
    * [MysqlT &amp; WhetherMysqlSham](#mysqlt--whethermysqlsham-)
    * [Viper](#viper-)
    
  * [Information analysis 信息分析](#information-analysis-%E4%BF%A1%E6%81%AF%E5%88%86%E6%9E%90) 
    * [java\-object\-searcher](#java-object-searcher) 
    * [HackBrowserData](#hackbrowserdata-) 
    * [frida\-skeleton](#frida-skeleton-) 
    * [MySQLMonitor &amp; FileMonitor](#mysqlmonitor--filemonitor-) 
    * [CodeReviewTools](#codereviewtools-)
    
  * [Back\-penetration, intranet tools  后渗透、内网工具](#back-penetration-intranet-tools--%E5%90%8E%E6%B8%97%E9%80%8F%E5%86%85%E7%BD%91%E5%B7%A5%E5%85%B7) 
    
    * [antSword](#antsword) 
    * [ServerScan](#serverscan--)
    
  * [Others 其他相关](#others-%E5%85%B6%E4%BB%96%E7%9B%B8%E5%85%B3) 
    * [passive-scan-client](#passive-scan-client) 
    * [f8x](#f8x--)

# 甲方工具向

这个分类下主要包含甲方工具向的工具，包括4个在甲方常见的安全链路。



## Threat identification 威胁识别

在攻击发生之前识别，如流量分析等 



## Mitigation measures 缓解措施

在攻击发生之中缓解威胁，如hids，waf等


### [Juggler](https://github.com/C4o/Juggler) 

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85☆-yellow) ![](https://img.shields.io/badge/Author-C4o-orange) ![](https://img.shields.io/badge/Language-Go-blue) 

##### 项目链接：

https://github.com/C4o/Juggler

##### 项目简述：

一个也许能骗到黑客的系统。可以作为WAF等防护体系的一环。

##### 推荐评语：

该项目利用了渗透测试从业者在渗透测试中的惯性思维反影响攻击者，从而大幅度的影响了攻击者的渗透思路。可惜的是，该项目本身强依赖基础WAF，单靠Juggler很难提升防护本身的能力。


## Security inspection 安全检测

对目标的安全检测，主要集中在对不同链路的主动安全检测

### [linglong](https://github.com/awake1t/linglong) ![](https://img.shields.io/badge/-New-red)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Language-Golang-blue) ![](https://img.shields.io/badge/Author-awake1t-orange)

##### 项目链接：

https://github.com/awake1t/linglong

##### 项目简述：
linglong是一款甲方资产巡航扫描系统。系统定位是发现资产，进行端口爆破。帮助企业更快发现弱口令问题。主要功能包括: 资产探测、端口爆破、定时任务、管理后台识别、报表展示.

##### 推荐评语：

一个定位为甲方的扫描系统最重要的一点就是保持维护力度以及系统本身的稳定。如果你需要这样一个系统，参考linglong会是不错的选择。

## Security Monitor 安全监控

对某个安全链路的安全监控、管理平台

### [gshark](https://github.com/madneal/gshark) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-madneal-orange) ![](https://img.shields.io/badge/Language-Go-blue) 

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

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Author-gh0stkey-orange) ![](https://img.shields.io/badge/Language-Java-blue) 

##### 项目链接：

https://github.com/gh0stkey/HaE

##### 项目简述：
HaE是一款可以快速挖掘目标指纹和关键信息的Burp插件

##### 推荐评语：

如果说为了挖掘资产和敏感信息用专用的工具太过繁重，那选择一个burp插件不失为一个好的选择，作者整理的大量指纹也是项目的一个很大的亮点。


### [zsdevX/DarkEye](https://github.com/zsdevX/DarkEye)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-zsdevX-orange) ![](https://img.shields.io/badge/Language-Go-blue) 

##### 项目链接：

https://github.com/zsdevX/DarkEye

##### 项目简述：
基于go完成的渗透测试信息收集利器

##### 推荐评语：

信息收集作为渗透测试的前置步骤一直以来都繁琐复杂，这个工具很好的集成了多个功能以及api来完成这一步，且内置图形界面的工具会让使用者的体验大大提升。


### [Glass](https://github.com/s7ckTeam/Glass)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Author-s7ckTeam-orange)  ![](https://img.shields.io/badge/Language-Python-blue) 

##### 项目链接：

https://github.com/s7ckTeam/Glass

##### 项目简述：
Glass是一款针对资产列表的快速指纹识别工具，通过调用Fofa/ZoomEye/Shodan/360等api接口快速查询资产信息并识别重点资产的指纹，也可针对IP/IP段或资产列表进行快速的指纹识别。

##### 推荐评语：

如果从大量杂乱的信息收集结果中提取有用的系统是一个亘古不变的话题，足够的指纹识别+多来源的数据不失为一个有效的手段。

### [AppInfoScanner](https://github.com/kelvinBen/AppInfoScanner)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Python-blue) ![](https://img.shields.io/badge/Author-kelvinBen-orange)

##### 项目链接：

https://github.com/kelvinBen/AppInfoScanner

##### 项目简述：
一款适用于以HW行动/红队/渗透测试团队为场景的移动端(Android、iOS、WEB、H5、静态网站)信息收集扫描工具，可以帮助渗透测试工程师、攻击队成员、红队成员快速收集到移动端或者静态WEB站点中关键的资产信息并提供基本的信息输出,如：Title、Domain、CDN、指纹信息、状态信息等。

##### 推荐评语：

从移动端APP(Android,iOS)中收集信息是在渗透测试过程中很容易忽略的一个点，如果有一个合适的工具来完成它那么最合适不过了。

### [ZoomEye-go](https://github.com/gyyyy/ZoomEye-go) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Go-blue) ![](https://img.shields.io/badge/Author-gyyyy-orange)

##### 项目链接：

https://github.com/gyyyy/ZoomEye-go

##### 项目简述：
ZoomEye-go 是一款基于 ZoomEye API 开发的 Golang 库，提供了 ZoomEye 命令行模式，同时也可以作为SDK集成到其他工具中。该库可以让技术人员更便捷地搜索、筛选、导出 ZoomEye 的数据。

##### 推荐评语：

ZoomEye-go是Golang版本的Zoomeye命令行工具，无论是直接下载release还是在使用Go编写的工具中引入都是不错的使用方案。

## Vulnerability Assessment 漏洞探测

对目标的各类漏洞探测扫描

### [Kunpeng](https://github.com/opensec-cn/kunpeng) 

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-opensec_cn-orange) ![](https://img.shields.io/badge/Language-Go-blue) 

##### 项目链接：

https://github.com/opensec-cn/kunpeng

##### 项目简述：

Kunpeng是一个Golang编写的开源POC检测框架，集成了包括数据库、中间件、web组件、cms等等的漏洞POC（[查看已收录POC列表](https://github.com/opensec-cn/kunpeng/blob/master/doc/plugin.md) ），可检测弱口令、SQL注入、XSS、RCE等漏洞类型，以动态链接库的形式提供调用，通过此项目可快速开发漏洞检测类的系统，比攻击者快一步发现风险漏洞。

##### 推荐评语：

基于Golang开发的检测框架在使用过程中有着显而易见的优势，有经验的开发维护更是将这一点发挥到极致。

### [myscan](https://github.com/amcai/myscan) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Author-amcai-orange) ![](https://img.shields.io/badge/Language-Python-blue) 

##### 项目链接：

https://github.com/amcai/myscan

##### 项目简述：

myscan是参考awvs的poc目录架构，pocsuite3、sqlmap等代码框架，以及搜集互联网上大量的poc，由python3开发而成的被动扫描工具。

##### 推荐评语：

被动扫描器+不断更新收集的poc+burp插件是很不错的渗透测试使用场景，不错的代码质量也是作为开源项目的保障。只是每次都需要启动redis对于日常使用来说还是有些不方便。

## Penetration Test 攻击与利用

在实际渗透测试过程中涉及到的工具

### [Redis Rogue Server](https://github.com/Dliv3/redis-rogue-server) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Author-Dliv3-orange) ![](https://img.shields.io/badge/Language-Python-blue) 

##### 项目链接：

[https://github.com/Dliv3/redis-rogue-server](https://github.com/Dliv3/redis-rogue-server) 

##### 项目简述：

Redis 4.x/Redis 5.x RCE利用脚本. 项目最初来源于[https://github.com/n0b0dyCN/redis-rogue-server](https://github.com/n0b0dyCN/redis-rogue-server) 

##### 推荐评语：

基于主从复制的Redis getshell方式出现之后，各种利用脚本也不断被开源出来，这个脚本是完善程度最高的。不但适配了5.0.8，且实现了主动连接模式和被动链接模式，非常实用。

### [CDK](https://github.com/cdk-team/CDK) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Go-blue) ![](https://img.shields.io/badge/Author-cdkteam-orange)

##### 项目链接：

https://github.com/cdk-team/CDK

##### 项目简述：
CDK是一款为容器环境定制的渗透测试工具，在已攻陷的容器内部提供零依赖的常用命令及PoC/EXP。集成Docker/K8s场景特有的逃逸、横向移动、持久化利用方式，插件化管理。

##### 推荐评语：

针对容器的渗透已经成了现代渗透中很重要的一环，而一款集成了各种场景以及漏洞的工具可以说是事半功倍了。

### [MysqlT](https://github.com/BeichenDream/MysqlT) & [WhetherMysqlSham](https://github.com/BeichenDream/WhetherMysqlSham) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-C%23-blue) ![](https://img.shields.io/badge/Author-BeichenDream-orange)

##### 项目链接：

- https://github.com/BeichenDream/MysqlT
- https://github.com/BeichenDream/WhetherMysqlSham

##### 项目简述：
MysqlT: 伪造Myslq服务端,并利用Mysql逻辑漏洞来获取客户端的任意文件反击攻击者.
WhetherMysqlSham：检测目标Mysql数据库是不是蜜罐。

##### 推荐评语：

针对Mysql客户端攻击可以说大家已经很熟悉了，Mysqlt可以在利用的过程中节省很多麻烦，相应的反制工具设计思路也非常有趣。

### [Viper](https://github.com/FunnyWolf/Viper) ![](https://img.shields.io/badge/-New-red)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-JS/Python-blue) ![](https://img.shields.io/badge/Author-FunnyWolf-orange)

##### 项目链接：

https://github.com/FunnyWolf/Viper

##### 项目简述：
VIPER是一款图形化内网渗透工具,将内网渗透过程中常用的战术及技术进行模块化及武器化。

##### 推荐评语：

一个好用的工具+靠谱的作者是一个开源项目成熟最关键的特点，在特殊的时期，你一定需要这样一个工具。

## Information analysis 信息分析
对在渗透测试中获取到的各种信息做分析

### [java-object-searcher](https://github.com/c0ny1/java-object-searcher) 

![](https://img.shields.io/badge/Positivity-In-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-c0ny1-orange) ![](https://img.shields.io/badge/Language-Java-blue) 

##### 项目链接：

https://github.com/c0ny1/java-object-searcher

##### 项目简述：

java内存对象搜索辅助工具，配合IDEA在Java应用运行时，对内存中的对象进行搜索。比如可以可以用挖掘request对象用于回显等场景。

##### 推荐评语：

当你知道某个或某种类型对象存在于内存并且你刚好需要它时，却往往因为它隐藏得太深而放弃寻找，这款<java内存对象搜索辅助工具>可能帮助你从成千上万对象构成的森林中解脱。

### [HackBrowserData](https://github.com/moonD4rk/HackBrowserData) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-moonD4rk-orange) ![](https://img.shields.io/badge/Language-Go-blue) 

##### 项目链接：

https://github.com/moonD4rk/HackBrowserData

##### 项目简述：
hack-browser-data 是一个解密浏览器数据（密码|历史记录|Cookies|书签）的导出工具，支持全平台主流浏览器的数据导出窃取。

##### 推荐评语：

这是一个你无论什么时候都有可能突然用上的工具，基于golang编写的项目也适用于各种不同场合。

### [frida-skeleton](https://github.com/Margular/frida-skeleton) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-Margular-orange) ![](https://img.shields.io/badge/Language-Python-blue) 

##### 项目链接：

https://github.com/Margular/frida-skeleton

##### 项目简述：
frida-skeleton是基于frida的安卓hook框架，提供了很多frida自身不支持的功能，将hook安卓变成简单便捷，人人都会的事情

##### 推荐评语：

调试apk项目时不可避免地需要用到frida来做辅助工具，这个项目建立在frida的基础上进一步优化了使用的许多细节以及体验。

### [MySQLMonitor & FileMonitor](https://github.com/TheKingOfDuck/MySQLMonitor) 

![](https://img.shields.io/badge/Positivity-IN-green) ![![](https://img.shields.io/badge/Author-madneal-orange) ](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Author-TheKingofDuck-orange) ![](https://img.shields.io/badge/Language-Java|Python-blue) 

##### 项目链接：

[https://github.com/TheKingOfDuck/MySQLMonitor](https://github.com/TheKingOfDuck/MySQLMonitor) 

[https://github.com/TheKingOfDuck/FileMonitor](https://github.com/TheKingOfDuck/FileMonitor) 

##### 项目简述：

MySQL实时监控工具(代码审计/黑盒/白盒审计辅助工具) 
文件变化实时监控工具(代码审计/黑盒/白盒审计辅助工具) 

##### 推荐评语：

这个项目可以说是很特别的一个小工具，很简单的实现方式却解决了很常见的场景，如果说开源项目最大的特点，那一定是特别的思路解决特别的痛点。

### [CodeReviewTools](https://github.com/Ppsoft1991/CodeReviewTools) ![](https://img.shields.io/badge/-New-red)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Language-Java-blue) ![](https://img.shields.io/badge/Author-Ppsoft1991-orange)

##### 项目链接：

https://github.com/Ppsoft1991/CodeReviewTools

##### 项目简述：
CodeReviewTools是一个可以快速批量反编译jar包的工具，为审计Java代码做好第一步。

##### 推荐评语：

如果你从事过Java的代码审计，你总会遇到代码和jar包混用、大量的jar包需要反编译、知道class名却不知道具体位置等等各种场景，为什么不选择一个好用的工具来帮你呢？

## Back-penetration, intranet tools  后渗透、内网工具

在渗透测试后涉及到的权限维持，或者内网渗透涉及到的工具

### [antSword](https://github.com/AntSwordProject/antSword) 

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Author-AntSwordProject-orange) ![](https://img.shields.io/badge/Language-Nodejs-blue) 

##### 项目链接：

https://github.com/AntSwordProject/antSword

##### 项目简述：

中国蚁剑是一款开源的跨平台网站管理工具.

##### 推荐评语：

一个真正的安全从业人员，那他一定不应该错过蚁剑。一个成熟、稳定的开源项目。

### [ServerScan](https://github.com/Adminisme/ServerScan)   

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Go-blue) ![](https://img.shields.io/badge/Author-Trim-orange)

##### 项目链接：

https://github.com/Adminisme/ServerScan

##### 项目简述：
一款使用Golang开发且适用于攻防演习内网横向信息收集的高并发网络扫描、服务探测工具。

##### 推荐评语：

网络扫描、服务探测工具并不稀奇。但专注于在内网环境的时候可用的工具就变少了很多，往往都需要用回nmap。这个工具依托于开发者诸多的实战经验，不但支持cs且在多种环境下都使用自如，实用体验极佳。

## Others 其他相关

其他安全链路下的安全类工具

### [passive-scan-client](https://github.com/c0ny1/passive-scan-client)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85-yellow) ![](https://img.shields.io/badge/Language-Java-blue) ![](https://img.shields.io/badge/Author-c0ny1-orange)

##### 项目链接：

https://github.com/c0ny1/passive-scan-client

##### 项目简述：
Passive Scan Client是一款可以将经过筛选的流量转发到指定代理的Burp被动扫描流量转发插件

### [f8x](https://github.com/ffffffff0x/f8x)   

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Bash-blue) ![](https://img.shields.io/badge/Author-ffffffff0x-orange)

##### 项目链接：

https://github.com/ffffffff0x/f8x

##### 项目简述：
一款红/蓝队环境自动化部署工具,支持多种场景,渗透,开发,代理环境,服务可选项等。

##### 推荐评语：

快速、针对、便携、无需环境依赖，这个工具解决了在红/蓝队场景下对环境最大的几个痛点，不得不说，这一定是深度从业者才能做的出来的好工具。