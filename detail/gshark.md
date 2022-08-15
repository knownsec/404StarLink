## GShark <https://github.com/madneal/gshark>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-madneal-orange)
![GitHub stars](https://img.shields.io/github/stars/madneal/gshark.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)
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

#### [v1.0.0] - 2022-08-13

**Added**  
- 增加 Postman 监控功能

#### [v0.9.9] - 2022-07-09

**Added**  
- 增加多种规则类型支持  
- README 文档增加描述，增加文章以及视频链接  

**Fixed**  
- 修复批量导入规则默认没有启用规则的问题  
- 修改规则新增前端是否启用的样式

#### [v0.9.8] - 2022-07-02

**Added**  
- 批量导入规则功能  

**Fixed**  
- 登录背景图案调整  
- 企业微信通知提醒启用配置问题

#### [v0.9.7] - 2022-05-21

**Added**  
- Gitlab 提供更好的搜索能力  

**Removed**  
- 移除无用的图片资源  
- 优化 Config 数据结构，进行配置项合并

#### [v0.9.6] - 2022-05-04

**新增**  
- 增加 DNS 内置模块进行子域名爆破  
- 前端增加 domian 类型  
- 调整登录页样式  
- 增加中文 README  
- 增加 sql.md，用于增量部署  

**修复**  
- 修复保存时的数据库报错  
- 修复未发送消息提醒的问题  
- 修复未处理结果重复保存的问题  

**优化**  
- 简化 token 的数据结构

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
