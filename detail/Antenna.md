## Antenna <https://github.com/wuba/Antenna>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-wuba-orange)
![GitHub stars](https://img.shields.io/github/stars/wuba/Antenna.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.2.1-red)
![Time](https://img.shields.io/badge/Join-20220914-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

Antenna是58同城安全团队打造的一款辅助安全从业人员辅助验证网络中多种漏洞是否存在以及可利用性的工具。其基于带外应用安全测试(
OAST)通过任务的形式，将不同漏洞场景检测能力通过插件的形式进行集合，通过与目标进行Out-of-bind的数据通信方式进行辅助检测。

## Antenna的目标

我们绝不仅仅只是将Antenna做成一款只能监听DNS、HTTP等协议来简单判断无回显类型漏洞的工具，我们的目标是尝试在良好使用体验的基础上支持高度灵活的自定义组件能力，满足用户通过Antenna探索并实现各种应用安全漏洞场景的辅助检测。尽可能得实现通过Antenna这款产品降低各种安全漏洞场景的检测成本。

## 相关网站

博客：[Antenna 博客](http://blog.antenna.cool/docs/intro)

演示平台：[演示平台](http://jiemuzu.cn)

漏洞靶场(已支持docker部署,docker-compose文件在项目docker目录中)：[lcttty/antenna-range:0.0.1](https://github.com/wuba/Antenna/blob/main/docker/docker-compose-range.yaml)

## Antenna_Inside计划

在我们开发Antenna时，就希望能够支持现有市场上流行的漏洞扫描工具漏洞结果回调与主动查询
,所以我们推出了CallBack与OpenAPI。为了让我们的这两个模块能够更加灵活与优雅。我们决定发起
Antenna_Inside计划，如果您是使用扫描工具的用户或者作者请联系我们，我们会无条件支持您的项目与
需求，帮助Antenna更方便的与漏洞扫描流程打通。如果您有推荐打通的项目，也可以在issue中提出来

已加入Antenna_Inside项目

| 项目名称       | 项目地址                                                                       |
|------------|----------------------------------------------------------------------------|
| EasyPen    | [https://github.com/lijiejie/EasyPen](https://github.com/lijiejie/EasyPen) |


## 近期使用疑问解答


#### 1、关于各类组件的使用说明以及能否再详细的进行说明自定义组件开发教程

回答：文章将在Antenna博客不定时更新，基础文章已有，后续详细的也会有的，作者在加班加点的写，绝不会让各位师傅等太久

#### 2、运行docker-compose命令后镜像构建时间过长

回答：可修改docker-compose文件中镜像,系统镜像已打包至dockerhub https://hub.docker.com/r/jihongjun/antenna/tags

#### 3、镜像部署总是遇到各种权限不允许的错误

回答：可将docker下列内容删除

```dockerfile
RUN addgroup --system antenna \
    && adduser --system --ingroup antenna antenna

USER antenna
```

#### 5、其他问题

如果您遇到了其他问题可查阅项目issue进行寻找相关解决方案，如果发现并没有其他人遇到和您相关的问题，请新建issue，
作者会及时回答您的疑问


## 相关教程链接
### 最新公告

Antenna chrome扩展 antenna-tools(试用版)发布[Antenna-tools 使用教程](http://blog.antenna.cool/blog/antenna_plugin)


### 关于部署
基础部署教程:[安装部署](http://blog.antenna.cool/docs/intro)

隐匿部署教程：[关于Antenna的隐匿性部署](http://blog.antenna.cool/blog/%20%20Secrecy)

前后端分离部署 [Antenna的前后端分离部署](http://blog.antenna.cool/blog/client_server)

### 关于配置

基础配置教程:[基础配置教程](http://blog.antenna.cool/docs/%E5%85%B3%E4%BA%8E%E9%85%8D%E7%BD%AE/config)

域名配置及DNS相关配置:[域名配置及阿里云dns服务修改教程](http://blog.antenna.cool/docs/%E5%85%B3%E4%BA%8E%E9%85%8D%E7%BD%AE/DNS)

开通邮箱通知以及邮箱授权码申请教程:[QQ邮箱授权码申请教程](https://service.mail.qq.com/cgi-bin/help?subtype=1&id=28&no=1001256)

### 关于任务

任务基础使用教程:[如何简单的使用任务](http://blog.antenna.cool/docs/%E5%85%B3%E4%BA%8E%E4%BB%BB%E5%8A%A1/task)

### 关于组件

组件基础使用教程:[Antenna的灵魂-组件Template](http://blog.antenna.cool/docs/%E5%85%B3%E4%BA%8E%E7%BB%84%E4%BB%B6/template)

xss 组件使用教程:[xss组件使用教程](http://blog.antenna.cool/docs/%E5%85%B3%E4%BA%8E%E7%BB%84%E4%BB%B6/xss)

组件开发教程:[如何编写Antenna组件](http://blog.antenna.cool/docs/%E5%85%B3%E4%BA%8E%E7%BB%84%E4%BB%B6/template_demo)

自定义HTTP组件使用教程[自定义HTTP组件使用教程](http://blog.antenna.cool/docs/%E5%85%B3%E4%BA%8E%E7%BB%84%E4%BB%B6/custom_http)
### 关于OPEN_API与CallBack

OPEN_API与CallBack使用教程:[关于OPEN_API与CallBack](http://blog.antenna.cool/docs/api_back)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.2.1] - 2022-10-19

**更新**  
- 优化HTTP/HTTPS请求处理模块，消息结果展示数据请求报文  
- 修复组件模块bug，添加组件代码展示&编辑功能  
- OPEN_API新增domain_contains、content_contains查询关键字  
- 优化用户使用体验、更新配置无需再重启docker及系统  
- 日常修复了一些bug

#### [v1.2.0] - 2022-10-14

**更新**  
- 修复了一些bug  
- 新增https监听功能

#### [v1.1] - 2022-09-16

**更新**  
- 增加 OpenAPI 的部分接口  
- 修复了一些 bug  
- 支持 chrome 扩展 chrome-tools

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
