## Kunpeng <https://github.com/opensec-cn/kunpeng>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-opensec-orange)
![GitHub stars](https://img.shields.io/github/stars/opensec-cn/kunpeng.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)
![Time](https://img.shields.io/badge/Join-20201120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


## 简介

Kunpeng是一个Golang编写的开源POC检测框架，集成了包括数据库、中间件、web组件、cms等等的漏洞POC（[查看已收录POC列表](doc/plugin.md)），可检测弱口令、SQL注入、XSS、RCE等漏洞类型，以动态链接库的形式提供调用，通过此项目可快速开发漏洞检测类的系统，比攻击者快一步发现风险漏洞。

这不是一个POC框架轮子，而是为了解决轮子问题而设计的，也不仅仅只是框架，定位是期望成为一个大家共同维护的漏洞POC库，安全开发人员只需专注于相关安全检测系统的业务逻辑代码实现，而不必各自重复的耗费精力维护漏洞库。

**为避免被恶意使用，此项目所有收录的漏洞均为验证POC和理论判断，不存在漏洞利用过程，不会对目标发起真实攻击和漏洞利用。**

运行环境：Windows，Linux，Darwin  
工作形态：动态链接库，so、dll、dylib、go plugin  

## 特点
- 开箱即用，无需安装任何依赖
- 跨语言使用，动态链接库形式提供调用
- 单文件，更新方便，直接覆盖即可
- 开源社区维护，内置常见漏洞POC
- 最小化漏洞验证和理论判断，尽量避免攻击行为


## 使用场景
渗透测试辅助工具：例如msf，交互控制台 -> **Kunpeng**

网络资产安全监控：例如巡风，端口扫描 -> 指纹识别 -> **kunpeng**  或  nmap -> **kunpeng**

扫描器： 作为扫描器的漏洞库

更多使用场景可自由发挥 

## 使用方法

```go
接口调用说明

/*  传入需检测的目标JSON，格式为：
    {
        "type": "web", //目标类型web或者service
        "netloc": "http://xxx.com", //目标地址，web为URL，service格式为123.123.123.123:22
        "target": "wordpress", //目标名称，GO插件注册时使用的字符串（模糊匹配）、JSON插件的target属性（模糊匹配）、CVE编号（例：CVE-xx-xxx）、KPID(例：KP-0013)编号，决定使用哪些POC进行检测，具体查看 /doc/plguin.md
        "meta":{
            "system": "windows",  //操作系统，部分漏洞检测方法不同系统存在差异，提供给插件进行判断
            "pathlist":[], //目录路径URL列表，部分插件需要此类信息，例如列目录漏洞插件
            "filelist":[], //文件路径URL列表，部分插件需要此类信息，例如struts2漏洞相关插件
            "passlist":[] //自定义密码字典
        } // 非必填
    }
    返回是否存在漏洞和漏洞检测结果
*/
Check(taskJSON string) string

// 获取插件列表信息
GetPlugins() string


/*  配置设置，传入配置JSON，格式为：
    {
        "timeout": 15, // 插件连接超时
        "aider": "http://123.123.123.123:8088", // 漏洞辅助验证接口，部分漏洞无法通过回显判断是否存在漏洞，可通过辅助验证接口进行判断。python -c'import socket,base64;exec(base64.b64decode("aGlzdG9yeSA9IFtdCndlYiA9IHNvY2tldC5zb2NrZXQoc29ja2V0LkFGX0lORVQsc29ja2V0LlNPQ0tfU1RSRUFNKQp3ZWIuYmluZCgoJzAuMC4wLjAnLDgwODgpKQp3ZWIubGlzdGVuKDEwKQp3aGlsZSBUcnVlOgogICAgdHJ5OgogICAgICAgIGNvbm4sYWRkciA9IHdlYi5hY2NlcHQoKQogICAgICAgIGRhdGEgPSBjb25uLnJlY3YoNDA5NikKICAgICAgICByZXFfbGluZSA9IGRhdGEuc3BsaXQoIlxyXG4iKVswXQogICAgICAgIGFjdGlvbiA9IHJlcV9saW5lLnNwbGl0KClbMV0uc3BsaXQoJy8nKVsxXQogICAgICAgIHJhbmtfc3RyID0gcmVxX2xpbmUuc3BsaXQoKVsxXS5zcGxpdCgnLycpWzJdCiAgICAgICAgaHRtbCA9ICJORVcwMCIKICAgICAgICBpZiBhY3Rpb24gPT0gImFkZCI6CiAgICAgICAgICAgIGhpc3RvcnkuYXBwZW5kKHJhbmtfc3RyKQogICAgICAgICAgICBwcmludCAiYWRkIityYW5rX3N0cgogICAgICAgIGVsaWYgYWN0aW9uID09ICJjaGVjayI6CiAgICAgICAgICAgIHByaW50ICJjaGVjayIrcmFua19zdHIKICAgICAgICAgICAgaWYgcmFua19zdHIgaW4gaGlzdG9yeToKICAgICAgICAgICAgICAgIGh0bWw9IlZVTDAwIgogICAgICAgICAgICAgICAgaGlzdG9yeS5yZW1vdmUocmFua19zdHIpCiAgICAgICAgcmF3ID0gIkhUVFAvMS4wIDIwMCBPS1xyXG5Db250ZW50LVR5cGU6IGFwcGxpY2F0aW9uL2pzb247IGNoYXJzZXQ9dXRmLThcclxuQ29udGVudC1MZW5ndGg6ICVkXHJcbkNvbm5lY3Rpb246IGNsb3NlXHJcblxyXG4lcyIgJShsZW4oaHRtbCksaHRtbCkKICAgICAgICBjb25uLnNlbmQocmF3KQogICAgICAgIGNvbm4uY2xvc2UoKQogICAgZXhjZXB0OnBhc3M="))'
在辅助验证机器上运行以上代码，填入http://IP:8088，不开启则留空。
        "http_proxy": "http://123.123.123.123:1080", // HTTP代理，所有插件http请求流量将通过代理发送（需使用内置的http请求函数util.RequestDo）
        "pass_list": ["passtest"], // 默认密码字典，不定义则使用硬编码在代码里的小字典
        "extra_plugin_path": "/tmp/plugin/" // 除已编译好的插件（Go、JSON）外，可指定额外插件目录（仅支持JSON插件），指定后程序会周期读取加载插件
    }
*/
SetConfig(configJSON string)

// 开启web接口，开启后可通过web接口进行调用，webapi调用格式请查看例子：/example/call_webapi_test.py
StartWebServer(bindAddr string)

// 获取当前版本 例如：20190227
GetVersion() string
```

## 使用例子
Python

```python
#coding:utf-8

import time
import json
from ctypes import *

# 加载动态连接库
kunpeng = cdll.LoadLibrary('./kunpeng_c.so')

# 定义出入参变量类型
kunpeng.GetPlugins.restype = c_char_p
kunpeng.Check.argtypes = [c_char_p]
kunpeng.Check.restype = c_char_p
kunpeng.SetConfig.argtypes = [c_char_p]
kunpeng.GetVersion.restype = c_char_p

# 获取插件信息
out = kunpeng.GetPlugins()
print(out)

# 修改配置
config = {
    'timeout': 10,
    # 'aider': 'http://xxxx:8080',
    # 'http_proxy': 'http://xxxxx:1080',
    # 'pass_list':['xtest']
    # 'extra_plugin_path': '/home/test/plugin/',
}
kunpeng.SetConfig(json.dumps(config))

# 开启日志打印
kunpeng.ShowLog()

# 扫描目标
task = {
    'type': 'web',
    'netloc': 'http://www.google.cn',
    'target': 'web'
}
task2 = {
    'type': 'service',
    'netloc': '192.168.0.105:3306',
    'target': 'mysql'
}
out = kunpeng.Check(json.dumps(task))
print(json.loads(out))
out = kunpeng.Check(json.dumps(task2))
print(json.loads(out))
```

更多例子查看: [example] 目录，目前已提供python、golang、nodejs、lua、java的调用例子，欢迎提交更多语言的调用样例。


## 插件开发
支持2种类型插件，Go和JSON插件，大部分漏洞使用JSON插件即可实现验证，分别存放在plugin/go/和plugin/json/目录中。

- golang插件例子1

```go
// 包名需定义goplugin
package goplugin

// 引入plugin
import (
	"fmt"
	"github.com/opensec-cn/kunpeng/plugin"
	"github.com/go-redis/redis"
)

// 定义插件结构，info，result需固定存在
type redisWeakPass struct {
	info   plugin.Plugin // 插件信息
	result []plugin.Plugin // 漏洞结果集，可返回多个
}

func init() {
    // 注册插件，定义插件目标名称
	plugin.Regist("redis", &redisWeakPass{})
}
func (d *redisWeakPass) Init() plugin.Plugin{
	d.info = plugin.Plugin{
		Name:    "Redis 未授权访问/弱口令", // 插件名称
		Remarks: "导致敏感信息泄露，严重可导致服务器直接被入侵控制。", // 漏洞描述
		Level:   0, // 漏洞等级 {0:"严重"，1:"高危"，2："中危"，3："低危"，4："提示"}
		Type:    "WEAKPASS", // 漏洞类型，自由定义
		Author:  "wolf", // 插件编写作者
	    	References: plugin.References{
		    URL: "https://www.freebuf.com/vuls/162035.html", // 漏洞相关文章
		    CVE: "", // CVE编号，没有留空或不申明
		    KPID: "KP-0008", // kunpeng的POC编号，累加数字
		},
	}
	return d.info
}

func (d *redisWeakPass) GetResult() []plugin.Plugin {
	var result = d.result
	d.result = []plugin.Plugin{}
	return result
}

func (d *redisWeakPass) Check(netloc string, meta plugin.TaskMeta) bool {
	for _, pass := range meta.PassList {
		client := redis.NewClient(&redis.Options{
			Addr:     netloc,
			Password: pass,
			DB:       0,
		})
		_, err := client.Ping().Result()
		if err == nil {
			client.Close()
			result := d.info
			result.Request = fmt.Sprintf("redis://%s@%s", pass, netloc)
			if pass == "" {
				result.Remarks = fmt.Sprintf("未授权访问，%s", result.Remarks)
			} else {
				result.Remarks = fmt.Sprintf("弱口令：%s,%s", pass, result.Remarks)
			}
			d.result = append(d.result, result)
			return true
		}
	}
	return false
}
```


- golang插件例子2

```go
package goplugin

import (
	"net/http"
	"strings"
	"github.com/opensec-cn/kunpeng/util"
	"github.com/opensec-cn/kunpeng/plugin"
)

type webDavRCE struct {
	info   plugin.Plugin
	result []plugin.Plugin
}

func init() {
	plugin.Regist("iis", &webDavRCE{})
}

func (d *webDavRCE) Init() plugin.Plugin{
	d.info = plugin.Plugin{
		Name:    "WebDav PROPFIND RCE(理论检测)",
		Remarks: "CVE-2017-7269,Windows Server 2003R2版本IIS6.0的WebDAV服务中的ScStoragePathFromUrl函数存在缓存区溢出漏洞",
		Level:   1,
		Type:    "RCE",
		Author:  "wolf",
		References: plugin.References{
			URL: "https://www.seebug.org/vuldb/ssvid-92834",
			CVE: "CVE-2017-7269",
			KPID: "KP-0009",
		},
	}
	return d.info
}

func (d *webDavRCE) GetResult() []plugin.Plugin {
	var result = d.result
	d.result = []plugin.Plugin{}
	return result
}

func (d *webDavRCE) Check(URL string, meta plugin.TaskMeta) bool {
	request, err := http.NewRequest("OPTIONS", URL, nil)
	if err != nil {
		return false
	}
	// 使用封装好的RequestDo函数发送http请求
	resp, err := util.RequestDo(request, true)
	if err != nil {
		return false
	}
	if resp.Other.Header.Get("Server") == "Microsoft-IIS/6.0" && strings.Contains(resp.Other.Header.Get("Allow"), "PROPFIND") {
		result := d.info
		result.Response = resp.ResponseRaw
		result.Request = resp.RequestRaw
		d.result = append(d.result, result)
		return true
	}
	return false
}
```

- JSON插件例子

```javascript
{
    "//": "用 Google 的方式进行注释",
    "//": "插件所属应用名，自由定义",
    "target": "wordpress",
    "meta":{
        "//": "插件名称",
        "name": "WordPress example.html jQuery DomXSS",
        "//": "漏洞描述",
        "remarks": "WordPress example.html jQuery 1.7.2 存在DomXSS漏洞",
        "//": "漏洞等级 {0:严重，1:高危，2：中危，3：低危，4：提示}",
        "level":   3,
        "//": "漏洞类型，自由定义",
        "type":    "XSS",
        "//": "插件编写作者",
        "author":  "wolf",
        "references": {
            "//": "漏洞相关文章",
            "url":"https://www.seebug.org/vuldb/ssvid-89179",
            "//": "CVE编号，没有留空",
            "cve":"",
	    "//": "kunpeng的POC编号，累加数字",
	    "kpid":"KP-0003"
        }
    },
    "request":{
        "//": "漏洞请求URL",
        "path": "/wp-content/themes/twentyfifteen/genericons/example.html",
        "//": "请求POST内容，留空即为GET",
        "postData": ""
    },
    "verify":{
        "//": "漏洞验证类型 {string：字符串判断,regex：正则匹配,md5：文件md5}",
        "type":  "string",
        "//": "漏洞验证值，与type相关联",
        "match": "jquery/1.7.2/jquery.min.js"
    }
}
```

### 编译

**注意, 第三方库管理已更改为GoMod**

```shell
go get -d github.com/opensec-cn/kunpeng
cd $GOPATH/src/github.com/opensec-cn/kunpeng


# 静态资源打包进工程的小程序
go install github.com/mjibson/esc

# 打包JSON插件到项目代码中
esc -include='\.json$' -o plugin/json/JSONPlugin.go -pkg jsonplugin plugin/json/

# 编译c版本（所有语言均可使用）
go build -buildmode=c-shared --ldflags="-w -s -X main.VERSION=20190226" -o kunpeng_c.so

# 编译Go专用版本（不支持win）
go build -buildmode=plugin --ldflags="-w -s -X main.VERSION=20190226" -o kunpeng_go.so

# 样例测试
python example/call_so_test.py
go run example/callsoTest.go
```

### 效果图

![img](https://github.com/opensec-cn/kunpeng/raw/master/doc/img.png)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
