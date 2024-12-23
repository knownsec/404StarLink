## 全部项目 / All_Projects

* [甲方工具/party_a](#甲方工具party_a)
    * [dperf](#dperf)
    * [Elkeid](#elkeid)
    * [linglong](#linglong)
    * [murphysec](#murphysec)
    * [veinmind-tools](#veinmind-tools)
    * [camille](#camille)
    * [appshark](#appshark)
    * [Tai-e](#tai-e)
    * [OpenStar](#openstar)
    * [gshark](#gshark)
    * [AppScan](#appscan)
    * [Juggler](#juggler)
    * [vArmor](#varmor)
    * [Hades](#hades)

* [信息收集/reconnaissance](#信息收集reconnaissance)
    * [HaE](#hae)
    * [AppInfoScanner](#appinfoscanner)
    * [ENScanGo](#enscango)
    * [Kunyu](#kunyu)
    * [Glass](#glass)
    * [ksubdomain](#ksubdomain)
    * [scaninfo](#scaninfo)
    * [ZoomEye-Python](#zoomeye-python)
    * [ct](#ct)
    * [ZoomEye-Tools](#zoomeye-tools)
    * [ZoomEye-go](#zoomeye-go)
    * [vultrap](#vultrap)
    * [xtate](#xtate)

* [漏洞探测/vulnerability_assessment](#漏洞探测vulnerability_assessment)
    * [afrog](#afrog)
    * [Kunpeng](#kunpeng)
    * [Pocassist](#pocassist)
    * [myscan](#myscan)
    * [LSpider](#lspider)

* [攻击与利用/penetration_test](#攻击与利用penetration_test)
    * [dperf](#dperf)
    * [CDK](#cdk)
    * [Viper](#viper)
    * [pocsuite3](#pocsuite3)
    * [MDUT](#mdut)
    * [JYso](#jyso)
    * [BurpCrypto](#burpcrypto)
    * [WMIHACKER](#wmihacker)
    * [MySQL-Fake-Server](#mysql-fake-server)
    * [ysomap](#ysomap)
    * [DNSlog-GO](#dnslog-go)
    * [Cloud-Bucket-Leak-Detection-Tools](#cloud-bucket-leak-detection-tools)
    * [Antenna](#antenna)
    * [Redis-Rogue-Server](#redis-rogue-server)
    * [Cola-Dnslog](#cola-dnslog)
    * [GrabAccess](#grabaccess)
    * [MysqlT](#mysqlt)

* [信息分析/information_analysis](#信息分析information_analysis)
    * [HackBrowserData](#hackbrowserdata)
    * [KunLun-M](#kunlun-m)
    * [Pillager](#pillager)
    * [AppScan](#appscan)
    * [frida-skeleton](#frida-skeleton)
    * [java-object-searcher](#java-object-searcher)
    * [js-cookie-monitor-debugger-hook](#js-cookie-monitor-debugger-hook)
    * [MySQLMonitor](#mysqlmonitor)
    * [CodeReviewTools](#codereviewtools)

* [内网工具/intranet_tools](#内网工具intranet_tools)
    * [fscan](#fscan)
    * [antSword](#antsword)
    * [Stowaway](#stowaway)
    * [shellcodeloader](#shellcodeloader)
    * [ServerScan](#serverscan)
    * [Platypus](#platypus)
    * [WMIHACKER](#wmihacker)
    * [rakshasa](#rakshasa)
    * [As-Exploits](#as-exploits)
    * [PortForward](#portforward)

* [其他/others](#其他others)
    * [f8x](#f8x)
    * [BinAbsInspector](#binabsinspector)
    * [Heimdallr](#heimdallr)
    * [passive-scan-client](#passive-scan-client)
    * [GrabAccess](#grabaccess)
    * [wam](#wam)
    * [LBot](#lbot)

----------------------------------------

## 甲方工具/party_a
### [dperf](detail/dperf.md)
![Author](https://img.shields.io/badge/Author-Benjamin-orange)
![Language](https://img.shields.io/badge/Language-C-blue)
![GitHub stars](https://img.shields.io/github/stars/baidu/dperf.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.8.0-red)

<https://github.com/baidu/dperf>

dperf 是一个100Gbps的网络性能与压力测试软件。国内多个知名安全厂商用dperf测试其防火墙。知名开源四层负载均衡DPVS在用dperf做性能测试，发布性能测试报告。

### [Elkeid](detail/Elkeid.md)
![Author](https://img.shields.io/badge/Author-bytedance-orange)
![Language](https://img.shields.io/badge/Language-C/Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/bytedance/Elkeid.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)

<https://github.com/bytedance/Elkeid>

Elkeid是一个云原生的基于主机的安全(入侵检测与风险识别)解决方案。Elkeid 包含两大部分：Elkeid Agent与Elkeid Driver作为数据采集层，它在Linux系统的内核和用户空间上均可使用，从而提供了具有更好性能的且更丰富的数据。 Elkeid Server可以提供百万级Agent的接入能力，采集Agent数据，支持控制与策略下发。包含实时、离线计算模块，对采集上来的数据进行分析和检测。又有自带的服务发现和管理系统，方便对整个后台管理和操作。

### [linglong](detail/linglong.md)
![Author](https://img.shields.io/badge/Author-awake1t-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/awake1t/linglong.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)

<https://github.com/awake1t/linglong>

linglong是一款甲方资产巡航扫描系统。系统定位是发现资产，进行端口爆破。帮助企业更快发现弱口令问题。主要功能包括: 资产探测、端口爆破、定时任务、管理后台识别、报表展示。

### [murphysec](detail/murphysec.md)
![Author](https://img.shields.io/badge/Author-murphysecurity-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/murphysecurity/murphysec.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.10.0-red)

<https://github.com/murphysecurity/murphysec>

墨菲安全专注于软件供应链安全，murphysec 是墨菲安全的 CLI 工具，用于在命令行检测指定目录代码的依赖安全问题，也可以基于 CLI 工具实现在 CI 流程的检测。

### [veinmind-tools](detail/veinmind-tools.md)
![Author](https://img.shields.io/badge/Author-长亭科技-orange)
![Language](https://img.shields.io/badge/Language-Golang/Python-blue)
![GitHub stars](https://img.shields.io/github/stars/chaitin/veinmind-tools.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1.5-red)

<https://github.com/chaitin/veinmind-tools>

veinmind-tools 是基于 veinmind-sdk 打造的一个容器安全工具集，目前已支持镜像 恶意文件/后门/敏感信息/弱口令 的扫描，更多功能正在逐步开发中。

### [camille](detail/camille.md)
![Author](https://img.shields.io/badge/Author-zhengjim-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/zhengjim/camille.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)

<https://github.com/zhengjim/camille>

现如今APP隐私合规十分重要，各监管部门不断开展APP专项治理工作及核查通报，不合规的APP通知整改或直接下架。camille可以hook住Android敏感接口，并识别是否为第三方SDK调用。根据隐私合规的场景，辅助检查是否符合隐私合规标准。

### [appshark](detail/appshark.md)
![Author](https://img.shields.io/badge/Author-bytedance-orange)
![Language](https://img.shields.io/badge/Language-Kotlin-blue)
![GitHub stars](https://img.shields.io/github/stars/bytedance/appshark.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.1.2-red)

<https://github.com/bytedance/appshark>

Appshark 是一个针对安卓的静态分析工具，它的设计目标是针对超大型App的分析，Appshark支持基于json的自定义扫描规则,发现自己关心的安全漏洞以及隐私合规问题，支持灵活配置，可以在准确率以及扫描时间空间之间寻求平衡，支持自定义扩展规则，根据自己的业务需要，进行定制分析

### [Tai-e](detail/Tai-e.md)
![Author](https://img.shields.io/badge/Author-pascal_lab-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/pascal-lab/Tai-e.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.2.2-red)

<https://github.com/pascal-lab/Tai-e>

Tai-e（太阿）是一个通用型Java程序分析框架，包含了开发程序分析技术所需的各类基础设施，并提供了可配置性高、功能强大的污点分析系统，用于检测各类隐私泄露、注入攻击等安全漏洞。

### [OpenStar](detail/OpenStar.md)
![Author](https://img.shields.io/badge/Author-starjun-orange)
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![GitHub stars](https://img.shields.io/github/stars/starjun/openstar.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)

<https://github.com/starjun/openstar>

OpenStar 是一个基于 OpenResty 的高性能 Web 应用防火墙，支持复杂规则编写。提供了常规的 HTTP 字段规则配置，还提供了 IP 黑白名单、访问频次等配置，对于 CC 防护更提供的特定的规则算法，并且支持搭建集群进行防护。

### [GShark](detail/gshark.md)
![Author](https://img.shields.io/badge/Author-madneal-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/madneal/gshark.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.0-red)

<https://github.com/madneal/gshark>

一款开源敏感信息检测系统，可以监测包括 GitHub, GitLab(支持私有部署版本), Postman, searchcode 多个平台的敏感信息监测。

### [AppScan](detail/AppScan.md)
![Author](https://img.shields.io/badge/Author-TongchengOpenSource-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/TongchengOpenSource/AppScan.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1.5-red)

<https://github.com/TongchengOpenSource/AppScan>

安全隐私卫士（AppScan）一款免费的企业级自动化App隐私合规检测工具

### [Juggler](detail/Juggler.md)
![Author](https://img.shields.io/badge/Author-C4o-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/C4o/Juggler.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)

<https://github.com/C4o/Juggler>

一个也许能骗到黑客的系统，可以作为WAF等防护体系的一环。

### [vArmor](detail/vArmor.md)
![Author](https://img.shields.io/badge/Author-bytedance-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/bytedance/vArmor.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.6.1-red)

<https://github.com/bytedance/vArmor>

vArmor 是一个云原生容器沙箱系统，它借助 Linux 的 LSM 技术（AppArmor & BPF）实现强制访问控制器（即 enforcer），从而对容器进行安全加固。它可以用于增强容器隔离性、减少内核攻击面、增加容器逃逸或横行移动攻击的难度与成本。vArmor 遵循 Kubernetes Operator 设计模式，用户可通过操作 CRD API 对特定的 Workload 进行加固。从而以更贴近业务的视角，实现对容器化微服务的沙箱加固。此外 vArmor 还包含多种内置加固策略，具备开箱即用的特性。

### [Hades](detail/Hades.md)
![Author](https://img.shields.io/badge/Author-theSecHunter-orange)
![Language](https://img.shields.io/badge/Language-Golang&C++&C-blue)
![GitHub stars](https://img.shields.io/github/stars/theSecHunter/Hades.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1.0-red)

<https://github.com/theSecHunter/Hades>

Hades 是一款支持 Windows/Linux 的内核级别数据采集主机入侵检测系统，其中每个插件均可独立分开运行。



## 信息收集/reconnaissance
### [HaE](detail/HaE.md)
![Author](https://img.shields.io/badge/Author-gh0stkey-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/gh0stkey/HaE.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V4.0-red)

<https://github.com/gh0stkey/HaE>

HaE是一款可以快速挖掘目标指纹和关键信息的Burp插件。

### [AppInfoScanner](detail/AppInfoScanner.md)
![Author](https://img.shields.io/badge/Author-kelvinBen-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/kelvinBen/AppInfoScanner.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.9-red)

<https://github.com/kelvinBen/AppInfoScanner>

一款适用于以HW行动/红队/渗透测试团队为场景的移动端(Android、iOS、WEB、H5、静态网站)信息收集扫描工具，可以帮助渗透测试工程师、攻击队成员、红队成员快速收集到移动端或者静态WEB站点中关键的资产信息并提供基本的信息输出,如：Title、Domain、CDN、指纹信息、状态信息等。

### [ENScanGo](detail/ENScanGo.md)
![Author](https://img.shields.io/badge/Author-wgpsec-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/wgpsec/ENScan_GO.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1.0-red)

<https://github.com/wgpsec/ENScan_GO>

一款基于各大企业信息API的工具，解决在遇到的各种针对国内企业信息收集难题。一键收集控股公司ICP备案、APP、小程序、微信公众号等信息聚合导出。

### [Kunyu](detail/Kunyu.md)
![Author](https://img.shields.io/badge/Author-风起-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/knownsec/Kunyu.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.7.2-red)

<https://github.com/knownsec/Kunyu>

Kunyu(坤舆)，是一款基于ZoomEye API开发的信息收集工具，旨在让企业资产收集更高效，使更多安全相关从业者了解、使用网络空间测绘技术。

### [Glass](detail/Glass.md)
![Author](https://img.shields.io/badge/Author-s7ckTeam-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/s7ckTeam/Glass.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.0.6-red)

<https://github.com/s7ckTeam/Glass>

Glass是一款针对资产列表的快速指纹识别工具，通过调用Fofa/ZoomEye/Shodan/360等api接口快速查询资产信息并识别重点资产的指纹，也可针对IP/IP段或资产列表进行快速的指纹识别。

### [ksubdomain](detail/ksubdomain.md)
![Author](https://img.shields.io/badge/Author-w8ay-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/boy-hack/ksubdomain.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.9.5-red)

<https://github.com/boy-hack/ksubdomain>

ksubdomain是一款基于无状态子域名爆破工具，支持在Windows/Linux/Mac上使用，它会很快的进行DNS爆破，在Mac和Windows上理论最大发包速度在30w/s,linux上为160w/s的速度。

### [scaninfo](detail/scaninfo.md)
![Author](https://img.shields.io/badge/Author-华东360安服团队-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/redtoolskobe/scaninfo.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1.0-red)

<https://github.com/redtoolskobe/scaninfo>

scaninfo 是一款开源、轻量、快速、跨平台的红队内外网打点扫描器。比较同类工具，其能够在 nmap 的扫描速度和 masscan 的准确度之间寻找一个较好的平衡点，能够快速进行端口扫描和服务识别，内置指纹识别用于 web 探测，可以用报告的方式整理扫描结果。

### [ZoomEye-Python](detail/ZoomEye-Python.md)
![Author](https://img.shields.io/badge/Author-Knownsec404-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/knownsec/ZoomEye-python.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.2.0-red)

<https://github.com/knownsec/ZoomEye-python>

ZoomEye-python 是一款基于 ZoomEye API 开发的 Python 库，提供了 ZoomEye 命令行模式，同时也可以作为 SDK 集成到其他工具中。该库可以让技术人员更便捷地搜索、筛选、导出 ZoomEye 的数据

### [ct](detail/ct.md)
![Author](https://img.shields.io/badge/Author-rungobier@Knownsec404-orange)
![Language](https://img.shields.io/badge/Language-Rust-blue)
![GitHub stars](https://img.shields.io/github/stars/knownsec/ct.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.9-red)

<https://github.com/knownsec/ct>

ct 是一款使用 rust 语言进行开发，并且基于ZoomEye域名查询以及利用域名字典进行子域名爆破的工具，同时在最终爆破完成后可使用脚本，将相应的的.gv 文件转化成为相应的 .png 文件进行可视化展示

### [Zoomeye-Tools](detail/ZoomEye-Tools.md)
![Author](https://img.shields.io/badge/Author-Knownsec404-orange)
![Language](https://img.shields.io/badge/Language-JS-blue)
![GitHub stars](https://img.shields.io/github/stars/knownsec/Zoomeye-Tools.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.3.2-red)

<https://github.com/knownsec/Zoomeye-Tools>

一个配合ZoomEye使用的Chrome插件，可以查看当前网页所在ip信息或跳转查看详细信息，还可以根据关键词一键跳转至ZoomEye进行搜索

### [ZoomEye-go](detail/ZoomEye-go.md)
![Author](https://img.shields.io/badge/Author-gyyyy-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/gyyyy/ZoomEye-go.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.0-red)

<https://github.com/gyyyy/ZoomEye-go>

ZoomEye-go 是一款基于 ZoomEye API 开发的 Golang 库，提供了 ZoomEye 命令行模式，同时也可以作为SDK集成到其他工具中。该库可以让技术人员更便捷地搜索、筛选、导出 ZoomEye 的数据。

### [vultrap](detail/vultrap.md)
![Author](https://img.shields.io/badge/Author-liqzz-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/liqzz/vultrap.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)

<https://github.com/liqzz/vultrap>

在开源领域，从来不缺少优秀的漏洞POC框架和POC，现今情况下，当有相关漏洞的漏洞情报出现的时候，其用于漏洞的验证的POC代码或利用请求都会很快的被公布在互联网上，比如Nuclei等漏洞检测框架也会即时得跟进新的漏洞，并以漏洞检测模板的形式进行更新，如nuclei 的nuclei-temaplte 仓库几乎每天都会出现新的漏洞需求和检测模板提交。对于漏洞检测模板而言，其主要目的用来验证目标是否存在漏洞，但仔细了解漏洞检测的机制之后，漏洞检测大多数情况下实际就是构造请求和判断响应的过程，那么基于次，是否可以反向思维，通过判断漏洞验证的请求来返回迷惑性的结果，扰乱扫描器的判断呢，其实本质还是honeypot的思路，也可以称“漏洞伪装”，也是本项目 vultrap的实现背景。

### [xtate](detail/xtate.md)
![Author](https://img.shields.io/badge/Author-sharkocha-orange)
![Language](https://img.shields.io/badge/Language-C-blue)
![GitHub stars](https://img.shields.io/github/stars/sharkocha/xtate.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.5.0-red)

<https://github.com/sharkocha/xtate>

Xtate是面向互联网规模网络测量的模块化全栈扫描器（框架）。利用自研的应用层无状态扫描模型ZBanner和混合状态轻量级TCP协议栈HLTCP实现异步高速扫描。与已有的无状态端口扫描器只能探测端口是否开放不同，Xtate基于应用层无状态扫描模型，在千兆带宽下能够在6分钟内完成中国大陆地址集中所有80端口的开放性检测和Banner抓取。基于HLTCP用户态协议栈实现和TLS支持，Xtate也能够在有状态模式下执行多轮数据交互的高速扫描，包括TLS上层服务Banner抓取。Xtate框架提供统一接口以自定义模块实现不同的扫描任务，专注于大规模网络的协议层面测量（包括传输层、应用层和TLS上层服务），具有坚实的底层高速异步数据包收发机制，期望为学术和实践领域中大规模网络测量的各种算法和任务提供承载平台。



## 漏洞探测/vulnerability_assessment
### [afrog](detail/afrog.md)
![Author](https://img.shields.io/badge/Author-zan8in-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/zan8in/afrog.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V3.1.3-red)

<https://github.com/zan8in/afrog>

afrog 是一款性能卓越、快速稳定、PoC 可定制的漏洞扫描工具，PoC 包含 CVE、CNVD、默认口令、信息泄露、指纹识别、未授权访问、任意文件读取、命令执行等多种漏洞类型，帮助网络安全从业者快速验证并及时修复漏洞。

### [Kunpeng](detail/Kunpeng.md)
![Author](https://img.shields.io/badge/Author-opensec-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/opensec-cn/kunpeng.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)

<https://github.com/opensec-cn/kunpeng>

Kunpeng是一个Golang编写的开源POC检测框架，集成了包括数据库、中间件、web组件、cms等等的漏洞POC，可检测弱口令、SQL注入、XSS、RCE等漏洞类型，以动态链接库的形式提供调用，通过此项目可快速开发漏洞检测类的系统，比攻击者快一步发现风险漏洞。

### [Pocassist](detail/Pocassist.md)
![Author](https://img.shields.io/badge/Author-jweny-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/jweny/pocassist.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.5-red)

<https://github.com/jweny/pocassist>

Pocassist 是一个 Golang 编写的全新开源漏洞测试框架，帮助安全人员专注于漏洞验证的逻辑的实现。Pocassist 提供了简洁的 Web 图形化界面，用户可以在线编辑漏洞验证程序即可进行批量的测试；规则完全兼容 xray，可以直接使用现有开源的 PoC 库，同时也支持添加自定义规则。

### [myscan](detail/myscan.md)
![Author](https://img.shields.io/badge/Author-amcai-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/amcai/myscan.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)

<https://github.com/amcai/myscan>

myscan是参考awvs的poc目录架构，pocsuite3、sqlmap等代码框架，以及搜集互联网上大量的poc，由python3开发而成的被动扫描工具。

### [LSpider](detail/LSpider.md)
![Author](https://img.shields.io/badge/Author-LoRexxar-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/knownsec/LSpider.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.2-red)

<https://github.com/knownsec/LSpider>

LSpider 一个为被动扫描器定制的前端爬虫



## 攻击与利用/penetration_test
### [dperf](detail/dperf.md)
![Author](https://img.shields.io/badge/Author-Benjamin-orange)
![Language](https://img.shields.io/badge/Language-C-blue)
![GitHub stars](https://img.shields.io/github/stars/baidu/dperf.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.8.0-red)

<https://github.com/baidu/dperf>

dperf 是一个100Gbps的网络性能与压力测试软件。国内多个知名安全厂商用dperf测试其防火墙。知名开源四层负载均衡DPVS在用dperf做性能测试，发布性能测试报告。

### [CDK](detail/CDK.md)
![Author](https://img.shields.io/badge/Author-cdkteam-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/cdk-team/CDK.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.4-red)

<https://github.com/cdk-team/CDK>

CDK是一款为容器环境定制的渗透测试工具，在已攻陷的容器内部提供零依赖的常用命令及PoC/EXP。集成Docker/K8s场景特有的逃逸、横向移动、持久化利用方式，插件化管理。

### [Viper](detail/Viper.md)
![Author](https://img.shields.io/badge/Author-FunnyWolf-orange)
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![GitHub stars](https://img.shields.io/github/stars/FunnyWolf/Viper.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V3.0.0-red)

<https://github.com/FunnyWolf/Viper>

VIPER是一款图形化内网渗透工具,将内网渗透过程中常用的战术及技术进行模块化及武器化。

### [pocsuite3](detail/pocsuite3.md)
![Author](https://img.shields.io/badge/Author-knownsec404-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/knownsec/pocsuite3.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.0.8-red)

<https://github.com/knownsec/pocsuite3>

pocsuite3是由Knownsec 404团队开发的开源远程漏洞测试和概念验证开发框架。它带有强大的概念验证引擎，以及针对最终渗透测试人员和安全研究人员的许多强大功能。

### [MDUT](detail/MDUT.md)
![Author](https://img.shields.io/badge/Author-Ch1ngg-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/SafeGroceryStore/MDUT.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1.1-red)

<https://github.com/SafeGroceryStore/MDUT>

MDUT 全称 Multiple Database Utilization Tools，旨在将常见的数据库利用手段集合在一个程序中，打破各种数据库利用工具需要各种环境导致使用相当不便的隔阂；MDUT 使用 Java 开发，支持跨平台使用。

### [JYso](detail/JYso.md)
![Author](https://img.shields.io/badge/Author-qi4L-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/qi4L/JYso.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.3.5-red)

<https://github.com/qi4L/JYso>

JYso是一个可以用于 jndi 注入攻击和生成反序列化数据流的工具，既可以当 JNDIExploit 用也可以当作 ysoserial 使用。

### [BurpCrypto](detail/BurpCrypto.md)
![Author](https://img.shields.io/badge/Author-whwlsfb-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/whwlsfb/BurpCrypto.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)

<https://github.com/whwlsfb/BurpCrypto>

支持多种加密算法或直接执行JS代码的用于爆破前端加密的BurpSuite插件。

### [WMIHACKER](detail/WMIHACKER.md)
![Author](https://img.shields.io/badge/Author-rootclay-orange)
![Language](https://img.shields.io/badge/Language-VBScript-blue)
![GitHub stars](https://img.shields.io/github/stars/rootclay/WMIHACKER.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)

<https://github.com/rootclay/WMIHACKER>

WMIHACKER是一款免杀横向渗透远程命令执行工具，常见的WMIEXEC、PSEXEC执行命令是创建服务或调用Win32_Process.create执行命令，这些方式都已经被杀软100%拦截，通过改造出的WMIHACKER可免杀横向移动。并且在企业网络目前阻断445端口严重的情况下可以无需445端口进行横向移动，效率高且不易被检测。

### [MySQL-Fake-Server](detail/MySQL-Fake-Server.md)
![Author](https://img.shields.io/badge/Author-fnmsd-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/fnmsd/MySQL_Fake_Server.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)

<https://github.com/fnmsd/MySQL_Fake_Server>

用于渗透测试过程中的假MySQL服务器，纯原生python3实现，不依赖其它包。

### [ysomap](detail/ysomap.md)
![Author](https://img.shields.io/badge/Author-wh1t3p1g-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/wh1t3p1g/ysomap.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.1.4-red)

<https://github.com/wh1t3p1g/ysomap>

Ysomap是一款适配于各类实际复杂环境的Java反序列化利用框架，可动态配置具备不同执行效果的Java反序列化利用链payload，以应对不同场景下的反序列化利用。

### [DNSlog-GO](detail/DNSlog-GO.md)
![Author](https://img.shields.io/badge/Author-lanyi-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/lanyi1998/DNSlog-GO.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.2-red)

<https://github.com/lanyi1998/DNSlog-GO>

DNSLog-GO 是一款golang编写的监控 DNS 解析记录的工具，自带WEB界面。单文件运行，无依赖。部署方便快捷。

### [Cloud-Bucket-Leak-Detection-Tools](detail/Cloud-Bucket-Leak-Detection-Tools.md)
![Author](https://img.shields.io/badge/Author-UzJu-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/UzJu/Cloud-Bucket-Leak-Detection-Tools.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.4.0-red)

<https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools>

Cloud-Bucket-Leak-Detection-Tools是一款针对云厂商存储桶扫描检测与利用的工具

### [Antenna](detail/Antenna.md)
![Author](https://img.shields.io/badge/Author-wuba-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/wuba/Antenna.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.3.5-red)

<https://github.com/wuba/Antenna>

Antenna是58同城安全团队打造的一款辅助安全从业人员辅助验证网络中多种漏洞是否存在以及可利用性的工具。其基于带外应用安全测试( OAST)通过任务的形式，将不同漏洞场景检测能力通过插件的形式进行集合，通过与目标进行Out-of-bind的数据通信方式进行辅助检测。

### [Redis-Rogue-Server](detail/Redis-Rogue-Server.md)
![Author](https://img.shields.io/badge/Author-Dliv3-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/Dliv3/redis-rogue-server.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)

<https://github.com/Dliv3/redis-rogue-server>

Redis 4.x/Redis 5.x RCE利用脚本. 项目最初来源于 <https://github.com/n0b0dyCN/redis-rogue-server>

### [Cola-Dnslog](detail/Cola-Dnslog.md)
![Author](https://img.shields.io/badge/Author-AbelChe-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/AbelChe/cola_dnslog.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)

<https://github.com/AbelChe/cola_dnslog>

Cola Dnslog 是一款更加强大的dnslog平台(无回显漏洞探测辅助平台)，支持dns http ldap rmi等协议，提供API调用方式便于与其他工具结合，支持钉钉机器人、Bark等提醒，并支持docker一键部署。

### [GrabAccess](detail/GrabAccess.md)
![Author](https://img.shields.io/badge/Author-Push3AX-orange)
![Language](https://img.shields.io/badge/Language-C-blue)
![GitHub stars](https://img.shields.io/github/stars/Push3AX/GrabAccess.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1-red)

<https://github.com/Push3AX/GrabAccess>

GrabAccess：Bookit/Windows登陆密码和Bitlocker绕过工具，在物理接触目标计算机的情况下，GrabAccess可以：绕过Windows登陆密码执行任意操作（以System权限执行命令、重置Windows账户密码等），植入木马并添加自启动（可以绕过Bitlocker，但要求受害者登录），通过修改主板UEFI固件实现无视重装系统、更换硬盘的持久化（Bootkit）

### [MysqlT](detail/MysqlT.md)
![Author](https://img.shields.io/badge/Author-BeichenDream-orange)
![Language](https://img.shields.io/badge/Language-C%23-blue)
![GitHub stars](https://img.shields.io/github/stars/BeichenDream/MysqlT.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)

<https://github.com/BeichenDream/MysqlT>

伪造Myslq服务端,并利用Mysql逻辑漏洞来获取客户端的任意文件反击攻击。



## 信息分析/information_analysis
### [HackBrowserData](detail/HackBrowserData.md)
![Author](https://img.shields.io/badge/Author-moonD4rk-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/moonD4rk/HackBrowserData.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.4.6-red)

<https://github.com/moonD4rk/HackBrowserData>

hack-browser-data 是一个解密浏览器数据（密码/历史记录/Cookies/书签）的导出工具，支持全平台主流浏览器的数据导出窃取。

### [KunLun-M](detail/KunLun-M.md)
![Author](https://img.shields.io/badge/Author-LoRexxar-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/LoRexxar/Kunlun-M.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.6.5-red)

<https://github.com/LoRexxar/Kunlun-M>

KunLun-M是一个完全开源的静态白盒扫描工具，支持PHP、JavaScript的语义扫描，基础安全、组件安全扫描，Chrome Ext\Solidity的基础扫描。

### [Pillager](detail/Pillager.md)
![Author](https://img.shields.io/badge/Author-qwqdanchun-orange)
![Language](https://img.shields.io/badge/Language-C#-blue)
![GitHub stars](https://img.shields.io/github/stars/qwqdanchun/Pillager.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)

<https://github.com/qwqdanchun/Pillager>

Pillager是一个适用于后渗透期间的信息收集工具，可以收集目标机器上敏感信息，方便下一步渗透工作的进行。

### [AppScan](detail/AppScan.md)
![Author](https://img.shields.io/badge/Author-TongchengOpenSource-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/TongchengOpenSource/AppScan.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1.5-red)

<https://github.com/TongchengOpenSource/AppScan>

安全隐私卫士（AppScan）一款免费的企业级自动化App隐私合规检测工具

### [frida-skeleton](detail/frida-skeleton.md)
![Author](https://img.shields.io/badge/Author-Margular-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/Margular/frida-skeleton.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V3.3-red)

<https://github.com/Margular/frida-skeleton>

frida-skeleton是基于frida的安卓hook框架，提供了很多frida自身不支持的功能，将hook安卓变成简单便捷，人人都会的事情。

### [java-object-searcher](detail/java-object-searcher.md)
![Author](https://img.shields.io/badge/Author-c0ny1-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/c0ny1/java-object-searcher.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.1.0-red)

<https://github.com/c0ny1/java-object-searcher>

java内存对象搜索辅助工具，配合IDEA在Java应用运行时，对内存中的对象进行搜索。比如可以可以用挖掘request对象用于回显等场景。

### [js-cookie-monitor-debugger-hook](detail/js-cookie-monitor-debugger-hook.md)
![Author](https://img.shields.io/badge/Author-JSREI-orange)
![Language](https://img.shields.io/badge/Language-JavaScript-blue)
![GitHub stars](https://img.shields.io/github/stars/JSREI/js-cookie-monitor-debugger-hook.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.11.0-red)

<https://github.com/JSREI/js-cookie-monitor-debugger-hook>

js cookie逆向利器：js cookie变动监控可视化工具 & js cookie hook打条件断点

### [MySQLMonitor](detail/MySQLMonitor.md)
![Author](https://img.shields.io/badge/Author-TheKingOfDuck-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/TheKingOfDuck/MySQLMonitor.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)

<https://github.com/TheKingOfDuck/MySQLMonitor>

MySQL实时监控工具(代码审计/黑盒/白盒审计辅助工具) 

### [CodeReviewTools](detail/CodeReviewTools.md)
![Author](https://img.shields.io/badge/Author-Ppsoft1991-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/Ppsoft1991/CodeReviewTools.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1.0-red)

<https://github.com/Ppsoft1991/CodeReviewTools>

CodeReviewTools是一个可以快速批量反编译jar包的工具，为审计Java代码做好第一步。



## 内网工具/intranet_tools
### [fscan](detail/fscan.md)
![Author](https://img.shields.io/badge/Author-shadow1ng-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/shadow1ng/fscan.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.0.0-red)

<https://github.com/shadow1ng/fscan>

一款内网综合扫描工具，方便一键自动化、全方位漏扫扫描。支持主机存活探测、端口扫描、常见服务的爆破、ms17010、redis批量写公钥、计划任务反弹shell、读取win网卡信息、web指纹识别、web漏洞扫描、netbios探测、域控识别等功能。

### [antSword](detail/antSword.md)
![Author](https://img.shields.io/badge/Author-AntSwordProject-orange)
![Language](https://img.shields.io/badge/Language-Nodejs-blue)
![GitHub stars](https://img.shields.io/github/stars/AntSwordProject/antSword.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1.15-red)

<https://github.com/AntSwordProject/antSword>

中国蚁剑是一款开源的跨平台网站管理工具。

### [Stowaway](detail/Stowaway.md)
![Author](https://img.shields.io/badge/Author-ph4ntonn-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/ph4ntonn/Stowaway.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.2-red)

<https://github.com/ph4ntonn/Stowaway>

Stowaway 是一款多级代理工具，可将外部流量通过多个节点代理至内网，突破内网访问限制。Stowaway 可以方便渗透测试人员通过多级跳跃，从外部dmz等一系列区域逐步深入核心网络；Stowaway 除了流量转发功能，还提供了端口复用、ssh隧道，流量伪装等专为渗透测试人员所用的功能。

### [shellcodeloader](detail/shellcodeloader.md)
![Author](https://img.shields.io/badge/Author-m0ngo0se@knownsec404-orange)
![Language](https://img.shields.io/badge/Language-C++-blue)
![GitHub stars](https://img.shields.io/github/stars/knownsec/shellcodeloader.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1-red)

<https://github.com/knownsec/shellcodeloader>

Windows平台的shellcode免杀加载器，自带多种加载方式：32位自带13种加载方式，64位自带12种加载方式。

### [ServerScan](detail/ServerScan.md)
![Author](https://img.shields.io/badge/Author-Adminisme-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/Adminisme/ServerScan.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.2-red)

<https://github.com/Adminisme/ServerScan>

一款使用Golang开发且适用于攻防演习内网横向信息收集的高并发网络扫描、服务探测工具。

### [Platypus](detail/Platypus.md)
![Author](https://img.shields.io/badge/Author-WangYihang-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/WangYihang/Platypus.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.0-red)

<https://github.com/WangYihang/Platypus>

Platypus 是一个基于终端与 Web UI 交互式的反弹 Shell 会话管理工具。在实际的渗透测试中，为了解决 Netcat/Socat 等工具在文件传输、多会话管理方面的不足。该工具在多会话管理的基础上增加了在渗透测试中更加有用的功能，可以更方便灵活地对反弹 Shell 会话进行管理。

### [WMIHACKER](detail/WMIHACKER.md)
![Author](https://img.shields.io/badge/Author-rootclay-orange)
![Language](https://img.shields.io/badge/Language-VBScript-blue)
![GitHub stars](https://img.shields.io/github/stars/rootclay/WMIHACKER.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)

<https://github.com/rootclay/WMIHACKER>

WMIHACKER是一款免杀横向渗透远程命令执行工具，常见的WMIEXEC、PSEXEC执行命令是创建服务或调用Win32_Process.create执行命令，这些方式都已经被杀软100%拦截，通过改造出的WMIHACKER可免杀横向移动。并且在企业网络目前阻断445端口严重的情况下可以无需445端口进行横向移动，效率高且不易被检测。

### [rakshasa](detail/rakshasa.md)
![Author](https://img.shields.io/badge/Author-Mob2003-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/Mob2003/rakshasa.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.2.3-red)

<https://github.com/Mob2003/rakshasa>

rakshasa是一个使用Go语言编写的强大多级代理工具，专为实现多级代理，内网穿透而设计。它可以在节点群里面任意两个节点之间转发TCP请求和响应，同时支持socks5代理，http代理，并且可以引入外部http、socks5代理池，自动切换请求IP。

### [As-Exploits](detail/As-Exploits.md)
![Author](https://img.shields.io/badge/Author-yzddmr6-orange)
![Language](https://img.shields.io/badge/Language-JavaScript-blue)
![GitHub stars](https://img.shields.io/github/stars/yzddmr6/As-Exploits.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.0-red)

<https://github.com/yzddmr6/As-Exploits>

中国蚁剑后渗透框架

### [PortForward](detail/PortForward.md)
![Author](https://img.shields.io/badge/Author-knownsec404-orange)
![Language](https://img.shields.io/badge/Language-Golang-blue)
![GitHub stars](https://img.shields.io/github/stars/knownsec/PortForward.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.5.0-red)

<https://github.com/knownsec/PortForward>

PortForward 是使用 Golang 进行开发的端口转发工具，解决在某些场景下内外网无法互通的问题



## 其他/others
### [f8x](detail/f8x.md)
![Author](https://img.shields.io/badge/Author-ffffffff0x-orange)
![Language](https://img.shields.io/badge/Language-Bash-blue)
![GitHub stars](https://img.shields.io/github/stars/ffffffff0x/f8x.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.6.2-red)

<https://github.com/ffffffff0x/f8x>

一款红/蓝队环境自动化部署工具,支持多种场景,渗透,开发,代理环境,服务可选项等。

### [BinAbsInspector](detail/BinAbsInspector.md)
![Author](https://img.shields.io/badge/Author-KeenSecurityLab-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/KeenSecurityLab/BinAbsInspector.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.1-red)

<https://github.com/KeenSecurityLab/BinAbsInspector>

BinAbsInspector(Binary Abstract Inspector)是一款用于自动化逆向工程和扫描二进制文件漏洞的静态分析器，是 Keenlab 孵化的长期研究项目。基于 Ghidra 的支持下的抽象解释，适用于 Ghidra 的 Pcode 而非汇编。目前支持 x86、x64、armv7 和 aarch64 的二进制文件。

### [Heimdallr](detail/Heimdallr.md)
![Author](https://img.shields.io/badge/Author-graynjo-orange)
![Language](https://img.shields.io/badge/Language-JavaScript-blue)
![GitHub stars](https://img.shields.io/github/stars/graynjo/Heimdallr.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1.3-red)

<https://github.com/graynjo/Heimdallr>

一款完全被动监听的谷歌插件，用于高危指纹识别、蜜罐特征告警和拦截、机器特征对抗。

### [passive-scan-client](detail/passive-scan-client.md)
![Author](https://img.shields.io/badge/Author-c0ny1-orange)
![Language](https://img.shields.io/badge/Language-Java-blue)
![GitHub stars](https://img.shields.io/github/stars/c0ny1/passive-scan-client.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.3.1-red)

<https://github.com/c0ny1/passive-scan-client>

Passive Scan Client是一款可以将经过筛选的流量转发到指定代理的Burp被动扫描流量转发插件

### [GrabAccess](detail/GrabAccess.md)
![Author](https://img.shields.io/badge/Author-Push3AX-orange)
![Language](https://img.shields.io/badge/Language-C-blue)
![GitHub stars](https://img.shields.io/github/stars/Push3AX/GrabAccess.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1-red)

<https://github.com/Push3AX/GrabAccess>

GrabAccess：Bookit/Windows登陆密码和Bitlocker绕过工具，在物理接触目标计算机的情况下，GrabAccess可以：绕过Windows登陆密码执行任意操作（以System权限执行命令、重置Windows账户密码等），植入木马并添加自启动（可以绕过Bitlocker，但要求受害者登录），通过修改主板UEFI固件实现无视重装系统、更换硬盘的持久化（Bootkit）

### [wam](detail/wam.md)
![Author](https://img.shields.io/badge/Author-knownsec404-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/knownsec/wam.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0-red)

<https://github.com/knownsec/wam>

WAM是一个由Python开发的用于监控'Web App'、'动态网络信息'的平台。在一定程度上，它极大地帮助安全研究人员节省了跟踪代码补丁的时间。

### [LBot](detail/LBot.md)
![Author](https://img.shields.io/badge/Author-LoRexxar@knownsec404-orange)
![Language](https://img.shields.io/badge/Language-Python-blue)
![GitHub stars](https://img.shields.io/github/stars/knownsec/LBot.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)

<https://github.com/knownsec/LBot>

LBot主要用于方便的编写一个xss的bot程序。使用者可以简单的修改其逻辑以及配置环境，即可获得一个简单的xss的bot程序。由于原型来自于爬虫程序，所以只要前端有一定的频率限制，后端很难出现问题，比较稳定。



