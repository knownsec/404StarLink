## ZoomEye-Python <https://github.com/knownsec/ZoomEye-python>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-Knownsec404-orange)
![GitHub stars](https://img.shields.io/github/stars/knownsec/ZoomEye-python.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V3.0.0-red)
![Time](https://img.shields.io/badge/Join-20200821-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

`ZoomEye` 是一款网络空间搜索引擎，用户可以使用浏览器方式 <https://www.zoomeye.org> 搜索网络设备。

`ZoomEye-python` 是一款基于 `ZoomEye API` 开发的 Python 库，提供了 `ZoomEye` 命令行模式，同时也可以作为 `SDK` 集成到其他工具中。该库可以让技术人员更便捷地**搜索**、**导出** `ZoomEye` 的数据。

### 0x01 安装步骤
可直接从 `pypi` 进行安装：

	pip3 install zoomeye

也可以通过 `github` 进行安装：

	pip3 install git+https://github.com/knownsec/ZoomEye-python.git


### 0x02 使用cli
在成功安装 `ZoomEye-python` 后，可以直接使用 `zoomeye` 命令，如下：

```
$ zoomeye -h
usage: zoomeye [-h] [-v] {info,init,search,clear} ...

positional arguments:
  {info,init,search,clear}
    info                Show ZoomEye account info
    init                Initialize the token for ZoomEye-python
    search              get network asset information based on query conditions.
    clear               Manually clear the cache and user information

options:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit

```

#### 1.初始化token
在使用 `ZoomEye-python cli` 前需要先初始化用户 `token`，该凭证用于验证用户身份以便从 `ZoomEye` 查询数据；仅支持 API-KEY 认证。

可以通过 `zoomeye init -h` 查看帮助，下面通过 `APIKEY` 来进行演示：

```
$ zoomeye init -apikey "01234567-acbd-00000-1111-22222222222"
Username: your username
Role: Professional
Points: 800000
Zoomeye Points: 0
```

用户可以通过登陆 `ZoomEye` 在个人信息中(<https://www.zoomeye.org/profile>) 获取 `APIKEY`；`APIKEY` 不会过期，用户可根据需求在个人信息中进行重置。


#### 2.用户信息
用户可以通过 `info` 命令获取用户信息、订阅详细信息和当前积分情况，如下：

```
$ zoomeye info
username: <username>
email: <email>
phone: <phone number>
created_at: 2021-01-15
Subscription:: {'plan': 'Professional', 'end_date': '2025-12-31', 'points': 800000, 'zoomeye_points': 0}
```

#### 3.搜索
搜索是 `ZoomEye-python` 最核心的功能，通过 `search` 命令进行使用。`search` 命令需要指定搜索关键词(`dork`)，下面我们进行简单的搜索：

```
$ zoomeye search "telnet" 
search "telnet" 
ip                            port                          domain                        update_time                   
134.xx.xx.129                 1901                          [unknown]                     2025-02-06T15:45:20           
134.xx.xx.138                 1901                          [unknown]                     2025-02-06T15:45:19
......

total: 20/9976411
```

使用 `search` 命令和使用浏览器在 `ZoomEye` 进行搜索一样简单，在默认情况下我们显示了较为重要的字段，用户可以使用这些数据了解目标信息：

	1.ip             ip 地址
    2.port           端口
    3.domain         目标域名
    4.update_time    目标扫描时间

`search` 支持以下参数(`zoomeye search -h`)，以便用户对数据进行处理，我们将在下文进行说明和演示：

    -facets facets        统计项，如果有多个，用逗号分隔；支持 country、subdivisions、city、product、service、device、os 和 port。
    -fields field=regexp  返回的字段，用逗号分隔；默认：ip, port, domain, update_time。更多信息，请参阅: https://www.zoomeye.org/doc/
    -sub_type {v4,v6,web,all}  数据类型，支持 v4、v6 和 web；默认为 v4。
    -page page            默认为第1页，按照更新时间排序。
    -pagesize pagesize    每页查询数量，默认是10条，最大是10,000条/页。
    -figure {pie,hist}    参数为数据图像化参数
    -save                 将搜索结果保存到本地
    -force                忽略本地缓存文件，直接从 ZoomEye 获取数据


#### 4.数据聚合
我们可以通过 `-facets`  进行数据的聚合统计，使用 `-facets` 可以查询该 dork 全量数据的聚合情况(由 `ZoomEye` 聚合统计后通过 `API` 获取)

```
$ zoomeye search "telnet" -facets product -pagesize 1
ip                            port                          domain                        update_time                   
177.xxx.xx.142               2020                          [unknown]                     2025-02-06T15:59:49           

total: 1/9976296
 ----------------------------------------
 ZoomEye total data:9976296
 -------------product Top 10-------------
 product                            count               
 MikroTik router config httpd       3326013             
 [unknown]                          2421245             
 Apache httpd                       2411293             
 ProFTPD                            285649              
 Pulse Secure VPN httpd             182296              
 Samsung printer telnetd            178147              
 Huawei telnetd                     144382              
 Huawei switch telnetd              120421              
 TP-LINK TL-WR841N WAP httpd        118836              
 DVR httpd                          100068 
```


#### 5.数据导出
`-save` 参数可以对数据进行导出如下：

```
$ zoomeye search "telnet" -pagesize 1 -save
search "telnet"  -pagesize 1 -save
ip                            port                          domain                        update_time                   
88.xx.xxx.78                  3011                          [unknown]                     2025-02-06T16:00:53           

total: 1/9976301
save file to telnet_1_1738829058.json successful!

```


#### 6. 数据图像化

`-figure` 参数为数据图像化参数，该参数提供了 `pie(饼图)` 和  `hist(柱状图)` 两种展示方式，在没有进行指定依旧显示数据，在指定  `-figure` 时，需要和 `-facets` 一起使用。饼图如下：

![](https://github.com/knownsec/ZoomEye-python/raw/master/images/pie.png)

柱状图如下：

![](https://github.com/knownsec/ZoomEye-python/raw/master/images/hist.png)


#### 7.清理功能
用户每天都会搜索大量的数据，这样就导致缓存文件夹所占的存储空间逐渐增大；如果用户在公共服务器上使用 `ZoomEye-python` 可能会导致自己的 `API KEY` 和 `ACCESS TOKEN` 泄漏。
为此 `ZoomEye-python` 提供了清理命令 `zoomeye clear`，清理命令可以缓存数据和用户配置进行清空。使用方式如下：

```
$zoomeye clear -h
usage: zoomeye clear [-h] [-setting] [-cache]

optional arguments:
  -h, --help  show this help message and exit
  -setting    clear user api key and access token
  -cache      clear local cache file
```


#### 12.缓存机制

`ZoomEye-python` 在 `cli` 模式下提供了缓存机制，位于 `~/.config/zoomeye/cache` 下，尽可能的节约用户配额；用户查询过的数据集将在本地缓存 5 天，当用户查询相同的数据集时，不会消耗配额。


### 0x04 使用SDK
#### 1.初始化token
同样，在 SDK 中仅支持通过 `APIKEY` 认证，如下：

**APIKEY**

```python
from zoomeye.sdk import ZoomEye
zm = ZoomEye(api_key="01234567-acbd-00000-1111-22222222222")
```

#### 2.SDK API
以下是 SDK 提供的接口以及说明：
```
1.userinfo()
    获取当前用户信息

2.search(dork, qbase64='', page=1, pagesize=20, sub_type='all', fields='', facets='')
    根据查询条件获取网络资产信息。
```


#### 3.使用示例

```python

from zoomeye.sdk import ZoomEye
>>> dir(ZoomEye)
['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_check_header', '_request', 'search', 'userinfo']
>>> zm = ZoomEye(api_key="01234567-acbd-00000-1111-22222222222")
>>> zm.search('country=cn')
{'code': 60000, 'message': 'success', 'query': 'country=cn', 'total': 823268005, 'data': [{...}], 'facets': {}}
```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-03-23 发布文章[《关于ZoomEye-python更新这件事》](https://paper.seebug.org/1522/)
- 2021-01-20 发布文章[《ZoomEye-python 使用指南》](https://paper.seebug.org/1461/)

## 最近更新

#### [v3.0.0] - 2025-02-06

**更新**  
- 使用 zoomeye v2 api

#### [v2.2.0] - 2023-04-12

**更新**  
- 移除用户名和密码的认证方式，仅支持 API- KEY 认证

#### [v2.1.1] - 2021-12-14

**更新**  
- 支持到处 dot 语言脚本，生成域名 IP 指向图，命令行和 sdk 均支持  
- 添加 domain 参数，支持域名查询功能(包括关联域名查询和子域名查询功能)  


<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
