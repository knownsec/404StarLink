## OpenStar <https://github.com/starjun/openstar>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![Author](https://img.shields.io/badge/Author-starjun-orange)
![GitHub stars](https://img.shields.io/github/stars/starjun/openstar.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)
![Time](https://img.shields.io/badge/Join-20210702-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


欢迎使用 **{OpenStar}(WAF+)**，该项目是从实际需求中产生，经过多次的版本迭代，实属不易。感谢**春哥**，以及[春哥][1]的神器（**[OpenResty][2]**）
注意：使用版本一定要大于 1.11.0 因为使用了ngx.var.request_id
**代码写的比较好理解，肯定不优雅  哈~**

个人的一些开发实践，有需要的朋友可以加入下
![xq][27]

正在更新说明WIKI篇,已经更新了安装篇，请自行查阅。

更新：规则支持方式
```
支持并行正则匹配(使用 https://github.com/cloudflare/lua-aho-corasick 实现)
增加：并行正则("aho") -- 列表
"host":[[
          "^www.baidu",
          ".*.baidu.com$"
        ],
            "aho"
        ]
```

更新：规则支持方式
```
现有：等于("") 包含("in") 列表("list") 字典("dict") 正则("jio|jo|***")
增加：开头列表("start_list") -- 以什么什么开头列表
      不区分大小写 开头列表("ustart_list")
      结尾列表("end_list")  -- 以什么什么结尾列表
      不区分大小写 结尾列表("uend_list")
      包含列表("in_list")   -- 包含的列表形式
      不区分大小写包含列表("uin_list")  --in_list扩展(不区分大小写)
      【json 同 list 一样】
增加：长度("len") [Min,Max] 表示大于等于 Min,且小于等于 Max
EG：
"host":[[
          "www.baidu.",
          "img.baidu."
        ],
            "start_list"
        ]
"referer":[[0,150],"len"]   --- referer 长度 在 0~150 之间
```

# 非开源版本 【带后台、带 4 层防护模块等...】完全免费！！！
https://www.kancloud.cn/openstar/install/1136671


# 变更历史

## 1.7 更新二阶匹配规则支持取反，动作取消next等
原二阶规则：["baidu","in"],支持取反后：["baidu","in",true];最后的默认是nil也就是false,不取反的意思，所以规则基本可以之间复用，动作为next的需要修改一下即可

## 1.7.1.11 更新规则匹配等于判断表达式支持("="),post_form支持("*")对所有表单名称进行匹配
```
["post_form",["(;|-|/)","jio",["*",2],false]] 对表单所有名称的文件名进行匹配

["www.test.com",""]
["www.test.com","="] 新增加表达方式

```


## 1.7.1.10 更新支持基于业务属性进行限速的功能
network_Mod: `"network":{"maxReqs":30,"pTime":10,"blackTime":600,"guid":"cookie_userguid"}`，业务代码ngx.var[%guid%]，实际上是从ngx.var中去值进行限速操作，所以一定要配置正常；这里表示从cookie中名称为userguid的值进行频率统计来限速。默认则是用ip限速

### 1.7.1.1 修改 host_Mod 规则匹配
目前只有两种规则（app_ext | network） 请参考 conf_json/host_json/101.200.122.200.json

### 1.7.0.24 原规则匹配变更：table-->list;list-->dict
方便理解list表示序列，dict表示字典。
EG：
```
"method":[
            {
                "POST":true,
                "GET":true
            },
            "dict" --- 原 list
        ]
"ips": [[
            "101.254.241.149",
            "106.37.236.170"],
            "list" --- 原 table
        ]
```

## 1.6 更新计数count_dict到DB 2,key也进行分开，优化规则缓存
规则进行了缓存，大幅提高性能，json文件保存进行了美化等......

## 1.5 应一些朋友强烈要求增加Master/Slave模式
主：定时将内存中的配置推送到redis, 从：定时从redis拉取数据到内存后，并保存到文件

## 1.4 更新命名相关，以多规则匹配
原来url改成uri，args改成query_string，修改的比较多，还有增加app_Mod实现多规则匹配，连接符支持OR

## 1.3 更新跳转功能，可配置进行set-cookie操作
可以配置某一个或者多个url使用跳转set-cookie操作。cookie是无状态的。

## 1.2 更新支持拦截外部的csrf
在referer_Mod处，增加action，`allow`表示允许且后续的规则不用在匹配（一般是静态资源如图片/js/css等），`next`表示白名单匹配成功后，会继续后面的规则匹配（这里就用于拦截外部的CSRF）增加`next`是因为原来代码中，若配置了防护站外的CSRF，后续的规则会bypass,所以增加的，这样就不会出现一些绕过问题。
**后续的action理论上都支持该语法**

## 1.1 增加app_Mod,丰富allow动作（ip）
网站的某个目录进行IP白名单的访问控制（后台、phpmyadmin等）

## 0.9 - 1.0 修改了大量全局函数
在学习完[OpenResty最佳实践][7]后，代码太不专业，修改了大量全局变量、函数

## 0.8 优化一下算法
原来args是遍历每个参数在连接起来，感觉性能有时有点瓶颈，就使用新api取出url中的所有参数，经过测试效果要比原来好很多。

## 0.7 增加集群版本
当时大约有2-4台OpenStar服务器用于安全防护，通过脚本进行统一管理的，没有进行真正的统一管理，所以抽空的时候把redis用上。

## 0.6 增加API相关操作
因为是个蹩脚的程序员（没办法，搞安全的现在都被逼的写代码了；感谢春哥，我在写的过程中非常的快乐，所以就把项目叫做OpenStar[开心]，请勿见笑了）、前端界面我迟迟没有想好，所以先把一下操作的API封装了，也满足当时公司脚本化需求。

## 0.4-0.5 增加配置文件操作
刚开始都是写在lua代码中，随着功能增加，决定通过配置文件进行操作，所有就使用json方式进行定义配置文件。

## 0.3 增加waf防护模块
随着cc防护成功后，我陆续增加了waf相关的功能，规则参考了[modsecurity][8]、[loveshell][9]防护模块、以及互联网搜集的一些过滤点

## 0.2 CC防护应用层版
通过网络层+应用层的防护后，我后续增加了应用层的安全防护，如应用层set cookie、url跳转、js跳转等这样应用层的防护模块

## 0.1 CC防护版
当时是为了解决公司的CC攻击，由于一些硬件抗D设备在新的网络环境下（有CDN网络下）无法获取用户真实IP头，我才动手将第一个版本完成，当时功能就是有通过自定义HTTP头获取用户真实ip进行访问频率的限制。（OpenStar可以根据某个url进行频率限制，不仅仅是整个网站的[排除静态文件，如设置了referer\_Mod 或者 url\_Mod 中资源的allow操作]）

# TOP

[安装篇][3]

[基础配置说明][4] base.json

[STEP 0：realIpFrom_Mod][10]

[STEP 1：ip_Mod][11]

[STEP 2：host_method_Mod][12]

[STEP 3：rewrite_Mod][13]

[STEP 4：host_Mod][14]

[STEP 5：app_Mod][15]

[STEP 6：referer_Mod][16]

[STEP 7：uri_Mod][17]

[STEP 8：header_Mod][18]

[STEP 9：useragent_Mod][19]

[STEP 10：cookie_Mod][20]

[STEP 11：args_Mod][21]

[STEP 12：post_Mod][22]

[STEP 13：network_Mod][23]

[STEP 14：replace_Mod][24]


一些同学问的比较多的问题：

0：规则组问题
支持IFTTT模式，如条件是（referer中包含baidu 或者 cookie中不包含abc 且useragent正则匹配spider）等等这样复杂的表达式，执行动作也是有多个可以使用(deny allow log refile rehtml relua*)可以定制各种复杂的场景


1：关于多站点的事

使用ngx本身的增加配置文件就不说了，使用动态upstream可以参考我另外的项目https://github.com/starjun/dynamic_upstream-by-balancer
一些接口没有加上去，看看代码自己非常容易搞定了。反向代理的host和后端的IP组都在DICT中（注意是IP组，而不仅仅是类似一些balancer写动态upstream的是一个IP），且支持多种负载均衡方式，相信可以满足大多数需求。https的后面有时间我在完善下。

2：集群相关(提供了Master/Slave配置)

目前openstar是支持集群的，规则同步和下发等都是提供了api，都是被动方式，规则为什么没有放到redis中，请自己测试一下，每次规则过滤都从redis取后在序列化，和从dict取在序列化，自己动手测试看性能，顺便说下，规则在集群下当然存在redis中，都是通过api进行操作更新到dict中，而不是每次都从redis中取，且最近增加了定时从redis拉取配置功能（测试中...）

3：如有一些技术类问题，请尽量完整一些，包括ngx配置文件，和比较完整的代码，不然真心不好作答，有时间我会尽量回复（不一定是对的），没时间回复的请谅解。

admin@17173.com邮箱已经没有在用了，请不要给这个发邮箱啦。

## TODO ##

  无

  商业版说明：

  **支持域名管理，支持geoip（按国家，城市进行拦截等），支持SQL语义分析(功能完善中)，更强大的api接口，默认规则更强大等等**

----------

CC防护、防抓取、刷单等防护算法：

CC攻击点：

a：用户可直接访问的url(搜索请求[数据库查询]，高计算[cpu计算]，随机url[耗连接]等)

b：嵌入类型的url(嵌入的验证码url[CPU计算]、ajax判断用户是否存在的url[数据库查询]等)

c：非浏览器类型的接口(一些公共API、WEBservice等无SDK的接口)

d：特定语言、服务器的攻击(php dos、慢速攻击等)

我提供的防护算法是用于防护a、b类型的攻击，a类型防护启用时，可以先生成一个添加标记的跳转页面，b类型防护启用时，动态对其渲染页面进行标记的添加，c类型有sdk，自己写代码支持自己设定的防护算法的不是问题。

js静态、动态验证：

跳转页面/渲染页面对下一次请求的url进行标记增加（openstar已经实现的增加url尾巴），增加一个get的args参数，参数名称和值都是由服务器产生或者前端页面js产生，如对下一次请求的url增加`cc=1ldldj`这个尾巴，服务端判断合法性有静态的正则判断值的合法性，有动态的判断值是否由服务器生成的,合法性检查更加严格。

js增强：（获取鼠标轨迹、鼠标点击事件、随机延迟、基于特定浏览器对js的方言）

普通的js一些攻击软件或者爬虫工具是可以分析执行的，故可以进行js增加，如判断鼠标轨迹、鼠标点击事件这些事件判断失败就不会进行下一步请求；如基于浏览器的js方言，一些浏览器会有自己的方言，那些爬虫工具和攻击工具是不可能解析js方言的，就不会进行下一步请求；还有使用js随机延迟函数，用于下一次请求的时间分流，这样请求频率就会被分开，这样就缓解了请求频率，以及结合鼠标轨迹和鼠标事件判断，可以很好的识别工具和人。

浏览器指纹：（对浏览器会生成一个唯一指纹，从而判断链式请求指纹的一致性）
广告厂商来做这件事就事半功倍了，毕竟浏览器指纹在整个互联网的数据还是很有参考价值的，毕竟不是要指纹对应的广告标签等这些商业价值数据，仅是需要一个指纹的信誉库（同IP信誉库类似，当然也有时效性），因为CC攻击和一些爬虫、刷单工具在互联网上的指纹还是非常清晰的。
情况可以公司可以建立自己的体系，对CC攻击、页面抓取、刷单是有相当大的帮助的，以后各大公司可以共享这些浏览器指纹数据，组成一个联盟也行，从而判断该指纹是否是真实用户等一些可用数据。

http://123.57.220.116/fgjs2.html 看看自己的浏览器指纹吧(如果访问不了，哈，我买的ECS过期了！)

参考：https://github.com/Valve/fingerprintjs2


控件/浏览器防护:

使用js进行下一次请求的跳转，以及增强的鼠标轨迹、鼠标事件、浏览器js方言等这些判断还是有一定的缺陷，故可以直接使用控件方式、或者和浏览器合作（浏览器支持这种防护标记）


```
PS：简单举个例子
http://www.cc.com?cc=@{"api":"http://1.1.1.1/cc/api","key":"iodjdjkdldskl"}@
http://www.cc.com?cc=@{"api":"tcp://1.1.1.1:908","key":"iodjdjkdldskl"}@
http://www.cc.com?cc=@{"api":"local","key":"1:2345:44"}@
跳转页面或者渲染页面，控件/浏览器是可以识别@中间的内容的，向这个api使用key取到一个值，下一次请求带上这个值。

```

i：set 一个cookie,其合法性是由控件和web服务器双向约定或加密产生，从而判断下一次请求是否合法

ii：增加args参数尾巴，其value值合法性由控件和web服务器双向约定或加密产生，从而判断下一次请求是否合法

iii：增加POST参数，其value值合法性由控件和web服务器双向约定或加密产生，等等对下一次请求进行验证增加

## 重点 ##

这些防护算法我正在申请相关专利，个人用户以后永久免费的，仅对企业收费，请抄袭党，无耻公司放过小弟一码。

这些防护算法我正在申请相关专利，个人用户以后永久免费的，仅对企业收费，请抄袭党，无耻公司放过小弟一码。

这些防护算法我正在申请相关专利，个人用户以后永久免费的，仅对企业收费，请抄袭党，无耻公司放过小弟一码。


# 概览


----------


**OpenStar**是一个基于[OpenResty][2]的，高性能WAF，还相应增加了其他灵活、友好、实用的功能，是增强的WAF。
**app_Mod 支持规则组 连接符支持 or , 参考doc/demo.md文档**
# WAF防护


----------


在**OpenStar**中的WAF防护模块，采用传统的字符串的匹配如正则过滤、包含等（*有人会问现在不是流行自主学习么；正则、包含等会有盲点、会被绕过；WAF的误报和漏报问题等等......*）。**规则不是万能的，但是没有规则是万万不能的** 这里我简单说明一下，自主分析学习引擎是我们的日志分析引擎做的（预留了api可实时增加拦截），这里是高性能、高并发的点，就用简单快速的方法解决，且根据业务实际调整好防护策略，可以解决绝大多数WEB安全1.0和WEB安全2.0类型的漏洞（90%+的问题）。
WAF 防护从header,args,post,访问频率等，分层进行按顺序防护，详细在后面的功能会详细说明

 - **WEB安全1.0**
   在1.0时代下，攻击是通过服务器漏洞（IIS6溢出等）、WEB应用漏洞（SQL注入、文件上传、命令执行、文件包含等）属于服务器类的攻击，该类型漏洞虽然经历了这么多年，很遗憾，此类漏洞还是存在，并且重复在犯相同的错误。

 - **WEB安全2.0**
   随着社交网络的兴起，原来不被重视的XSS、CSRF等漏洞逐渐进入人们的视野，那么在2.0时代，漏洞利用的思想将更重要，发挥你的想象，可以有太多可能。

 - **WEB安全3.0**
   同开发设计模式类似（界面、业务逻辑、数据），3.0将关注应用本身的业务逻辑和数据安全，如密码修改绕过、二级密码绕过、支付类漏洞、刷钱等类型的漏洞，故注重的是产品本身的业务安全、数据安全、风控安全等。

   > `安全不仅仅是在技术层面、还应该在行政管理层面、物理层面去做好安全的防护，才能提供最大限度的保护。`
   > 安全行业多年的从业经验：人，才是最大的威胁；无论是外部、内部、无心、有意过失。（没有丑女人、只有懒女人）我想可以套用在此处，纯属个人见解。

# CC/采集防护
什么是**CC攻击**，简单的说一下，就是用较少的代价恶意请求web（应用）中的重资源消耗点（CPU/IO/数据库等等）从而达到拒绝服务的目的；**数据采集**，就是内容抓取了，简单这么理解吧
> `非官方学术类的解释，先将就理解下`
**关于本文对CC攻击的分析和相关的防护算法，都是我在实战中分析总结，并形成自己的方法论，不足之处、欢迎指正。**

## 攻击类型
 - 行为（GET、POST等）
  目前主要还是这两中method攻击为主，其他的少之又少。
 - 被攻击的点

    1：用户可直接访问的URL（搜索、重CPU计算、IO、数据库操作等）

    2：嵌入的URL（验证码、ajax接口等）

    3：面向非浏览器的接口（一些API、WEBservice等）

    4：基于特定web服务、语言等的特定攻击（慢速攻击、PHP-dos等）

> `面对CC攻击我们需要根据实际情况采用不同的防护算法，比如攻击的点是一个ajax点，你使用js跳转/验证码肯定就有问题`

## 防护方法
 - 网络层
 通过访问ip的频率、统计等使用阀值的方式进行频率和次数的限制，黑名单方式

- 网络层+应用层
 在后来的互联网网络下，有了的CDN加入，现在增加的网络层的防护需要扩展，那么统计的IP将是在HTTP头中的IP，仍然使用频率、次数、黑名单的方式操作。
 > `但是很多厂家的硬件流量清洗等设备，有的获取用户真实IP从HTTP头中取的是固定字段（X-FOR-F），不能自定义，更甚至有的厂家就没有该功能，这里就不说具体的这些厂家名字了`PS: 在传统的4层防护上，是没有问题的

-  应用层
TAG验证、SET COOKIE、URL跳转、JS跳转、验证码、页面嵌套、强制静态缓存等
防护是需要根据攻击点进行分别防护的，如攻击的是嵌入的url，我们就不能使用JS跳转、302验证码等这样的方法；**在多次的CC防护实战中，如使用url跳转、set cookie，在新型的CC攻击下，这些防护都已经失效了**。后面我会分享一下我的防护算法，并且在**OpenStar**中已经可以根据情况实现我所说的防护算法。
浏览器是可以执行JS和flash的，这里我分享一些基于JS的防护算法，flash需要自己去写（比js复杂一些），可以实现flash应用层的安全防护和防页面抓取（开动你的大脑吧）

1：客户端防护
使用JS进行前端的防护（浏览器识别、鼠标轨迹判断、url有规则添加尾巴（args参数）、随机延迟、鼠标键盘事件获取等）其实这里非常复杂，如浏览器的识别 ie 支持 `!-[1,]` 这个特殊JS，一些JS方言，一些浏览器有自定义标签等等；

2：服务端防护
url添加的尾巴（args参数）是服务器动态生成的token，而不是使用静态的正则去匹配其合法性。

3：特定攻击
该类特定攻击，可以通过特征快速匹配出来（慢速攻击、PHP5.3的http头攻击）

**简单场景**

1：用户可直接访问的url（这种是最好防的）

第一阶段：

 - 网络层：访问频率限制，超出阀值仅黑名单一段时间

 - 应用层：js跳转、验证码、flash策略（拖动识别等）

2：嵌入的url（ajax校验点、图片验证码）

第一阶段：

 - 网络层：访问频率限制，超出阀值仅黑名单一段时间

 - 应用层：载入被攻击的url页面，重写页面，使用js方操作链接被攻击的url。js随机在url尾巴增加有一定规则的校验串，服务端对串进行静态正则校验。

第二阶段：

 - 网络层+应用层：用户ip在http头中，需要从http头取ip，在进行频率限制
（其实做好了，这一层的防护，基本不用进入第三阶段的应用层防护了）

 - 应用层：校验串使用服务端生成的token，进行严格服务器token验证检查

第三阶段：

 - 应用层：js增加浏览器识别（不同agent匹配不同JS方言代码）、JS随机延迟、鼠标轨迹验证、键盘鼠标事件验证等js增加验证后，在进行校验串生成。

说明：多次实战CC处理经验，很少到第三阶段，当然储备好这些JS脚本非常重要，纯JS肯定也是有限的，所有我就提出了使用控件，甚至是和浏览器厂商合作等更精准的防护方法。这样对CC攻击、页面抓取、刷单等有非常好的防护效果。

> 应用层的防护是在网络层+扩展的网络层防护效果不佳时使用，一般情况基本用的不多，因为在OpenStar的防护下，极少数情况下，需要第三阶段防护。在防页面抓取时，发挥你的想象（js是个好帮手，善用）使用OpenStar就可以帮你快速实现；当然使用flash防抓取效果更好（不够灵活）。

# 目录

后续更新！~

# 下载

wget

git clone

**已经打包的一些脚本，请参考bash目录**

# 安装
 - 安装OpenResty
 这里不做过多重复描述，直接看链接[OpenResty][2]
 - 配置nginx.conf
 在http节点，引用waf.conf。注：原ngx相关配置基本不用修改，该优化优化、该做CPU亲缘绑定继续、该动静分离还继续、该IO、TIME等优化继续不要停。
 - 配置waf.conf
 修改lua\_package\_path，使用正确的路径即可；修改那些lua文件的路径，多检查几遍。
 - 设置目录权限
 OpenStar目录建议放到OR下，方便操作，该目录ngx运行用户有读写执行权限即可。因为要写日志，*暂时没有用ngx.log，后续可能会改动*。
 - lua文件修改
 在init.lua中，修改conf_json参数，base.json文件绝对路径根据自己的情况写正确。
 - api使用
2016年6月7日 23:31:09 更新啦，引用waf.conf，后就可以直接使用api接口了，通过监听5460端口来给管理用啦，界面也在筹划中，期待有人可以加入，帮我一起整界面。

**已经打包的一些脚本，请参考bash目录，运行前请阅读一下，感谢好友余总帮助写的脚本**

# 使用

## 配置规则

一般情况下匹配某一规则由3个参数组成，第二个参数标识第一个参数类型,第三个参数表示是否取反，默认为`nil` 即 `false` 表示不取反

hostname：`["*",""]` = `["*","",false]`

==>表示匹配所有域名（使用字符串匹配，非正则，非常快）

hostname：`["*\\.game\\.com","jio"]`

==>表示使用正则匹配host（**ngx.re.find($host,参数1，参数2)**）

hostname：`[["127.0.0.1","127.0.0.1:8080"],"list"]`

==>表示匹配参数1 列表 中所有host

hostname：`[{"127.0.0.1":true,"127.0.0.1:5460":true},"dict"]`

==>表示匹配 字典 中host为true的host

uri：`["/admin","in"]`

==>表示匹配uri中包含/admin的所有uri都会被匹配（**string.find($uri,参数1,1,true)**）

ip：`[["127.0.0.1/32",""113.45.199.0/24""],"cidr"]`

==>表示匹配的ip在这两组ip段/ip中

args：`["*","",["args_name","all"],false]`
args：`["*","",["args_name","end"]]` = `["*","",["args_name","end"],false]`
args：`["*","",["args_name",1]]`

说明：第3个参数表示取args参数table的key名称，第3个参数[2]表示取args[args_name]为table时，匹配任意(all)，匹配最后一个(end),匹配第几个(数字)，默认取第一个

==>表示匹配的GET的args参数名为args_name,使用第4个参数模式进行匹配，匹配规则就是第一个和二个参数。其中第1、2参数支持前面描述的规则方式。

**table类型的匹配规则比较麻烦，暂时想着是这样处理，有好的想法可以告诉我**

## 执行流程

![enter description here][5]

 - init阶段

 a：首先加载本地的base.json配置文件，将相关配置读取到config\_dict,host\_dict,ip\_dict中

 - access阶段（自上到下的执行流程，规则列表也是自上到下按循序执行的）

 0：realIpFrom_Mod ==> 获取用户真实IP（从HTTP头获取，如设置）

 1：ip_Mod ==> 请求ip的黑/白名单、log记录

 2：host\_method\_Mod ==> host和method过滤（白名单）

 3：rewrite_Mod ==> 跳转模块，set-cookie操作

 4：host_Mod ==> 对应host执行的规则过滤（uri,referer,useragent等）

    这里是产品中提供给独立用户使用的过滤规则。目前支持自定义规则组（任意参数，任意组合）

 5：app_Mod ==> 用户自定义应用层过滤

 6：referer_Mod ==> referer过滤（黑/白名单、log记录）

 7：uri_Mod ==> uri过滤（黑/白名单、log记录）

 8：header_Mod ==> header过滤（黑名单）

 9：useragent_Mod ==> useragent过滤（黑/白名单、log记录）

 10：cookie_Mod ==> cookie过滤（黑/白名单、log记录）

 11：args\_Mod ==> args参数过滤[实际是query_string]（黑/白名单、log记录）

 12：post_Mod ==> post参数过滤[实际是整个post内容]（黑/白名单、log记录）

 13：network_Mod ==> 应用层网络频率限制（频率黑名单）

 - body阶段

 14：replace\_Mod ==> 内容替换规则（动态进行内容替换，性能消耗较高慎用，可以的话用app\_Mod中rehtml、refile这2个自定义action）

## <span id = "step0">STEP 0 : realIpFrom_Mod </span>

 - 说明：
`{"101.200.122.200:5460": {"ips": ["*",""],"realipset": "x-for-f"}}`

 通过上面的例子，表示域名id.game.com,从ips来的直连ip，用户真实ip在x-for-f中，ips是支持二阶匹配，可以参考例子进行设置，ips为\*时，表示不区分直连ip了。

## STEP 1：ip_Mod（黑/白名单、log记录）

 - 说明：
 `{"ip":"111.206.199.61","action":"allow"}`
`{"ip":"www.game.com-111.206.199.1","action":"deny"}`

 上面的例子，表示ip为111.206.199.61（从http头获取，如设置）白名单
 action可以取值[allow、deny]，deny表示黑名单；第二个就表示对应host的ip黑/白名单，其他host不受影响。

 [返回](#top)

## <span id = "step2">STEP 2：host\_method\_Mod（白名单）</span>

 - 说明：
 `{"state":"on","method":[["GET","POST"],"list"],"hostname":[["id.game.com","127.0.0.1"],"list"]}`

  上面的例子表示，规则开启，host为id\.game\.com、127.0.0.1允许的method是GET和POST
  state：表示规则是否开启
  method：表示允许的method，参数2标识参数1是字符串、列表(list)、正则、字典(dict)
  hostname：表示匹配的host，规则同上

  > **`"method": [["GET","POST"],"list"]`==> 表示匹配的method是GET和POST**

  > **`"method": ["^(get|post)$","jio"]` ==> 表示匹配method是正则匹配**

  > **`"hostname": ["*",""]` ==>表示匹配任意host（字符串匹配，非正则，非常快）**

  > **后面的很多规则都是使用该方式匹配的**

[返回](#top)


## STEP 3: rewrite_Mod（跳转模块）
- 说明：
```
    {
        "state": "on",
        "action": ["set-cookie"],
    "set_cookie":["asjldisdafpopliu8909jk34jk","token_name"],
        "hostname": ["101.200.122.200",""],
        "uri": ["^/rewrite$","jio"]
    }
```
上面的例子表示规则启用，host为101.200.122.200,且url匹配成功的进行302/307跳转，同时设置一个无状态cookie，名称是token。action中第二个参数是用户ip+和改参数进行md5计算的。请自行使用一个无意义字符串。防止攻击者猜测出生成算法。

 [返回](#top)

## STEP 4：host_Mod
 - 说明：
 该模块是匹配对应host进行规则匹配，在conf_json/host_json/目录下，本地的基于host的匹配规则
 支持host.state状态支持[on log off],log即表示原匹配被拦截将失效，off表示不做任何规则的过滤

## <span id = "step5">STEP 5：app_Mod（自定义action）</span>
 - 说明：
 ```
{
    "state":"on",
    "action":["deny"],
    "hostname":["127.0.0.1",""],
    "uri":["^/([\w]{4}\.html|deny1\.do|你好\.html)$","jio"]
}
 ```

  上面的例子表示规则启用，host为127.0.0.1，且url符合正则匹配的，拒绝访问

  state：规则是否启用
  action：执行动作

  1：deny ==> 拒绝访问

  2：allow ==> 允许访问

  3：log ==> 仅记录日志

  4：rehtml ==> 表示返回自定义字符串

  5：refile ==> 表示返回自定义文件（文件内容返回）

  6：relua ==> 表示返回lua执行脚本（使用dofile操作）

  7：relua_str ==> 表示返回lua代码执行

  hostname：匹配的host

  uri：匹配的uri

  > **hostname 和 uri 使用上面描述过的匹配规则，参数2标记、参数1内容**

  > **详细参见项目中的demo规则，多实验、多测试就知道效果了**

  > **各种高级功能基本就靠这个模块来实现了，需要你发挥想象**

 [返回](#top)

## STEP 6：referer_Mod（白名单）

 - 说明：
 `{"state":"on","uri":["\\.(gif|jpg|png|jpeg|bmp|ico)$","jio"],"hostname":["127.0.0.1",""],"referer":["*",""],"action":"allow"}`

  上面的例子表示，host为127.0.0.1，uri配置的正则成功，referer正则匹配成功就放行**【这里把一些图片等静态资源可以放到这里，因为使用OpenStar，不需要将access_by_lua_file 专门放到nginx的不同的location动态节点去，这样后续的匹配规则就不对这些静态资源进行匹配了，减少总体的匹配次数，提高效率】**，action表示执行的动作，`allow`表示规则匹配成功后，跳出后续所有规则（一般对静态资源图片），referer匹配失败就拒绝访问（白名单），防盗链为主；规则的取反可以设置防护站外的CSRF

  state：表示规则是否开启
  uri：表示匹配的uri
  hostname：匹配host
  referer：匹配referer
  action：匹配动作

  > referer的匹配是白名单，注意一下即可
  > 这些匹配都是基于上面说过的二阶匹配法

 [返回](#top)

## STEP 7：uri_Mod（黑、白名单）

 - 说明：
 `{"state":"on","hostname":["\*",""],"uri":["\\.(css|js|flv|swf|zip|txt)$","jio"],"action":"allow"}`

  上面的例子表示，规则启用，任意host，uri正则匹配成功后放行，不进行后续规则匹配（该场景同图片等静态资源一样进行放行，减少后续的匹配）
  state：表示规则是否开启
  hostname：表示匹配的host
  uri：表示匹配uri
  action：可取值[allow、deny、log]，表示匹配成功后的执行动作

  > 一般情况下，过滤完静态资源后，剩下的都是拒绝一下uri的访问如.svn等一些敏感目录或文件

 [返回](#top)

## STEP 8：header_Mod（黑名单）

 - 说明：
 `{"state":"on","uri":["\*",""],"hostname":["\*",""],"header":["Acunetix_Aspect","\*",""]}`

 上面的例子表示，规则启用，匹配任意host，任意uri，header中Acunetix_Aspect内容的匹配（本次匹配任意内容）这个匹配是一些扫描器过滤，该规则是wvs扫描器的特征
 state：规则是否启用
 uri：匹配uri
 hostname：匹配host
 header：匹配header头

 [返回](#top)

## STEP 9：useragent_Mod （黑名单）
  - 说明：
  `{"state":"off","action":"deny","useragent":["HTTrack|harvest|audit|dirbuster|pangolin|nmap|sqln|-scan|hydra|Parser|libwww|BBBike|sqlmap|w3af|owasp|Nikto|fimap|havij|PycURL|zmeu|BabyKrokodil|netsparker|httperf|bench","jio"],"hostname":[["127.0.0.1:8080","127.0.0.1"],"list"]}`

  上面的例子表示，规则关闭，匹配host为127.0.0.1 或者 127.0.0.1:8080 ，useragent正则匹配，匹配成功则拒绝访问，一般host设置为：`"hostname":["*",""]`表示所有（字符串匹配，非常快）
  state：规则是否启用
  hostname：匹配host
  useragent：匹配agent
  action：匹配动作

 [返回](#top)

## STEP 10：cookie_Mod（黑名单）
 - 说明：
 `{"state":"on","cookie":["\\.\\./","jio"],"hostname":["*",""],"action":"deny"}`

  上面的例子表示，规则启用，匹配任意host，cookies匹配正则，匹配成功则执行拒绝访问操作
  state：表示规则是否启用
  cookie：表示匹配cookie
  hostname：表示匹配host
  action：可选参数[deny、allow] 表示执行动作

  > action后续可以能增加其他action，所以预留在这，否则黑名单根本不需要action参数

 [返回](#top)

## STEP 11：args_Mod（黑名单）

 - 说明：
 `{"state":"on","hostname":["*",""],"args_data":["\\:\\$","jio"],"action":"deny"}`

 上面例子表示，规则启用，匹配任意host，query_string参数组匹配正则，成功则执行拒绝访问动作
 state：表示规则是否启用
 hostname：表示匹配host
 query_string：表示匹配args参数组
 action：表示匹配成功拒绝访问

 [返回](#top)

## STEP 12：post_Mod（黑名单）
 - 说明：
 `{"state":"on","hostname":["*",""],"posts_data":["\\$\\{","jio"],"action":"deny"}`

  上面的例子表示，规则启用，匹配任意host,post_str参数组匹配正则，成功则拒绝访问
  state：表示是否启用规则
  hostname：匹配host
  post_str：匹配post参数组
  action：匹配成功后拒绝访问

 [返回](#top)

## STEP 13：network_Mod（频率黑名单）
 - 说明：
 `{"state":"on","network":{"maxReqs":20,"pTime":10,"blackTime":600},"hostname":["id.game.com",""],"uri":["^/2.html$","jio"]}`

  上面的例子表示，规则启用，host为id.game.com,url匹配正则，匹配成功则进行访问频率限制，在10秒内访问次数超过20次，请求的IP到IP黑名单中10分钟（60秒\*10）
  state：表示是否启用规则
  hostname：表示匹配host
  uri：表示匹配uri
  network：maxReqs ==> 请求次数；pTime ==> 单位时间；blacktime ==> ip黑名单时长

  > 一般情况下，cc攻击的点一个网站只有为数不多的地方是容易被攻击的点，所以设计时，考虑增加通过url细化匹配。

 [返回](#top)

## STEP 14：replace_Mod（内容替换）
 - 说明：
 `{"state":"on","uri":["^/$","jio"],"hostname":["passport.game.com",""],"replace_list":[["联合","","联合FUCK"],["登录","","登录POSS"],["lzcaptcha\\?key='\\s\*\\+ key","jio","lzcaptcha?keY='+key+'&keytoken=@token@'"]]}`

  上面的例子表示，规则启用，host为passport.game.com,url是正则匹配，匹配成功则进行返回内容替换
  1：将"联合"替换为"联合FUCK"；
  2：将"登录"替换为"登录POSS"；
  3：通过正则进行匹配（`ngx.re.gsub`）其中@token@表示动态替换为服务器生成的一个唯一随机字符串
  state：表示是否启用规则
  hostname：表示匹配的host
  uri：表示匹配的uri
  replace_list：表示替换列表，参数1 ==> 被替换内容；参数2 ==> 匹配模式（正则、字符串）如例子中前2个替换列表就是字符串匹配，使用""即可，不能没有；参数3 ==> 被替换的内容

# API相关
参考doc目录下的api.md说明

# 样例
- 参见doc下，demo.md说明


# 性能评测

**操作系统信息**
OpenStar测试服务器：

```
 微软虚机，内网测试

 uname -a :
 Linux dpicsvr01 4.2.0-30-generic #36-Ubuntu SMP Fri Feb 26 00:58:07 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

 内存：
 cat /proc/meminfo | grep MemTotal
 MemTotal:       14360276 kB// 14GB

 CPU型号：cat /proc/cpuinfo | grep 'model name' |uniq
 Intel(R) Xeon(R) CPU E5-2660 0 @ 2.20GHz

 CPU核数：cat /proc/cpuinfo | grep "cpu cores" | uniq
 4

 CPU个数：cat /proc/cpuinfo | grep "physical id" | uniq | wc -l
 1
 ab：
 ab -c 1000 -n 100000 "http://10.0.0.4/test/a?a=b&c=d"
```
测试结果：
![enter description here][6]
 通过图片可以看到，关闭所有规则，做了2组测试，取最高的`8542`；

 启用规则（排除app，network，replace），测试结果`8388`，性能下降`1.81%`；

 启用规则（排除replace，app中未启用relua这个高消耗点），测试结果`7959`，性能下降`6.83%`；

 启用规则（排除useragent，ab工具默认被拦截了，第二个测试就不完全了。）测试结果`7116`，性能下降`16%`；

 总的来说，启用规则后，性能损失可以接受，根据自身的业务进行调整，还可以有所优化。

  [1]: https://github.com/agentzh
  [2]: http://openresty.org/cn/
  [3]: https://github.com/starjun/openstar/wiki/%E5%AE%89%E8%A3%85%E7%AF%87
  [4]: https://github.com/starjun/openstar/wiki/base.json
  [5]: https://github.com/starjun/openstar/raw/master/doc/Openstar.jpg "OpenStar.jpg"
  [6]: https://github.com/starjun/openstar/raw/master/doc/test.png "test.png"
  [7]: https://moonbingbing.gitbooks.io/openresty-best-practices/content/index.html
  [8]: http://www.modsecurity.org/
  [9]: https://github.com/loveshell/ngx_lua_waf
  [10]: https://github.com/starjun/openstar/wiki/0-realIpFrom_Mod
  [11]: https://github.com/starjun/openstar/wiki/1-ip_Mod
  [12]: https://github.com/starjun/openstar/wiki/2-host_method_Mod
  [13]: https://github.com/starjun/openstar/wiki/3-rewrite_Mod
  [14]: https://github.com/starjun/openstar/wiki/4-host_Mod
  [15]: https://github.com/starjun/openstar/wiki/5-app_Mod
  [16]: https://github.com/starjun/openstar/wiki/6-referer_Mod
  [17]: https://github.com/starjun/openstar/wiki/7-uri_Mod
  [18]: https://github.com/starjun/openstar/wiki/8-header_Mod
  [19]: https://github.com/starjun/openstar/wiki/9-useragent_Mod
  [20]: https://github.com/starjun/openstar/wiki/10-cookie_Mod
  [21]: https://github.com/starjun/openstar/wiki/11-args_Mod
  [22]: https://github.com/starjun/openstar/wiki/12-post_Mod
  [23]: https://github.com/starjun/openstar/wiki/13-network_Mod
  [24]: https://github.com/starjun/openstar/wiki/14-replace_Mod
  [27]: https://github.com/starjun/openstar/raw/master/doc/xq.jpg "xq.jpg"

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
