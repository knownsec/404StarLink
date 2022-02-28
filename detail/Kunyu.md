## Kunyu <https://github.com/knownsec/Kunyu>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-风起-orange)
![GitHub stars](https://img.shields.io/github/stars/knownsec/Kunyu.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.6.5-red)
![Time](https://img.shields.io/badge/Join-20211122-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


# 0x00 介绍

## 工具介绍

Kunyu (坤舆)，名字取自 <坤舆万国全图> ，测绘实际上是一个地理信息相关的专业学科，针对海里的、陆地的、天上的地理信息进行盘点。同样应用于网络空间，发现未知、脆弱的资产也是如此，更像是一张网络空间地图，用来全面描述和展示网络空间资产、网络空间各要素及要素之间关系，以及网络空间和现实空间的映射关系。所以我认为“坤舆”还是比较贴合这个概念的。

Kunyu(坤舆)，旨在让企业资产收集更高效，使更多安全相关从业者了解、使用网络空间测绘技术。

## 应用场景

对于 kunyu 的使用，应用场景可以有很多，例如：

* 企业内遗忘的，孤立的资产进行识别并加入安全管理。 
* 企业外部暴露资产进行快速排查，统计。
* 红蓝对抗相关需求使用，对捕获IP进行批量检查。
* 批量收集脆弱资产(0day/1day) 影响内的设备、终端。
* 新型网络犯罪涉案站点信息进行快速收集，合并，进行更高效的研判、分析。
* 对互联网上受相关漏洞影响的脆弱资产，进行统计、复现。
* .......

# 0x01 安装

**需要Python3以上的支持**

```
git clone https://github.com/knownsec/Kunyu.git
cd Kunyu
pip3 install -r requirements.txt

Linux:
	python3 setup.py install
	kunyu console

Windows:
	cd kunyu
	python3 console.py

PYPI:
	pip3 install kunyu
	
P.S. Windows同样支持python3 setup.py install
```

# 0x02 配置说明
在第一次运行程序时通过输入以下命令进行初始化操作，提供了其他登录方式，但是推荐使用API的方式，因为用户名/密码登录需要额外做一次请求，所以理论上API的方式会更加高效。
```
kunyu init --apikey <your zoomeye key> --seebug <your seebug key>
```
![](https://github.com/knownsec/Kunyu/raw/main/images/setinfo.png)

初次使用需要通过ZoomEye登录凭证，才使用该工具进行信息收集。

**ZoomEye访问地址：https://www.zoomeye.org/**

**Seebug访问地址：https://www.seebug.org/**

可以通过以下命令自定义输出文件路径 ，默认输出路径为:C:\Users\active user\kunyu\output\

```bash
kunyu init --output C:\Users\风起\kunyu\output
```

![](https://github.com/knownsec/Kunyu/raw/main/images/setoutput.png)

# 0x03 工具使用

## 命令详解

```
kunyu console
```
![](https://github.com/knownsec/Kunyu/raw/main/images/infos.png)

**Kunyu Command**

```
Global commands:
        info                                      Print User info
        SearchHost <query>                        Basic Host search
        SearchWeb <query>                         Basic Web search
        SearchIcon <File>/<URL>                   Icon Image search
        SearchBatch <File>                        Batch search Host
        SearchCert <Domain>                       SSL certificate Search
        SearchDomain <Domain>                     Domain name associated/subdomain search
        EncodeHash <encryption> <query>           Encryption method interface 
        HostCrash <IP> <Domain>                   Host Header Scan hidden assets
        Seebug <query>                            Search Seebug vulnerability information
        set <option>                              Set Global arguments values
        view/views <ID>                           Look over http/ssl row data information
        SearchKeyWord                             Query sensitive information by keyword
        Pocsuite3                                 Invoke the pocsuite component
        ExportPath                                Returns the path of the output file
        clear                                     Clear the console screen
        show                                      Show can set options
        help                                      Print Help info
        exit                                      Exit KunYu &
```

**OPTIONS**

```
ZoomEye:
	page <Number>    查询返回页数(默认查询一页，每页20条数据)
	dtype <0/1>      查询关联域名/子域名(设置0为查询关联域名，反之为子域名)
	stype <v4/v6>	 设置获取数据类型IPV4或IPV6，默认为 ipv4,ipv6 全选
	btype <host/web> 设置批量查询的API接口(默认为HOST)
	timeout <num>	 设置Kunyu HTTP请求的超时时间
```

## 使用案例

*Kunyu（坤舆）的使用教程如下所示*

**用户信息**

![](https://github.com/knownsec/Kunyu/raw/main/images/userinfo.png)

**HOST 主机搜索**

![](https://github.com/knownsec/Kunyu/raw/main/images/searchhost.png)

**Web 主机搜索**

![](https://github.com/knownsec/Kunyu/raw/main/images/searchweb.png)

**批量 IP 搜索**

![](https://github.com/knownsec/Kunyu/raw/main/images/searchbatch.png)

**Icon 搜索**

在搜集企业资产时，我们可以使用这样的方式进行检索相同 ico 图标资产，在关联相关企业资产时，通常会有不错的效果。但是需要注意的是如果某些站点也使用这个 ico 图标，可能会关联出无关资产(但是无聊用别人 ico 图标的人总归是少数吧)。支持url或本地文件的方式搜索。

**命令格式：**

SearchIocn https://www.baidu.com/favicon.ico

SearchIcon /root/favicon.ico

![](https://github.com/knownsec/Kunyu/raw/main/images/searchico.png)

**SSL证书搜索**

通过 SSL 证书的序列号进行查询，这样关联出来的资产较为精准，能搜索出使用相同证书的服务。碰到https站点时，可以通过这样的方式。

![](https://github.com/knownsec/Kunyu/raw/main/images/searchcert.png)

**特征搜索**

通过HTTP请求包特征或网站相关特征可以进行更加精准的串并相同框架资产

![](https://github.com/knownsec/Kunyu/raw/main/images/headersearch.png)

**多因素查询**

同样kunyu也支持多因素条件查询关联资产，可以通过ZoomEye逻辑运算语法实现。

![](https://github.com/knownsec/Kunyu/raw/main/images/factor.png)

**关联域名/子域名搜索**

对关联域名以及子域名进行搜索，默认查询关联域名，可以通过设置 dtype 参数设置 **关联域名/子域名** 两种模式。

命令格式：**SearchDomain Domain**

![](https://github.com/knownsec/Kunyu/raw/main/images/searchdomain.png)

**设置获取数据类型**

在V1.6.1版本后，用户可以通过stype参数设置获取的数据类型为IPV4或者IPV6，实现应用场景，默认参数为v4。

命令格式：**set stype = v6**

![](https://github.com/knownsec/Kunyu/raw/main/images/stype.png)

**查看Banner信息**

用户可以通过view命令查看指定序号对应信息的Banner，从而进一步分析前端代码及Header头，用户可以截取banner信息进一步的关联匹配。

命令格式: **view ID**

![](https://github.com/knownsec/Kunyu/raw/main/images/view.png)

用户也可以通过views命令查看指定序号的SSL证书信息，通过提取SLL证书信息中的敏感信息进一步关联。

命令格式：**views ID**

![](https://github.com/knownsec/Kunyu/raw/main/images/views.png)

**敏感信息收集**

在Kunyu v1.6.0版本后，增加了对banner中敏感信息的获取，平时使用正常使用相关语法，设置页数，Kunyu会自动收集上一次查询结果banner信息中的敏感数据，然后通过SearchKeyWord命令查看结果。**目前将持续测试关注该功能点**。

![](https://github.com/knownsec/Kunyu/raw/main/images/keyword.png)

**系统命令执行**

在Kunyu v1.6.0后增加了对系统命令执行的支持，可以通过执行常用的一些系统命令进行更方便有效的调试测绘数据，具体可执行命令列表可见README文件Issue中第11条。

**示例一**

![](https://github.com/knownsec/Kunyu/raw/main/images/systems.png)

**示例二**

![](https://github.com/knownsec/Kunyu/raw/main/images/system.png)

**编码哈希计算**

在一些场景下，可以通过该命令进行常用的HASH加密/编码，如：BASE64、MD5、mmh3、HEX编码，通过这种方式进行调试。

**命令格式：**

EncodeHash hex 7239dcc9beb5c9cd795415f9
EncodeHash md5 https://www.baidu.com/favicon.ico
EncodeHash md5 /root/favicon.ico
EncodeHash mmh3 https://www.baidu.com/favicon.ico
EncodeHash mmh3 /root/favicon.ico
EncodeHash base64 dasdasdsa

![](https://github.com/knownsec/Kunyu/raw/main/images/encode.png)

**Seebug漏洞查询**

通过输入想要查找的框架、设备等信息，查询历史相关漏洞，但是需要注意仅支持英文，这里后期会进行改进，升级。

命令格式: **Seebug tongda**

![](https://github.com/knownsec/Kunyu/raw/main/images/seebug.png)

**设置参数**

当设置set page = 2时，返回结果为40条，大家可以通过修改page参数，设置查询的页数，需要注意1 page = 20/条 ，可以根据需求修改该值，获取更多返回结果。

通过show显示可配置的参数，以及参数当前的值。

![](https://github.com/knownsec/Kunyu/raw/main/images/show.png)

![](https://github.com/knownsec/Kunyu/raw/main/images/set.png)

**Pocsuite3 联动**

在v1.3.1之后的版本中，您可以使用kunyu进行联动pocsuite3的console模式进行一体化的使用。

![](https://github.com/knownsec/Kunyu/raw/main/images/pocsuite.png)

**HOSTS头碰撞**

通过HOSTS碰撞，可以有效的碰撞出内网中隐藏的资产，根据中间件httpf.conf中配置的ServerName域名和IP捆绑访问即可直通内网业务系统！后续通过设置本地hosts文件实现本地DNS解析，因为本地hosts文件优先级高于DNS服务器解析。支持通过ZoomEye域名库反查或者读取TXT文件获取域名列表。

**命令格式：**

HostCrash C:\ip.txt C:\host.txt
HostCrash C:\ip.txt baidu.com
HostCrash 1.1.1.1 baidu.com
HostCrash 1.1.1.1 G:\host.txt

**示例一**

![](https://github.com/knownsec/Kunyu/raw/main/images/searchcrash.png)

**示例二**

![](https://github.com/knownsec/Kunyu/raw/main/images/searchcrashs.png)

**数据结果**

搜索的所有结果都保存在用户根目录下，并根据当前时间戳创建目录。单次启动的所有查询结果都在一个目录下，保存为Excel格式，给予更加直观的体验。可以通过ExportPath命令返回输出路径。

![](https://github.com/knownsec/Kunyu/raw/main/images/output.png)


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-11-23 发布文章[《Kunyu (坤舆) : 更高效的企业资产收集》](https://mp.weixin.qq.com/s/mjPDX8PhfnpjmS6LaMcD_A)

## 最近更新

#### [v1.6.5] - 2022-02-25

**新增**  
- 增加了对查询结果存活检测的功能  
- 修复了一些模块不兼容问题

#### [v1.6.4] - 2022-01-04

**新增**  
- 添加了“显示规则”/“显示配置”命令  
- 增加了外部加载指纹文件的功能

#### [v1.6.2] - 2021-12-11

**新功能**  
- 增加创建资产分布图功能  
- 优化依赖包版本  
- 增加了hosts crash Serverless 扫描的配置

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
