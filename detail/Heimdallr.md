## Heimdallr <https://github.com/graynjo/Heimdallr>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JavaScript-blue)
![Author](https://img.shields.io/badge/Author-graynjo-orange)
![GitHub stars](https://img.shields.io/github/stars/graynjo/Heimdallr.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1.3-red)
![Time](https://img.shields.io/badge/Join-20221117-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

**Heimdallr**是一款致力于被动嗅探浏览器流量，用于**提示漏洞框架指纹**、**告警拦截蜜罐请求**、**对抗浏览器特征追踪**（浏览器持久化、webRTC、Canvas画布等）的Chrome插件。

![image-20221017154419189](https://github.com/graynjo/Heimdallr/raw/main/README.assets/image-20221017154419189.png)

![image-20221017154934546](https://github.com/graynjo/Heimdallr/raw/main/README.assets/image-20221017154934546.png)

## 🥑安装

1. GitHub Releases 下载插件最新编译版本
2. Chrome浏览器-扩展设置-开发者模式-加载已解压的扩展程序

![image-20221017154934546](https://github.com/graynjo/Heimdallr/raw/main/README.assets/image-20221104111153079.png)

> 注意：Chrome版本需高于Chrome v96，部分代码逻辑不适配edge和firefox，请勿混用于非Chrome浏览器

## 🚀使用

### 基本功能

高危漏洞资产指纹识别和蜜罐jsonp请求识别功能无需配置，只要插件开启即可生效。

- 高危漏洞资产指纹识别规则103条，涉及框架或产品如下：

> ueditor、struts2、spring、weblogic、shiro、F5 BIG-IP、致远OA、用友NC、用友畅捷通、通达OA、心通达OA、新点OA、帆软报表、蓝凌OA、红帆OA、华天动力OA、万户OA、金蝶云、协众OA、金和OA、海昌OA、泛微多个产品(ecology、eoffice、ebridge、emobile)、拓尔思SSO、拓尔思内容管理系统、亿邮邮件、coremail邮件、Exchange邮件、若依后台管理系统、Wordpress、小鱼易连云视讯、tomcat、iis、jboss、jetty、ibm websphere、weblogic、thinkphp、showdoc、Laravel、kindeditor、fckeditor、ewebeditor、jeesite、海康威视多个产品（网络摄像头、安防管理平台、图像综合应用平台）、dedecms、jira、confluence、java web、博达站群、dubbo、向日葵客户端、宝塔waf、宝塔面板、米拓cms、teleport堡垒机、齐治堡垒机、帕拉迪堡垒机、H3C堡垒机、绿盟防火墙、安全狗Waf

- 蜜罐特征告警规则151条，涉及敏感域名请求(jsonp)、蜜罐网页资源特征、蜜罐对本机特殊软件（如Burpsuite）的探测请求、网站流量分析与跟踪请求、敏感关键词、敏感脚本调用等。

> 为了保证请求的最全面捕获，Heimdallr中不进行请求种类（如script、XMLHttpRequest等）的筛选，因此插件默认只进行蜜罐请求识别而不作拦截，若开启蜜罐请求拦截会影响正常访问CSDN、Github等网站的正常访问，可以通过日常使用时暂停插件（控制-暂停/开启插件）或关闭蜜罐拦截功能（策略配置-蜜罐拦截配置）解决。
>
> 因部分框架或产品（如百度网站在线客服会调用5个敏感域名、高德地图嵌入会调用高德域名）的正常使用也会出现Jsonp敏感域名的访问，故同一站点的Jsonp请求超过10个时，基本可以确定为蜜罐站点，此时将会出现系统弹窗告警（弹窗需要操作系统开启浏览器弹窗权限，该权限默认开启）。低于10个的敏感域名请求，使用者可根据当前站点内容和告警域名的关联度进行判断，例如某个小企业官网可能调用百度商桥接口实现在线客服功能，但一般不会调用虎牙直播账号接口或联通一键登录热点溯源接口。

### 控制

右上角三个选项分别为暂停/开启插件、清除所有嗅探结果集、设置选项。

> 暂停插件后，会清空所有页面的嗅探结果集，关闭对请求和响应的监听，扩展功能中仅WebRTC防护功能不关闭，其他的功能都会随插件暂停而暂停。

### 扩展功能

扩展功能由策略配置页面配置

![image-20221017093032294](https://github.com/graynjo/Heimdallr/raw/main/README.assets/image-20221017093032294.png)

#### 被动识别配置-启用响应体规则匹配

- 建议设置：仅在攻击期间对需高度关注页面（口子、靶标）开启该选项，用完即关

> 默认情况下，被动嗅探只对请求响应的URL、Request Header、Request Body、Response Header进行匹配，仅有较少部分高危指纹在Response Body中检测，开启该选项后会启用devtools调用chrome devtools protocol，检测Response Body中的指纹。但是启用该选项后会出现调试提示栏，如需关闭参考高级-4

#### 被动识别配置-关闭浏览器页面缓存（强制刷新）

- 建议设置：默认开启该选项

> 部分包含特征规则的静态资源（如JS文件）会在一次调用后存储在磁盘中，减少重复加载耗费的流量和带宽。这会导致识别规则在重复刷新页面是不会重复触发。开启该选项后可以达到更完善的特征识别，这也可以防止部分情况下静态资源文件不能及时更新导致的访问异常

#### 蜜罐拦截配置-符合蜜罐特征请求自动拦截

- 建议设置：攻击期间开启，日常使用时关闭

> 为保证能够识别、阻断部分新的Jsonp请求，插件按照请求域名进行拦截，这会导致开启该选项后访问部分日常网站（CSDN、GitHub等）会被阻断，影响日常访问。因此默认情况下插件不会拦截疑似蜜罐的Jsonp请求，需要手动开启拦截选项.日常网站被拦截也可以通过右上角的暂停插件按钮暂停，访问结束后重新启动插件。但是更建议的方式为日常使用浏览器和攻击使用浏览器分离开来，专事专用

#### 特征对抗配置-清除所有浏览器持久化项数据

- 建议设置：在被cookie追踪或其他持久化手段追踪浏览器特征时清除数据

> 清除的浏览器持久化项包括：网站应用缓存（appcache）、网站资源缓存、网站缓存存储、Cookie、网络文件系统、表单数据记录、索引数据库（indexDB）、localStorage、密码记录、网络SQL数据（webSQL）
> 
> **警告**：清除的数据中包含密码记录，即浏览器的密码管理器的记录。如果你使用浏览器自带的密码管理器和Google账号进行密码记录和维护，清除浏览器的密码管理器记录可能导致Google账号同步的密码被置空。再次建议将攻击主机和日常使用的主机分离，不在攻击主机上登录或保存任何私人有关的账号。

#### 特征对抗配置-WebRTC 防IP泄露严格策略

- 建议设置：安装后手动开启该选项

> 通过提高WebRTC策略严格度防止真实IP泄露，已知Chrome v104（截至2022.9.1）仍存在该漏洞，此选项可在并建议在日常使用时也开启
> 请勿将此策略与其他WebRTC防护插件（如WebRTC Control或WebRTC Leak Prevent）同时使用，各插件调节WebRTC策略会互相干涉，暂停其他插件的使用时的API调用也会影响Heimdallr的调节逻辑。

#### 特征对抗配置-Canves噪点干扰脚本注入

- 建议设置：攻击期间开启，日常使用时关闭

> 通过对当前网页注入内容脚本增加Canvas画布噪点防止特征锁定，开启后所有网页访问时将会额外加载content.js用于画布类的函数hook操作



## 🔔高级

1. 插件的识别对象基于【标签页】，标签页页面变更【(域名+端口)或(IP+端口)】时清空结果，切换标签页时结果会暂存，关闭标签页或窗口时删除对应结果。
2. 插件默认只存在被动流量监控，不会因为敏感指纹的识别触发防火墙处置。
3. 插件识别结果为页面及页面子框架的请求内容，部分页面告警【请求体数据为json格式】、【请求头Content-Type为application/json格式】时，不一定是当前document的请求，有可能是当前document页加载的相关页面的接口请求匹配了规则.
4. 因为谷歌Chrome API的安全限制和Chrome内核的历史遗留问题，插件对响应体Body的检查与其他指纹位置的检查不同，浏览器页面顶部会出现调试提示，可通过插件设置关闭响应包检查功能或添加谷歌浏览器的启动项规避提示（在Chrome快捷方式右键打开属性，在快捷方式栏的【目标】框添加启动参数 `--silent-debugger-extension-api`）。
5. 插件目的为发现直接访问无法识别的组件或框架，请勿添加可以直接识别的组件的特征到指纹库（如spark未授权页面），增加无意义的识别流程导致识别负担增加。


## 🎇继续开发

#### 新增指纹

在实战中遇到有意义的高危指纹特征或未在拦截列表中的蜜罐请求特征都可以打开新的issue提交，作者会尽快在验证可用性后将指纹添加到新的版本中。

#### 二次开发

Vue3前端模块

```
cd Vue_popup\heimdallr_v3
npm install
npm run build:watch
vim src\App.vue
```

chrome插件模块

```
cd .\Heimdallr\
```

指纹模块

```
cd .\Heimdallr\resource\data
vim data.js
```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
