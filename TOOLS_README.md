# Contents

* [Open-Projects](#Open-Projects)
  * [antSword](#antSword)
  * [kunpeng](#kunpeng)
  * [myscan](#myscan)
* [Fun-tools](#Fun-tools)
  * [java-object-searcher](#java-object-searcher)
  * [Juggler](#Juggler)
  * [Redis Rogue Server](#Redis Rogue Server)


# Open-Projects

这个分类下主要包含成熟、有意义的开源项目。


## [antSword](https://github.com/AntSwordProject/antSword)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Nodejs-blue)

##### 项目链接：

https://github.com/AntSwordProject/antSword

##### 项目简述：

中国蚁剑是一款开源的跨平台网站管理工具.

##### 推荐评语：

一个真正的安全从业人员，那他一定不应该错过蚁剑。一个成熟、稳定的开源项目。

## [Kunpeng](https://github.com/opensec-cn/kunpeng)

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Go-blue)

##### 项目链接：

https://github.com/opensec-cn/kunpeng

##### 项目简述：

Kunpeng是一个Golang编写的开源POC检测框架，集成了包括数据库、中间件、web组件、cms等等的漏洞POC（[查看已收录POC列表](https://github.com/opensec-cn/kunpeng/blob/master/doc/plugin.md)），可检测弱口令、SQL注入、XSS、RCE等漏洞类型，以动态链接库的形式提供调用，通过此项目可快速开发漏洞检测类的系统，比攻击者快一步发现风险漏洞。

##### 推荐评语：

基于Golang开发的检测框架在使用过程中有着显而易见的优势，有经验的开发维护更是将这一点发挥到极致。

## [myscan](https://github.com/amcai/myscan)

![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85☆-yellow) ![](https://img.shields.io/badge/Language-Python-blue)

##### 项目链接：

https://github.com/amcai/myscan

##### 项目简述：

myscan是参考awvs的poc目录架构，pocsuite3、sqlmap等代码框架，以及搜集互联网上大量的poc，由python3开发而成的被动扫描工具。

##### 推荐评语：

被动扫描器+不断更新收集的poc+burp插件是很不错的渗透测试使用场景，不错的代码质量也是作为开源项目的保障。只是每次都需要启动redis对于日常使用来说还是有些不方便。


# Fun-tools

这个分类下有新意、解决痛点的开源项目

## [java-object-searcher](https://github.com/c0ny1/java-object-searcher)

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Java-blue)

##### 项目链接：

https://github.com/c0ny1/java-object-searcher

##### 项目简述：

java内存对象搜索辅助工具，配合IDEA在Java应用运行时，对内存中的对象进行搜索。比如可以可以用挖掘request对象用于回显等场景。

##### 推荐评语：

当你知道某个或某种类型对象存在于内存并且你刚好需要它时，却往往因为它隐藏得太深而放弃寻找，这款<java内存对象搜索辅助工具>可能帮助你从成千上万对象构成的森林中解脱。

## [Juggler](https://github.com/C4o/Juggler)

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85☆-yellow) ![](https://img.shields.io/badge/Language-Go-blue)

##### 项目链接：

https://github.com/C4o/Juggler

##### 项目简述：

一个也许能骗到黑客的系统。可以作为WAF等防护体系的一环。

##### 推荐评语：

该项目利用了渗透测试从业者在渗透测试中的惯性思维反影响攻击者，从而大幅度的影响了攻击者的渗透思路。可惜的是，该项目本身强依赖基础WAF，单靠Juggler很难提升防护本身的能力。

## [Redis Rogue Server](https://github.com/Dliv3/redis-rogue-server)

![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85☆-yellow) ![](https://img.shields.io/badge/Language-Python-blue)

##### 项目链接：

[https://github.com/Dliv3/redis-rogue-server](https://github.com/Dliv3/redis-rogue-server)

##### 项目简述：

Redis 4.x/Redis 5.x RCE利用脚本. 项目最初来源于[https://github.com/n0b0dyCN/redis-rogue-server](https://github.com/n0b0dyCN/redis-rogue-server)

##### 推荐评语：

基于主从复制的Redis getshell方式出现之后，各种利用脚本也不断被开源出来，这个脚本是完善程度最高的。不但适配了5.0.8，且实现了主动连接模式和被动链接模式，非常实用。

