## Glass <https://github.com/s7ckTeam/Glass>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-s7ckTeam-orange)
![GitHub stars](https://img.shields.io/github/stars/s7ckTeam/Glass.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.0.6-red)
![Time](https://img.shields.io/badge/Join-20210120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


# Glass(镜) V2.0-剑客到刺客的蜕变

## 一、简介：

```
    _____    _      _____                    
 __|___  |__| | __ |_   _|__  __ _ _ __ ___  
/ __| / / __| |/ /   | |/ _ \/ _` | '_ ` _ \ 
\__ \/ / (__|   <    | |  __/ (_| | | | | | |
|___/_/ \___|_|\_\   |_|\___|\__,_|_| |_| |_|
  ____ _               
 / ___| | __ _ ___ ___ 
| |  _| |/ _` / __/ __|
| |_| | | (_| \__ \__ \
 \____|_|\__,_|___/___/ 	http://www.s7ck.com    
```


Glass为s7ck Team 红队武器库F-Box里的一款信息收集工具。

在红队作战中，信息收集是必不可少的环节，如何才能从大量的资产中提取有用的系统(如OA、VPN、路由、Weblogic...)是众多红队人员头疼的问题。

Glass是一款针对资产列表的快速指纹识别工具，通过调用Fofa/ZoomEye/Shodan/360等api接口快速查询资产信息并识别重点资产的指纹，也可针对IP/IP段或资产列表进行快速的指纹识别。

Glass旨在帮助红队人员在资产信息收集期间能够快速从C段、大量杂乱的资产中精准识别到易被攻击的系统，从而实施进一步测试攻击。

 s7ck Team F-box旨在通过开源或者开放的方式，长期维护并推进涉及安全研究各个领域不同环节的工具化，高度自动化，将立足于不同安全领域、不同安全环节的研究人员和工具链接/封装/优化起来。
 
 主要目的是改善安全圈内工具庞杂、水平层次不齐、开源无人维护、工具找不到的等多种问题，营造一个更好更开放的安全工具促进与交流的技术氛围。

### 开发语言

* Python3

### 运行环境

* Linux
* Windows
* Mac

### 使用依赖库

* requests
* colorama
* prettytable
* xlsxwriter


### 安装
	git clone https://github.com/s7ckTeam/Glass
	cd Glass
	pip3 install -r requirements.txt

## 二、更新日志：

### 正式版
* 2.0.6 更改默认搜索设置，添加哪个`api`就会默认调用哪个，不需要指定，如果有多个`api`可`-s`指定
* 2.0.5 添加自定义搜索（-s,--search）
  1. 添加钟馗之眼（https://www.zoomeye.org/）搜索
  2. 在`config/config.py`中`zoomeyeApi`设置，输入`key`值即可（**注：** 用的时候注意api使用条数）
  3. -s参数[eye（钟馗之眼） or fofa（Fofa）]（python3 Glass.py -i 127.0.0.1 -s eye or fofa）
  4. 不加参数`-s`默认使用`fofa`搜索

* 2.0.4 添加删除更新的缓存文件
* 2.0.3 扫描域名或批量扫描时可不加协议（**注：** 建议添加协议）
* 2.0.2 增加自定义输出格式（-o,--output）
  1. 支持输出的格式有：`txt`、`json`、`html`、`xls`、`csv`
  2. 默认输出`txt`格式
  3. 输出目录在根目录`output`下
* 2.0
  1. 增加代理功能（--proxy）
     - 全局访问代理，支持http、https
     - 支持自定义（格式：http://127.0.0.1:8080或者https://127.0.0.1:8080）
     - 首次使用会按照参数获取相应代理，然后在根目录生成`/proxyFile/proxy.txt`
     - 参数（all）使用全部代理进行随机分配
     - 参数（cn）使用国内代理进行随机分配
     - 参数（http://127.0.0.1:8080或者https://127.0.0.1:8080） 自定义的代理
  2. 增加获取代理功能（--proxy-list）
     - 首次使用会按照参数获取相应代理，然后在根目录生成`/proxyFile/proxy.txt`
     - 参数（all）获取全部
     - 参数（cn）获取国内
  3. 增加在线更新功能（--update）
  4. 去除print，改用logging输出
  5. 优化运行代码，后期还会优化
  6. 增加对url协议使用相应协议的代理
  7. 增加查看版本参数（-v,--version）
  8. 使用不生成pyc文件
  9. 全局随机分配代理，获取到多少就用多少，每次访问都不一样
  10. 将获取到的代理文件保存，根目录生成`/proxyFile/proxy.txt`，终端以表格形式输出，一目了然
  11. 增加版本判断，建议使用 >=python 3.7.3
  12. 对证书认证方面的处理
  13. 每过15分钟会重新获取一次代理IP
* 1.3（添加`cookie`识别方式，将识别规则改为列表，防止重复的cms不带入识别，识别精准度提高，速度更快）
* 1.2（修复编码问题，以及fofa会员获取数量问题，现在默认`100`，在`config/config.py`中`fofaSize`更改，普通会员为`100`，高级`10000`，企业`100000`，请自行更改）
* 1.1（处理每日一说超时后写入空文件问题）
* 1.0（全面优化识别效率，命中率`99%`）
* 0.9（添加每日一说获取异常，添加识别规则）

### Glass V2.0新版内容部分截图

![](https://github.com/s7ckTeam/Glass/raw/main/Image/proxy_1.png)

![](https://github.com/s7ckTeam/Glass/raw/main/Image/proxy_2.png)

![](https://github.com/s7ckTeam/Glass/raw/main/Image/Glass_pa3.png)

### 测试版更新信息

  - 0.9（优化IP段的扫描，以及批量下可添加IP段）
  - 0.8（更改线程运行方式）
  - 0.7（与协程对比，最好还是用线程并发）
  - 0.6（更改配色方案，采用线程并发，增加单url以及批量url识别）
  - 0.5（优化采集速度以及与识别分开，增加输出）
  - 0.4（整理识别规则）
  - 0.3（添加指纹扫描）
  - 0.2（更新每天一说，让红队不再乏味）
  - 0.1（写出整体实现功能，Fofa接口的设置与采集）

## 三、使用方法：

```
Usage: python3 Glass.py -i 127.0.0.1 or 127.0.0.0/24
Usage: python3 Glass.py -i 127.0.0.1 -s eye or fofa
Usage: python3 Glass.py -f ips.txt
Usage: python3 Glass.py -u https://96.mk/
Usage: python3 Glass.py -w webs.txt
Usage: python3 Glass.py --proxy-list all or cn
Usage: python3 Glass.py (-i -f -u -w) 127.0.0.1 or 127.0.0.0/24 --proxy all or cn
Usage: python3 Glass.py --update
Usage: python3 Glass.py -u https://96.mk/ -o html


usage: Glass.py [-h] [-i IP] [-f FILE] [-u URL] [-w WEB] [--proxy PROXY] [--proxy-list PROXYLIST] [-v] [--update] [-o OUTPUTTARGET] [-s SEARCH]

Glass scan.

optional arguments:
  -h, --help            show this help message and exit
  -i IP, --ip IP        Input your ip.
  -f FILE, --file FILE  Input your ips.txt.
  -u URL, --url URL     Input your url.
  -w WEB, --web WEB     Input your webs.txt.
  --proxy PROXY         Input your proxy options(all or cn) or proxy address(127.0.0.1:8080).
  --proxy-list PROXYLIST
                        List the proxys.
  -v, --version         Show program's version number and exit.
  --update              Update the program.
  -o OUTPUTTARGET, --output OUTPUTTARGET
                        Select the output format.
  -s SEARCH, --search SEARCH
                        Choose your search engine.


-i 可指定单独IP或者IP段（需添加您fofa的API或者zoomeye的API）
-f 批量要扫的IP或IP段（需添加您fofa的API或者zoomeye的API）
-u 单个url识别
-w 批量url识别
-s 指定搜索引擎
--proxy all/cn/http://127.0.0.1:8080 使用 all表示全部 cn表示国内或者自定义的代理（支持http、https）
--proxy-list all/cn 获取代理 all表示全部 cn表示国内
```
#### 相关配置更改

* API设置
  1. 在`config/config.py`中`fofaApi`设置，输入对应的`email`与`key`即可
  2. 在`config/config.py`中`zoomeyeApi`设置，输入`key`值即可
* 线程默认 `100`可在`config/config.py`中`threadNum`修改线程数 **（注：建议在200以内）**
* 每日一说可设置开启关闭，在`config/config.py`中`tosayRun`，`True`为开，`False`为关
* fofa会员搜索的更改，默认搜索`100`，在`config/config.py`中`fofaSize`更改，普通会员为`100`，高级`10000`，企业`100000`，请自行更改


Glass提供了**四种**指纹识别方式，可从本地读取识别，也可以从FOFA进行批量调用API识别(需要FOFA密钥)。

**1.本地识别：**

```bash
python Glass.py -u http://www.s7ck.com  // 单url测试
python Glass.py -w url.txt  // url文件内

```

**2.FOFA识别：**

注意：从FOFA识别需要配置FOFA 密钥以及邮箱，在`.../config/config.py`内配置好密钥以及邮箱即可使用。

```bash
fofaApi = {
    "email": "admin@s7ck.com",
    "key": "1234567890",
}
```

```
python3 Glass.py -i 127.0.0.1  //支持单IP资产
python3 Glass.py -i 127.0.0.1/24 //支持IP段资产
python3 Glass.py -f ips.txt //支持文本内IP资产，可添加IP段
```

#### 结果输出

结果输出在`../output/xxxxx.txt`

#### 识别规则添加方法

目前只加了对源码和`header`头文件进行识别，后面会陆续添加识别的规则以及方式

已加入`cookie`识别

规则文件在`config/rules.py`

**添加方法**

```
['CMS', 'headers', '(nginx)']
['CMS', 'cookie', '(MorkerSession)']
['CMS', 'code', '(<title>Morker</title>)']

三种识别方式，headers头文件识别，cookie识别，code源码识别

支持同方式多种识别内容，比如：

['CMS', 'code', '(<title>Morker</title>)|css/css.css']

注：单引号和反斜杆记得转义，转义符号为\
```

## 四、效果：

**1.本地识别：**
![](https://github.com/s7ckTeam/Glass/raw/main/Image/u1.png)
![](https://github.com/s7ckTeam/Glass/raw/main/Image/u2.png)

**2.fofa识别：**

![](https://github.com/s7ckTeam/Glass/raw/main/Image/c0.png)
![](https://github.com/s7ckTeam/Glass/raw/main/Image/c1.png)
![](https://github.com/s7ckTeam/Glass/raw/main/Image/c2.png)
![](https://github.com/s7ckTeam/Glass/raw/main/Image/Glass.gif)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
