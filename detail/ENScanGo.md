## ENScanGo <https://github.com/wgpsec/ENScan_GO>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-wgpsec-orange)
![GitHub stars](https://img.shields.io/github/stars/wgpsec/ENScan_GO.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1.0-red)
![Time](https://img.shields.io/badge/Join-20221117-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

剑指HW/SRC，解决在HW/SRC场景下遇到的各种针对国内企业信息收集难题

## 🤷‍♂️郑重声明

文中所涉及的技术、思路和工具仅供以安全为目的的学习交流使用，任何人不得将其用于非法用途以及盈利等目的，否则后果自行承担。

使用均为公开数据，**不提供破解、绕过防护手段**，使用程序可能导致 ⌈账号异常⌋

**若该程序影响或侵犯到您的合法权益，请与我们联系** admin#wgpsec.org(#替换为@)

## ⚒️功能列表

![ENScanGo](https://github.com/wgpsec/ENScan_GO/raw/master/README/ENScanGo.png)

- 支持以下数据源
    - 爱企查
    - 天眼查
    - 快查
    - 企查查（不提供）
    - 小蓝本（不提供）
- 数据插件
    - 阿拉丁 （数据反馈比较老旧暂时下线）
    - 酷安市场
    - 七麦数据
    - 备案信息查询API

- 可查询信息
    - ICP备案
    - APP
    - 微博
    - 微信公众号
    - 控股公司
    - 供应商
    - 小程序
    - 公开招聘信息
    - 对外投资信息
    - ...
- 实用功能
    - 支持合并导出
    - 正则过滤公司
    - 支持深度查询 收集多层孙公司
    - 支持API模式提供工具联动


## 使用指南

### 首次使用

前往[RELEASE](https://github.com/wgpsec/ENScan_GO/releases)下载编译好的文件使用

首次使用时需要使用 -v 命令生成配置文件并配置Cookie

```
./enscan -v
```

### 快速使用

*如遇到无法访问等情况，可自行尝试挂上burp或代理*

**默认公司信息** (网站备案, 微博, 微信公众号, app)

```
./enscan -n 小米
```

**批量查询**（ 文本按行分隔 可选PID模式）

```
./enscan -f f.txt
```

**对外投资占股100%的公司**

```
./enscan -n 小米 -invest 100
```

**组合筛选**

大于51%公司、分支机构，只要ICP备案信息

```
./enscan -n 小米 -field icp -invest 51  --branch
```

收集孙公司 (deep参数，需要与invest一起使用) 大于51%公司、分支机构，只要ICP备案信息

```
./enscan -n 小米 -field icp -invest 51 --branch --deep 2
```

**使用不同渠道**

使用天眼查数据源（或可设定为 all 组合多个数据源）

```
./enscan -n 小米 -type tyc
```

使用多数据源一起收集（暂不支持多渠道+筛选）

```
./enscan -n 小米 -type aqc,tyc
```

使用插件渠道

```
./enscan -n 小米 -type aqc,miit
```

**请设置请求延时，防止造成影响**

```
./enscan -n 小米 -delay 3
```

### Cookie配置

**AQC**

出现安全验证请使用获取cookie的浏览器过验证即可继续，默认查询为 aiqicha.baidu.com

Cookie信息请勿直接 `document.cookie`，可能因为http-only 选项无法复制全导致登陆失败

![image-20221028223835307](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20221028223835307.png)

**TYC tycid**

配置COOKIE后配置tycid

![image-20230722194839975](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20230722194839975.png)

其他Cookie请自行参考获取


### 选项说明

#### **field 获取字段**

使用参数 `field`指定需要查询的信息，可指定多参数一起查询，方便快速收集

```
-n 小米 -field icp,app
```

支持以下参数

- `icp` 网站备案信息
- `weibo` 微博
- `wechat` 微信公众号
- `app` 应用信息
- `job` 招聘信息
- `wx_app` 微信小程序
- `copyright` 软件著作权
- `supplier` 供应商信息（通过招标书确定）
- 其他（根据插件情况更新）

#### **type 获取字段**

使用参数 `type`可以指定需要API数据源

```
-n 小米 -type tyc
```
**查询数据源**

- `aqc`   爱企查
- `tyc`   天眼查
- `kc`    快查
- `all`   全部查询

**插件**

- `aldzs` 阿拉丁 （仅小程序）
- `coolapk` 酷安市场 （仅APP）
- `qimai` 七麦数据（仅APP）
- `miit`   HG-ha 的 ICP_Query  (ICP备案、APP、小程序、快应用) **非狼组维护，团队成员请使用内部版本**

#### 完整参数

*文档更新不及时，请以程序提示为准*

| 参数           | 样例           | 说明                                                         |
| -------------- | -------------- | ------------------------------------------------------------ |
| -n             | 小米           | 关键词                                                       |
| -i             | 29453261288626 | 公司PID（自动识别类型）                                      |
| -f             | file.txt       | 批量查询，文本按行分隔（可选PID模式）                        |
| -type          | aqc            | API类型                                                      |
| -o             |                | 结果输出的文件夹位置(可选)                                   |
| -is-merge      |                | 合并导出                                                     |
| -invest        |                | 投资比例                                                     |
| -field         | icp            | 获取字段信息                                                 |
| -deep          | 1              | 递归搜索n层公司，需搭配invest使用                            |
| -hold          |                | 是否查询控股公司（可能需要VIP账户）                          |
| -supplier      |                | 是否查询供应商信息                                           |
| -branch        |                | 查询分支机构（分公司）信息                                   |
| -is-branch     |                | 深度查询分支机构信息（数量巨大）                             |
| -api           |                | 是否API模式                                                  |
| -debug         |                | 是否显示debug详细信息                                        |
| -is-show       |                | 是否展示信息输出                                             |
| -is-group      |                | 查询关键词为集团                                             |
| -is-pid        |                | 批量查询文件是否为公司PID                                    |
| -delay         |                | 每个请求延迟（S）-1为随机延迟1-5S                            |
| -branch-filter |                | 提供一个正则表达式，名称匹配该正则的分支机构和子公司会被跳过 |
| -proxy         |                | 设置代理                                                     |
| -timeout       |                | 每个请求默认1（分钟）超时                                    |
| -no-merge      |                | 批量查询【取消】合并导出                                     |
| -v             |                | 版本信息                                                     |



### API模式

**api调用效果**

可使用 https://enscan.wgpsec.org/api/info 体验 (因被滥用下线)

🥹plat平台已停止维护，不要问了~

![image-20221028231744940](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20221028231744940.png)

![image-20221028231815437](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20221028231815437.png)

![image-20221028231831102](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20221028231831102.png)

![image-20221028232013627](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20221028232013627.png)

#### API说明

获取信息将实时查询展示，可与其他工具进行API联动，请注意**不要开放到公网**

**获取信息**

```
GET /api/info?search=小米&invest=100&branch=true
```

| 参数     | 参数                 | 说明                       |
| -------- | -------------------- | -------------------------- |
| name     | 文本                 | 完整公司名称（二选一）     |
| type     | 文本，与命令参数一致 | 数据源                     |
| field    | 文本，与命令参数一致 | 筛选指定信息               |
| depth    | 数字                 | 爬取几层公司 如 2 为孙公司 |
| invest   | 数字                 | 筛选投资比例               |
| holds    | true                 | 筛选控股公司               |
| supplier | true                 | 筛选供应商信息             |
| branch   | true                 | 筛选分支信息               |
| output   | true                 | 为true导出excel表格下载    |

#### 启动部署

**golang 版本依赖**

```
go >= 1.22.1
```

**API模式**

启动API模式将在31000端口监听，并启动api服务，可通过api服务进行调用读取数据

```
./enscan --api
```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.1.0] - 2024-12-20

**更新**  
- 增加分支机构和子公司名称过滤功能  
- 新增 miit 插件可自建实时查询，提供 ICP备案、APP、小程序等信息查询  
- 新增 kuaicha 数据源，提供企业信息、微信公众号、投资信息、招聘信息等查询  
- 重构部分代码以支持插件扩展  
- 优化数据处理和导出逻辑  
- 优化了 README 文档

#### [v1.0.2] - 2024-08-03

**更新**  
- 修复 AQC 查询经常触发验证问题  
- 修复自定义tls指纹ja3问题(应该不用挂burp了)

#### [v1.0.0] - 2024-05-21

**更新**  
- 重构查询代码，采用接口实现功能，方便接入新接口  
- 优化提示逻辑  
- 优化删除冗余代码，删除鸡肋的web功能，换成实时api功能方便接入其他工具  
- 增加意外退出保存功能  
- 增加单独信息实时保存功能 -n xxx -field icp -out-update icp.csv 将会实时写入该文件，可增加其他查询参数如投资占比等，但不会输出

#### [v0.0.18] - 2024-04-23

**更新**  
- 修复TYC验证码问题  
- 使用os库替换遗弃的io/ioutil  
- 更新交叉编译脚本  
- 更新安装使用说明

#### [v0.0.17] - 2024-04-14

**更新**  
- 修复AQC安全验证问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
