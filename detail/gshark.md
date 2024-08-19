## GShark <https://github.com/madneal/gshark>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-madneal-orange)
![GitHub stars](https://img.shields.io/github/stars/madneal/gshark.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.0-red)
![Time](https://img.shields.io/badge/Join-20201221-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


The project is based on Go and Vue to build a management system for sensitive information detection. For the full introduction, please refer to [articles](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzI3MjA3MTY3Mw==&action=getalbum&album_id=2376148333116850178#wechat_redirect) and [videos](https://mp.weixin.qq.com/mp/appmsgalbum?__biz=MzI3MjA3MTY3Mw==&action=getalbum&album_id=1834365721464651778#wechat_redirect). For now, all the scans are only targeted to the public environments, not local environments.

For the usage of GShark, please refer to the [wiki](https://github.com/madneal/gshark/wiki).

# Features

* Support multiple platforms, such as GitLab, GitHub, Searchcode, and Postman
* Flexible menu and API permission settings
* Flexible rules and filtering rules
* Utilize gobuster for subdomain brute force
* Easy-to-use management system
* Support for Docker deployment

# Quick start

## Docker

```
git clone https://github.com/madneal/gshark
cd gshark
docker-compose build && docker-compose up 
```

## Manual Deployment

### Requirements

* Nginx
* MySQL(version above **8.0**)

It is recommended to deploy the Front-End project using nginx. Place the `dist` folder in `/var/www/html`, and adjust the `nginx.conf` file (/etc/nginx/nginx.conf for Linux) to set up reverse proxy for the backend service. For detailed deployment tutorials, you can watch videos on [bilibili](https://www.bilibili.com/video/BV1Py4y1s7ap/) or [youtube](https://youtu.be/bFrKm5t4M54). For deployment on Windows, refer to [this link](https://www.bilibili.com/video/BV1CA411L7ux/).

### Nginx

Can use `nginx -t` to locate the `nginx.conf` file, then modify the `nginx.conf`:

```
// config the user accoring to your need
user  www www;
worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    server {
        listen       8080;
        server_name  localhost;

        location / {
            autoindex on;
            root   html;
            index  index.html index.htm;
        }
        location /api/ {
            proxy_set_header Host $http_host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            rewrite ^/api/(.*)$ /$1 break;
            proxy_pass http://127.0.0.1:8888;
        }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
    include servers/*;
}

```

The deployment work is straightforward. Find the corresponding version zip file from [releases](https://github.com/madneal/gshark/releases). 

Unzip and copy the files inside `dist` to `/var/www/html` folder of Nginx. 

```
unzip gshark*.zip
cd gshark*
mv dist /var/www/html/
# for Mac
mv dist /usr/local/www/html/
```

Start the Nginx and the Front-End is deployed successfully.

> [!TIP]
> If you installed Nginx by Homebrew, you need to stop Nginx by:
> ```shell
> brew services stop nginx
> ```

### Server service

For the first time, you need to rename `config-temp.yaml` to `config.yaml`. Then you can run the binary file `gshark` directly. Then access to `localhost:8080` for local deployment.

If you have not initial the database in the before, you will be redirec to the database initial page at first.

<img width="936" alt="image" src="https://github.com/user-attachments/assets/dfa7e53e-dc4a-4697-831f-a4f4f3810c3c">


For the scan service, it's necessary to config the corresponding rules. For example, Github or Gitlab rules.

### Incremental Deployment

For the incremental deployment, [sql.md](https://github.com/madneal/gshark/blob/master/sql.md) should be executed for the corresponding database operations.

## Development

### Server

``` 
git clone https://github.com/madneal/gshark.git

cd server

go mod tidy

mv config-temp.yaml config.yaml

go build

./gshark

or

go run main.go
```



### Web 

```
cd ../web

npm install

npm run serve
```

## Usage
### Add Token

#### GitHub

To execute the scan task for GitHub, you need to add a GitHub token for crawl information in GitHub. You can generate a token in [tokens](https://github.com/settings/tokens). Most access scopes are enough. For the GitLab search, remember to add a token too.

[![iR2TMt.md.png](https://s1.ax1x.com/2018/10/31/iR2TMt.md.png)](https://imgchr.com/i/iR2TMt)

#### Postman

Obtain the `postman.sid` cookie:

<img width="653" alt="image" src="https://github.com/madneal/gshark/assets/12164075/7775c8bb-79da-4e2b-b341-3c5b8395a6d0">


### Rule Configuration

For the Github or Gitlab rule, the rule will be matched by the syntax in the corresponding platforms. Directly, you config what you search at GitHub. You can download the rule import template CSV file, then batch import rules.

<img width="572" alt="image" src="https://user-images.githubusercontent.com/12164075/212504597-3e1ad5bd-bacf-433e-83e8-08de7eee6509.png">


### Filter Configuration

Filter is only addressed to GitHub search now. There are three classes of filters, including `extension`, `keyword`, `sec_keyword`. For `extension` and `keyword`, they can used for blacklist or whitelist.

For more information, you can refer to this [video](https://www.bilibili.com/video/BV1aG4y1c72N/?vd_source=ef4657ebf0549af8755f75118b6e81bb).

## Configuration

You are supposed to rename `config-temp.yaml` to `config.yaml` and config the database information and other information according to your environment.

### GitLab Base Url

<img width="363" alt="image" src="https://user-images.githubusercontent.com/12164075/203898719-1ce66395-083d-4226-937f-b6eed859addc.png">

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-11-12 发布文章[《GShark:多平台的敏感信息监测工具》](https://mp.weixin.qq.com/s/MG1lxiFg4a8KkAdhSMOu3Q)

## 最近更新

#### [v1.5.0] - 2024-08-17

**修复**  
- 组件版本升级  
- 将后端服务与扫描服务分离  
- 改进 Docker 镜像

#### [v1.4.6] - 2024-07-20

**修复**  
- 组件依赖升级  
- 修复部分安全问题  
- 丰富使用说明 README  
- 恢复本地 build 脚本  
- 简化项目，移除 autocode

#### [v1.4.5] - 2024-06-22

**修复**  
- 组件依赖升级  
- 修复 API 列表排序问题  
- 移除任务列表

#### [v1.4.4] - 2024-03-23

**修复**  
- 修复数据库初始化的问题  
- 修复 Postman 搜索结果格式  
- 前端组件安全升级

#### [v1.4.3] - 2024-03-16

**修复**  
- 组件版本的安全升级  
- 修复 golang User-Agent 被 Postman 禁用的问题  
- 修复前端缺少 postman 规则选项问题  

**新增**  
- 增加 Docker 版本 MySql 的数据持久化  
- GitHub client 可以忽略 TLS 错误

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
