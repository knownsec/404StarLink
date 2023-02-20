## GShark <https://github.com/madneal/gshark>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-madneal-orange)
![GitHub stars](https://img.shields.io/github/stars/madneal/gshark.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1.4-red)
![Time](https://img.shields.io/badge/Join-20201221-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

中文 | [英文](README.md)
<p align="center">
   <img alt="GgShark logo" src="https://s1.ax1x.com/2018/10/17/idhZvj.png" />
   <h3 align="center">GShark</h3>
   <p align="center">Scan for sensitive information easily and effectively.</p>
</p>

# GShark [![Go Report Card](https://goreportcard.com/badge/github.com/madneal/gshark)](https://goreportcard.com/report/github.com/madneal/gshark)   

项目基于 Go 以及 Vue 搭建的敏感信息检测管理系统。关于的完整介绍请参考[这里](https://mp.weixin.qq.com/s/Yoo1DdC2lCtqOMAreF9K0w)。

# 特性

* 支持多个搜索平台，包括 Github，Gitlab（不稳定支持），Searchcode
* 灵活的菜单以及 API 权限管理
* 灵活的规则以及过滤规则设置
* 支持 gobuster 作为子域名爆破的支持
* 方便易用

# 快速开始

![GShark](https://user-images.githubusercontent.com/12164075/114326875-58e1da80-9b69-11eb-82a5-b2e3751a2304.png)

## 部署

建议通过 nginx 部署前端项目。 将 `dist` 文件夹放在 `/var/www/html`下，修改 `nginx.conf` 来反向代理后端服务。在[bilibili](https://www.bilibili.com/video/BV1Py4y1s7ap/) 和 [youtube](https://youtu.be/bFrKm5t4M54) 可以参考部署视频教程。 Windows 下的部署请参考[这里](https://www.bilibili.com/video/BV1CA411L7ux/)。

```
location /api/ {
proxy_set_header Host $http_host;
proxy_set_header  X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
rewrite ^/api/(.*)$ /$1 break;
proxy_pass http://127.0.0.1:8888;
}
```

部署工作非常简单。 从 [releases](https://github.com/madneal/gshark/releases) 中找到对应的版本 zip 文件。 解压后得将 `dist` 中的文件复制到  `/var/www/html` 文件夹中。

### Web 服务

```
./gshark web
```

### 扫描服务

```
./gshark scan
```

## 开发

### 服务端

``` 
git clone https://github.com/madneal/gshark.git

cd server

go mod tidy

mv config-temp.yaml config.yaml

go build

./gshark web
```

启动扫描服务：

```
./gshark scan
```



### Web 端

```
cd ../web

npm install

npm run serve
```

## 运行

```
USAGE:
   gshark [global options] command [command options] [arguments...]

COMMANDS:
     web      Startup a web Service
     scan     Start to scan github leak info
     help, h  Show a list of commands or help for one command

GLOBAL OPTIONS:
   --debug, -d             Debug Mode
   --host value, -H value  web listen address (default: "0.0.0.0")
   --port value, -p value  web listen port (default: 8000)
   --time value, -t value  scan interval(second) (default: 900)
   --help, -h              show help
   --version, -v           print the version
```

### 添加 Token

执行扫描任务需要在 Github 的 Github token。你可以在 [tokens](https://github.com/settings/tokens) 中生成令牌，只需要 public_repo 的读权限即可。对于 Gitlab 扫描，请记得添加令牌。

[![iR2TMt.md.png](https://s1.ax1x.com/2018/10/31/iR2TMt.md.png)](https://imgchr.com/i/iR2TMt)

## FAQ

1. 默认登录的用户名密码（**及时修改**）：

gshark/gshark

2. 数据库初始化失败

确保数据库 mysql 版本高于 5.6。如果是第二次初始化的时候记得移除第一次初始化产生的实例。

3. `go get ./... connection error`

[使用 GOPROXY](https://madneal.com/post/gproxy/:

```
go env -w GOPROXY=https://goproxy.cn,direct
go env -w GO111MODULE=on
```
4. 部署前端项目后，页面空白

尝试清除 LocalStorage


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-11-12 发布文章[《GShark:多平台的敏感信息监测工具》](https://mp.weixin.qq.com/s/MG1lxiFg4a8KkAdhSMOu3Q)

## 最近更新

#### [v1.1.4] - 2023-02-15

**Fixed**  
- 修复无法变更规则状态的问题  
- 增加新增 token 的 postman 类型  

**Added**  
- 增加 startSecFilterTask 以及 getTaskStatus API 权限初始化

#### [v1.1.3] - 2023-01-31

**Fixed**  
- 修复变更规则错误的问题  
- 修复搜索代码结果错误的问题  

**Added**  
- 增加 switchRuleStatus 权限初始化  
- github client 初始化增加 httpcache

#### [v1.1.2] - 2023-01-18

**Fixed**  
- 修复执行过滤任务时未成功忽略仓库的问题  
- 修复 deleted_at 字段造成的初始化失败的问题  
- 修复字段问题导致忽略单个结果失败的问题  

**Added**  
- 增加仅展示二次过滤的结果  
- 增加 getTaskStatus API 权限初始化

#### [v1.1.1] - 2023-01-16

**Mofified**  
- 修改日志时间格式  

**Fixed**  
- 修复前端变更过滤规则问题  
- 修改忽略仓库状态的问题  
- 修复 filter_type 黑白名单问题

#### [v1.1.0] - 2023-01-15

**Added**  
- 启用二次过滤规则功能(重大更新)  

**Modified**  
- 优化 GitHub 搜索  
- 过滤规则重构，支持 extension, keyword, sec_keyword 白名单以及黑名单过滤  
- 优化匹配结果展示，突出匹配的关键词  
- 修改 eslint 规则

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
