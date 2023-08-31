## scaninfo <https://github.com/redtoolskobe/scaninfo>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-华东360安服团队-orange)
![GitHub stars](https://img.shields.io/github/stars/redtoolskobe/scaninfo.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1.0-red)
![Time](https://img.shields.io/badge/Join-20220316-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

开源、轻量、快速、跨平台 的红队内外网打点扫描器

## 注意的点

- 漏洞扫描的时候有时候最后几个任务会卡住，是因为ftp爆破模块，这个fscan也一样目前没有好的解决办法，后续更新.先阶段可以-eq 21跳过ftp，或者control+c 主动停止不影响结果保存。
- 有时候扫外网的全端口会漏掉端口可以使用-n 指定线程为500，400，默认为900.网络好的话900-1000都是没有问题
- 关于结果报告 xlsx 文件是当你control+c 主动停止或任务正常结束时才会写入。txt文件是实时写入。


## 项目说明

>  为何有这个项目

在渗透测试的端口扫描阶段，相信很多人遇到的问题是nmap太慢，masscan不准确。难以在速度与准确度之间寻找一个平衡。 其实有个工具不错就是[TXPortMap](https://github.com/4dogs-cn/TXPortMap)。但是没有进度条当大量扫描的时候结果处理也太友好。

在内网这块[fscan](https://github.com/shadow1ng/fscan)算是一款很优秀的工具但也有一些问题，如端口扫描不支持服务识别等。

指纹这块[EHole](https://github.com/EdgeSecurityTeam/EHole)也算一款很优秀的工具

## 如何解决这个问题

- scaninfo 专门解决上述问题并对上述项目代码进行了优化与重构，快速的端口扫描和服务识别比masscan更快。

- 包含fscan的绝大部份功能除了poc扫描和自定义字典

- 更好的web探测与指纹识别

- 更好的报告输出

## 使用说明

![image-20211105132301924](https://github.com/redtoolskobe/scaninfo/raw/main/infoscan.assets/image-20211105132301924.png)

> 常见的参数

```shell
scaninfo -uf  url.txt -m  webfinger  web指纹识别
```

```shell
scaninfo  -i  192.168.0.0/24  -p  1-65535  -eq 53  -m port 端口扫描
```

```shell
scaninfo  -i  192.168.0.0/24  -l ip.txt  -uf  url.txt -t1000   可以组合各种目标ip段ip文件url文件 
```

## 报告

> 报告主要是直观的excel并对每一种类型进行分类。同时也会生成txt json格式的结果。

![image-20211105134827966](https://github.com/redtoolskobe/scaninfo/raw/main/infoscan.assets/image-20211105134827966.png)

![image-20211105134954709](https://github.com/redtoolskobe/scaninfo/raw/main/infoscan.assets/image-20211105134954709.png)

## 参数

>  主要参数

| 参数  | 说明                             |
| ----- | -------------------------------- |
| -ei   | 排除某IP                         |
| -eq   | 排除某端口                       |
| -l    | 指定IP文件                       |
| -uf   | 指定要web指纹识别的url文件       |
| -ff   | 指定指纹文件默认使用内置         |
| -o    | 指定保存的结果文件默认为result   |
| -p    | 指定端口默认使用top100           |
| -m    | 指定扫描的模块默认为全部         |
| -pt   | 指定ping 探测存活的线程          |
| -vt   | 指定web指纹扫描的线程默认500     |
| -n    | 指定端口扫描的线程默认900        |
| -show | 查看扫描支持的模块               |
| -t    | 端口扫描tcp连接的超时时间默认0.5 |
| -np   | 跳过存活探测                     |

> 模块说明

| 模块      | 说明                                |
| --------- | ----------------------------------- |
| ftp       | ftp弱口令探测                       |
| ssh       | ssh弱口令探测                       |
| smb       | smb弱口令探测                       |
| mssql     | mssql弱口令探测                     |
| mysql     | mysql弱口令探测                     |
| mgo       | mongodb弱口令探测                   |
| redis     | redis弱口令探测                     |
| psql      | psql弱口令探测                      |
| ms17010   | ms17010探测                         |
| smbghost  | smbghost探测                        |
| webfinger | web指纹识别                         |
| netbios   | netbios探测，可以识别主机名发现域控 |
| findnet   | oxid                                |
| all       | 所有                                |
| port      | 端口扫描                            |
| ping      | ping 存活                           |
| mem       | memcached弱口令                     |


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
