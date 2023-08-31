## MDUT <https://github.com/SafeGroceryStore/MDUT>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-Ch1ngg-orange)
![GitHub stars](https://img.shields.io/github/stars/SafeGroceryStore/MDUT.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1.1-red)
![Time](https://img.shields.io/badge/Join-20210702-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


MDUT 全称 Multiple Database Utilization Tools，是一款中文的数据库跨平台利用工具，集合了多种主流的数据库类型。基于前人 SQLTOOLS 的基础开发了这套程序(向 SQLTOOLS 致敬)，旨在将常见的数据库利用手段集合在一个程序中，打破各种数据库利用工具需要各种环境导致使用相当不便的隔阂。此外工具以 JAVAFx 作为 GUI 操作界面，界面美观。同时程序还支持多数据库同时操作，每种数据库都相互独立，极大方便了网络安全工作者的使用。

## 截图
![image.png](https://i.loli.net/2021/05/11/c1M6YqZNAOnjmfp.png)

## 目录结构
```
.
├── CHANGELOG.md
├── MDAT-DEV // MDUT 源码
├── MDUTSqlKit
│   └── MDATKit.zip // CLR 源码
├── README.md
├── README_ZH.md
├── redis-cus-rogue.py // Redis 主从脚本
├── ShellUtil.java // Oracle JAVA 脚本
└── FileUtil.java  // Oracle JAVA 脚本

```

## TODO
1. HTTP Tunnel

## 致谢
[j1anFen](https://jianfensec.com/) / [冰蝎](https://github.com/rebeyond/Behinder) / [ODAT](https://github.com/quentinhardy/odat) / [MSDAT](https://github.com/quentinhardy/msdat) / SQLTOOLS - 深度撞击
 / [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings) / [WarSQLKit](https://github.com/mindspoof/MSSQL-Fileless-Rootkit-WarSQLKit)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v2.1.1] - 2022-06-22

**核心**  
- 优化逻辑代码  
- 更改用户协议窗口  
- 重构 Http Tunnel 生成界面  

**Mysql**  
- 修正 Mysql 某些时候错误不弹窗  

**Mssql**  
- 将依赖包重新替换为 jTDS (Microsoft 官方驱动太多问题)  

**Oracle**  
- 增加oracle 单独上传功能  

**Redis**  
- 优化内部代码  
- 再次修复 Redis 测试连接错误信息返回连接成功 Bug  
- 增加反弹shell功能 (不推荐使用影响生产环境)  
- 修复 Redis 某些时候错误不弹窗  
- 增强 替换 SSH 公钥 功能

#### [v2.1.0] - 2022-05-24

**核心**  
- 增加 HTTP 隧道功能(Redis暂不支持)  
- 优化逻辑代码  
- 加长默认超时时间  

**Mssql**  
- 修复下载文件 Bug  
- 删除获取管理员密码功能  
- 增加一键恢复所有组件功能   
- 修正 CLR Hex String  

**Oracle**  
- 更改 JAVA Util 导入方式  
- 优化 JAVA ShellUtil 代码  

**Redis**  
- 添加 slave-read-only 功能

#### [v2.0.8] - 2021-12-01

**核心**  
- 修复 Mssql 连接 2000 时候的语句兼容性问题  
- 设置程序默认编码  
- 删除敏感文件(详细说明情况请看文档里的公告一栏)

#### [v2.0.6] - 2021-08-17

**核心**  
- 优化内部代码  
- 删除软件自启更新功能  
- 优化更新功能界面，增加在线下载更新功能(Github Api)  
- 后续不再强制要求先下载 v2.0 版，下载即用

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
