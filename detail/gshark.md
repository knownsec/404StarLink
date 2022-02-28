## GShark <https://github.com/madneal/gshark>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-madneal-orange)
![GitHub stars](https://img.shields.io/github/stars/madneal/gshark.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.9.1-red)
![Time](https://img.shields.io/badge/Join-20201221-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


# GShark [![Go Report Card](https://goreportcard.com/badge/github.com/madneal/gshark)](https://goreportcard.com/report/github.com/madneal/gshark)   

The project is based on go with vue to build a management system for sensitive information detection. This is the total fresh version, you can refer the [old version](https://github.com/madneal/gshark/blob/gin/OLD_README.md) here. For the full introduction of the new version, please refer [here](https://mp.weixin.qq.com/s/Yoo1DdC2lCtqOMAreF9K0w).


# Features

* Support multi platform, including Gitlab, Github, Searchcode
* Flexible menu and API permission setting
* Flexible rules and filter rules
* Utilize gobuster to brute force subdomain
* Easily used management system

# Quick start

![GShark](https://user-images.githubusercontent.com/12164075/114326875-58e1da80-9b69-11eb-82a5-b2e3751a2304.png)

## Deployment

For the deployment, it's suggested to install nginx. Place the `dist` folder under `html`, modify the `nginx.conf` to reverse proxy the backend service. I have also made a video for the deployment in [bilibili](https://www.bilibili.com/video/BV1Py4y1s7ap/) and [youtube](https://youtu.be/bFrKm5t4M54). For the deploment in windows, refer [here](https://www.bilibili.com/video/BV1CA411L7ux/).

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

The deployment work is very easy. Find the corresponding binary zip file from [releases](https://github.com/madneal/gshark/releases). Unzip and run. Remember to copy the files inside `dist` to `html` folder of nginx.

### Web service

```
./gshark web
```

### Scan service

```
./gshark scan
```

## Development

### Server side

``` 
git clone https://github.com/madneal/gshark.git

cd server

go mod tidy

mv config-temp.yaml config.yaml

go build

./gshark web
```

If you want to set up the scan service, please run:

```
./gshark scan
```



### Web side

```
cd ../web

npm install

npm run serve
```

## Run

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

### Add Token

To execute `./gshark scan`, you need to add a Github token for crawl information in github. You can generate a token in [tokens](https://github.com/settings/tokens). Most access scopes are enough. For Gitlab search, remember to add token too.

[![iR2TMt.md.png](https://s1.ax1x.com/2018/10/31/iR2TMt.md.png)](https://imgchr.com/i/iR2TMt)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-11-12 发布文章[《GShark:多平台的敏感信息监测工具》](https://mp.weixin.qq.com/s/MG1lxiFg4a8KkAdhSMOu3Q)

## 最近更新

#### [v0.9.1] - 2022-02-25

**更新**  
- 升级前端组件依赖版本  
- 规则使用 switch 组件切换状态

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
