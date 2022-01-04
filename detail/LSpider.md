## LSpider <https://github.com/knownsec/LSpider>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-LoRexxar-orange)
![GitHub stars](https://img.shields.io/github/stars/knownsec/LSpider.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.2-red)
![Time](https://img.shields.io/badge/Join-20200821-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


# LSpider

LSpider - 一个为被动扫描器定制的前端爬虫

# 什么是LSpider?

一款为被动扫描器而生的前端爬虫~

由Chrome Headless、LSpider主控、Mysql数据库、RabbitMQ、被动扫描器5部分组合而成。

(1) 建立在Chrome Headless基础上，将模拟点击和触发事件作为核心原理，通过设置代理将流量导出到被动扫描器。

(2) 通过内置任务+子域名api来进行发散式的爬取，目的经可能的触发对应目标域的流量。

(3) 通过RabbitMQ来进行任务管理，支持大量线程同时任务。

(4) 智能填充表单，提交表单等。

(5) 通过一些方式智能判断登录框，并反馈给使用者，使用者可以通过添加cookie的方式来完成登录。

(6) 定制了相应的Webhook接口，以供Webhook统计发送到微信。

(7) 内置了Hackerone、bugcrowd爬虫，提供账号的情况下可以一键获取某个目标的所有范围。

### 为什么选择LSpider?

LSpider是专门为被动扫描器定制的爬虫，许多功能都是为被动扫描器而服务的。

建立在RabbitMQ的任务管理系统相当稳定，可以长期在无人监管的情况下进行发散式的爬取。

### LSpider的最佳实践是什么？

**服务器1（2c4g以上）**: Nginx + Mysql + Mysql管理界面（phpmyadmin）

将被动扫描器的输出位置设置为web路径下，这样可以通过Web同时管理结果以及任务。

LSpider部署5线程以上，设置代理连接被动扫描器（被动扫描器可以设置专门的漏扫代理）

**服务器2**（非必要，但如果部署在服务器1，那么就需要更好的配置）：RabbitMQ

### 还有什么问题？

LSpider从设计之初是为了配合像xray这种被动扫描器而诞生的，但可惜的是，在工具发展的过程中，深刻认识到爬虫是无法和被动扫描器拆分开来的。

强行将应该在被动扫描器实现的功能在爬虫端实现简直是舍本逐末，所以我们发起了另一个被动扫描器项目，如果有机会，后续还会开源出来给大家。

### 设计思路？

[为被动扫描器量身打造一款爬虫-LSpider](https://lorexxar.cn/2021/01/28/lspider-design/)

# Usage

[安装&使用](https://github.com/knownsec/LSpider/blob/master/docs/init.md)

你可以通过下面的命令来测试是否安装成功

```
python3 manage.py SpiderCoreBackendStart --test
```

通过dockerfile安装（不推荐的安装模式）
```
cd ./docker

docker-compose up -d
```

[dockerfile 安装&使用](https://github.com/knownsec/LSpider/blob/master/docker/readme.md)

**使用dockerfile安装，推荐修改其中必要的配置信息以避免安全漏洞诞生。**

**值得注意的是，以下脚本可能会涉及到项目路径影响，使用前请修改相应的配置**

建议配合screen来挂起进程

启动LSpider webhook 与漏洞展示页面（默认端口2062）

```
./lspider_webhook.sh
```

启动LSpider
```
./lspider_start.sh
```

完全关闭LSpider
```
./lspider_stop.sh
```

启动被动扫描器
```
./xray.sh
```

# 一些关键的配置

[配置说明](https://github.com/knownsec/LSpider/blob/master/docs/config.md)

# 如何配置扫描任务 以及 其他的配置相关

其中包含了如何配置扫描任务、鉴权信息、webhook。

值得注意的是，文中提到的Cookie配置，格式为浏览器请求包复制即可。

[如何配置扫描任务 以及 其他的配置相关](https://github.com/knownsec/LSpider/blob/master/docs/manage.md)

扫描器结果输出到配置文件相同目录（默认为vuls/）,则可以通过web界面访问。

![](https://github.com/knownsec/LSpider/raw/master/docs/6.png)

# 使用内置的hackerone、bugcrowd爬虫获取目标

使用hackerone爬虫，你需要首先配置好hackerone账号
```
 python3 .\manage.py HackeroneSpider {appname}
```
![](https://github.com/knownsec/LSpider/raw/master/docs/4.png)

同理，bugcrowd使用
```
 python3 .\manage.py BugcrowdSpider {appname}
```

![](https://github.com/knownsec/LSpider/raw/master/docs/5.png)


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-01-28 发布文章[《为被动扫描器量身打造一款爬虫 - LSpider》](https://paper.seebug.org/1473/)

## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
