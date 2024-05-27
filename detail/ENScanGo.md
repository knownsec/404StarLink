## ENScanGo <https://github.com/wgpsec/ENScan_GO>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-wgpsec-orange)
![GitHub stars](https://img.shields.io/github/stars/wgpsec/ENScan_GO.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)
![Time](https://img.shields.io/badge/Join-20221117-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

剑指HW/SRC，解决在HW/SRC场景下遇到的各种针对国内企业信息收集难题

## 功能列表
![ENScanGo](https://github.com/wgpsec/ENScan_GO/raw/master/README/ENScanGo.png)

 - 使用支持以下API，并支持合并数据导出
    - 爱企查 (未登陆信息带*)
    - 天眼查
    - 阿拉丁 （数据反馈比较老旧暂时下线）
    - 酷安市场
    - 七麦数据
 - 查询信息
    - ICP备案
    - APP
    - 微博
    - 微信公众号
    - 控股公司
    - 供应商
    - 客户信息
    - 小程序
    - 控股X的公司的以上所有信息
    - ...
 - 通过APK市场收集使用信息



## 使用指南
### 第一次使用
前往[RELEASE](https://github.com/wgpsec/ENScan_GO/releases)下载编译好的文件使用

初次使用时需要使用 -v 命令生成配置文件信息
```
./enscan -v
```

**遇到问题请加上参数 --debug 提issue**

如果查询不出来目标网站信息，可以都挂上BURP代理进行查询

**自行编译请使用 go 编译命令，或使用编译脚本 build.sh**

### 登陆配置

**AQC**

出现安全验证请勿结束进程，请使用带cookie的浏览器过验证即可继续

请注意获取COOKIE域名，默认查询为aiqicha.baidu.com，请勿使用 aiqicha.com

Cookie信息请勿直接 `document.cookie`，可能因为http-only 选项无法复制全导致登陆失败

![image-20221028223835307](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20221028223835307.png)

**TYC tycid**

配置COOKIE后配置tycid

![image-20230722194839975](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20230722194839975.png)

### 快速使用

**默认公司信息** (网站备案, 微博, 微信公众号, app)

```
./enscan -n 小米
```

**对外投资占股100%的公司 获取孙公司（深度2）**

```
./enscan -n 小米 -invest 100 -deep 2
```

**组合筛选** 

大于51%控股公司、供应商、分支机构，只要ICP备案信息，并且批量获取邮箱信息

```
./enscan -n 小米 -field icp --hold --supplier --branch --email 
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

#### **type 获取字段**

使用参数 `type`可以指定需要API数据源

```
-n 小米 -type tyc
```

- `aqc`   爱企查
- `tyc`   天眼查
- `all`   全部查询
- `aldzs` 阿拉丁 （仅小程序）
- `coolapk` 酷安市场 （仅APP）
- `qimai` 七麦数据（仅APP）
- `chinaz` 站长之家（仅ICP备案）

#### 完整参数

| 参数              | 样例           | 说明                                   |
| ----------------- | -------------- | -------------------------------------- |
| -n                | 小米           | 关键词                                 |
| -i                | 29453261288626 | 公司PID（自动识别类型）                |
| -f                | file.txt       | 批量查询，文本按行分隔（可选PID模式）  |
| -type             | aqc            | API类型                                |
| -o                |                | 结果输出的文件夹位置(可选)             |
| -is-merge         |                | 合并导出                               |
| -invest           |                | 投资比例                               |
| -field            | icp            | 获取字段信息                           |
| -deep             | 1              | 递归搜索n层公司                        |
| -hold             |                | 是否查询控股公司                       |
| -supplier         |                | 是否查询供应商信息                     |
| -branch           |                | 查询分支机构（分公司）信息             |
| -is-branch        |                | 深度查询分支机构信息（数量巨大）       |
| -api              |                | 是否API模式                            |
| -debug            |                | 是否显示debug详细信息                  |
| -is-show          |                | 是否展示信息输出                       |
| -is-group         |                | 查询关键词为集团                       |
| -is-pid           |                | 批量查询文件是否为公司PID              |
| -delay            |                | 每个请求延迟（S）-1为随机延迟1-5S      |
| -proxy            |                | 设置代理                               |
| -timeout          |                | 每个请求默认1（分钟）超时              |
| -no-merge         |                | 批量查询【取消】合并导出               |
| -v                |                | 版本信息                               |
### API模式


**api调用效果（前端开发中）**

可使用 https://enscan.wgpsec.org/api/info 体验 (因被滥用下线)

![image-20221028231744940](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20221028231744940.png)

![image-20221028231815437](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20221028231815437.png)

![image-20221028231831102](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20221028231831102.png)

![image-20221028232013627](https://github.com/wgpsec/ENScan_GO/raw/master/README/image-20221028232013627.png)

#### API说明

获取信息将实时查询展示，可与其他工具进行API联动

**获取信息**

```
GET /api/info?search=小米&invest=100&branch=true
```

| 参数     | 参数                 | 说明                       |
| ------ | -------------------- | -------------------------- |
| name   | 文本                 | 完整公司名称（二选一）     |
| type   | 文本，与命令参数一致 | 数据源                     |
| field  | 文本，与命令参数一致 | 筛选指定信息               |
| depth  | 数字                 | 爬取几层公司 如 2 为孙公司 |
| invest | 数字                 | 筛选投资比例               |
| holds  | true                 | 筛选控股公司               |
| supplier | true                 | 筛选供应商信息             |
| branch | true                 | 筛选分支信息               |
| output | true                 | 为true导出excel表格        |


#### 启动部署

**golang 版本依赖**
```
go >= 1.22.1
```


**API模式**

启动API模式将在配置端口监听，并启动api服务，可通过api服务进行调用读取数据

```
./enscan --api
```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

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

#### [v0.0.16] - 2024-01-16

**更新**  
- 增加轻量web模式 --web 模式即可启动默认端口为3000  
- 访问 /api/info 即可搜索，无需配置数据库

#### [v0.0.15] - 2023-08-16

**更新**  
- 修复AQC查询问题  
- 当ENSCAN无法正常访问网站可尝试使用-proxy参数挂上代理

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
