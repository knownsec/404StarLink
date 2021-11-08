## myscan <https://github.com/amcai/myscan>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-amcai-orange)
![GitHub stars](https://img.shields.io/github/stars/amcai/myscan.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)
![Time](https://img.shields.io/badge/Join-20201120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


myscan是参考awvs的poc目录架构，pocsuite3、sqlmap等代码框架，以及搜集互联网上大量的poc，由python3开发而成的被动扫描工具。
此项目源自个人开发项目，结合个人对web渗透，常见漏洞原理和检测的代码实现，通用poc的搜集，被动扫描器设计，以及信息搜集等思考实践。

## 法律免责声明

未经事先双方同意，使用myscan攻击目标是非法的。  
myscan仅用于安全测试目的

## 运行原理
myscan依赖burpsuite和redis，需启动redis和burpsuite插入myscan的插件。

依靠burp强大的抓包和解析数据包的功能，插件调取api把burp的请求体和响应体的处理数据整合成json数据传输到redis。

myscan调取redis数据，对每一个request/response数据包进行perfile(访问url)、perfolder(每一个目录)、perscheme(每一个数据包)分类去重，通过redis分发到各个子进程与运行相应的poc。

![流程图](https://github.com/amcai/myscan/raw/master/docs/images/%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

## 演示地址

[myscan演示视频](https://www.bilibili.com/video/BV1tV411f7p6/)

## 如何运行

平台要求:

不支持Windows,目前仅支持Linux（Windows python多进程不会把变量共享过去）

软件要求: 

python > 3.7.5 , redis-server ,(开发基于3.7.5，建议使用此版本，某些版本会出问题)

```bash
$ redis-server # 起一个redis服务，默认监听127.1:6379
$ pip3 install -r requirements.txt 安装依赖
$ # burpsuite安转扩展插件,默认连接127.1:6379
$ python3 cli.py -h 
```

Example:

建议大批量测试时候禁用未授权,baseline，cors，jsonp等插件，指定输出:

```
python3 cli.py webscan --disable power baseline cors jsonp sensitive_msg_transfer host_inject --html-output test.html 
```
大批量测试时只测试严重rce的poc，可在--enable筛选出来的的poc上再次通过--level 3，筛选严重等级的poc
```
python3 cli.py webscan --enable poc_ struts2 --level 3
```
把redis所有数据清除（即清除当前的所有任务队列），针对指定host，指定redis连接方式,默认输出到myscan_result_{num}.html，启动10个进程，某些poc线程为5

```
python3 cli.py webscan --host 127.0.0.1 192.168 --redis pass@127.0.0.1:6379:0 --clean --process 10 --threads 5
```
启动反连平台(服务器端)

```
python3 cli.py reverse
```

更多参数

```
python cli.py -h
```

## 检测插件

目录扫描，重定向，XSS，SQL，XXE，CORS，JSONP，CRLF，CmdInject，敏感信息泄漏，Struts2，Thinkphp，Weblogic，Shiro... ，详见pocs目录，可根据数据包的特征，对每个参数进行测试，或者选择性测试，新的检测模块将不断添加。

## 优势与不足

* 支持--ipv6绕过防火墙， 优先解析域名为IPV6，前提是在支持IPV6的网站和网络上。

* 内置反连平台，支持rmi，ldap，http，dnslog方式，可配置config.py部署在内外网，POC准确率高。
* python代码开源，不会编程难写poc。
* 依靠burp和redis，不用写监听程序和多进程处理数据容易，同时也严重依赖burp。
* 自定义插件，比如把request/response数据包导入到elasticsearch，便于后续查询。
* 通过redis，可分布式检测。

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
