## cf <https://github.com/teamssix/cf>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-teamssix-orange)
![GitHub stars](https://img.shields.io/github/stars/teamssix/cf.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.4.4-red)
![Time](https://img.shields.io/badge/Join-20220829-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

CF 是一个云环境利用框架，适用于在红队场景中对云上内网进行横向、SRC 场景中对 Access Key 即访问凭证的影响程度进行判定、企业场景中对自己的云上资产进行自检等等。

CF 下载地址：[github.com/teamssix/cf/releases](https://github.com/teamssix/cf/releases)

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202212132148217.png)

当前已支持的云：

- [x] 阿里云
- [x] 腾讯云
- [x] AWS
- [x] 华为云

## 使用手册

使用手册请参见：[wiki.teamssix.com/cf](https://wiki.teamssix.com/cf)

[![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202210121147330.png)](https://wiki.teamssix.com/cf)

## 安装

直接在 CF 下载地址：[github.com/teamssix/cf/releases](https://github.com/teamssix/cf/releases) 中下载系统对应的压缩文件，解压后在命令行中运行即可，目前支持以下系统：

|            文件名            |  系统   |                架构                | 位数 |
| :--------------------------: | :-----: | :--------------------------------: | :--: |
| cf_x.x.x_darwin_amd64.tar.gz |  MacOS  |   AMD（适用于 Intel 芯片的 Mac）   |  64  |
| cf_x.x.x_darwin_arm64.tar.gz |  MacOS  | ARM（适用于苹果 M 系列芯片的 Mac） |  64  |
|  cf_x.x.x_linux_386.tar.gz   |  Linux  |                AMD                 |  32  |
| cf_x.x.x_linux_amd64.tar.gz  |  Linux  |                AMD                 |  64  |
| cf_x.x.x_linux_arm64.tar.gz  |  Linux  |                ARM                 |  64  |
|   cf_x.x.x_windows_386.zip   | Windows |                AMD                 |  32  |
|  cf_x.x.x_windows_amd64.zip  | Windows |                AMD                 |  64  |
|  cf_x.x.x_windows_arm64.zip  | Windows |                ARM                 |  64  |

## 使用案例

|                标题                | 所使用的 CF 版本 |                           文章地址                           |   作者   |  发布时间  |
| :--------------------------------: | :--------------: | :----------------------------------------------------------: | :------: | :--------: |
|    《一次简单的"云"上野战记录》    |      v0.4.2      | [https://mp.weixin.qq.com/s/wi8C...](https://mp.weixin.qq.com/s/wi8CoNwdpfJa6eMP4t1PCQ) | carrypan | 2022.10.19 |
| 《记录一次平平无奇的云上攻防过程》 |      v0.4.0      | [https://zone.huoxian.cn/d/2557](https://zone.huoxian.cn/d/2557) | TeamsSix | 2022.9.14  |
|   《我用 CF 打穿了他的云上内网》   |      v0.2.4      | [https://zone.huoxian.cn/d/1341-cf](https://zone.huoxian.cn/d/1341-cf) | TeamsSix | 2022.7.13  |

## 简单上手

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202210121148379.png)

> 这里以阿里云为例，其他更多操作可以查看上面的使用手册。

配置访问配置

```bash
cf config
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202209071737407.png)

一键列出当前访问凭证的权限

```bash
cf alibaba perm
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202209071737408.png)

一键接管控制台

```bash
cf alibaba console
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202209071737409.png)

一键列出当前访问凭证的云服务资源

```bash
cf alibaba ls
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202209071737410.png)

查看 CF 为实例执行命令的操作的帮助信息

```bash
cf alibaba ecs exec -h
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202210121148805.png)

一键为所有实例执行三要素，方便 HVV

```bash
cf alibaba ecs exec -b
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202209071737412.png)

一键获取实例中的临时访问凭证数据

```bash
cf alibaba ecs exec -m
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202209071737413.png)

一键下载 OSS 对象存储数据

```bash
cf alibaba oss obj get
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202209071737414.png)

一键升级 CF 版本

```bash
cf upgrade
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202209071737416.png)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v0.4.4] - 2022-12-14

**新增功能**  
- 增加本地访问密钥扫描功能  
- 增加 huawei obs ls 功能  

**功能优化**  
- 优化错误信息输出  

**Bug 修复**  
- 修复一处 aws ec2 ls 处的 Bug  
- 修复一处配置功能处的 Bug

#### [v0.4.3] - 2022-12-04

**新增功能**  
- 在配置访问密钥时，会自动识别并提示导入本地的访问密钥  
- 增加 aws ec2 实例的列出功能  

**功能优化**  
- 优化输出信息的展示  
- 优化 config 命令功能  

**Bug 修复**  
- 修复一处删除配置时的 Bug

#### [v0.4.2] - 2022-10-11

**新增功能**  
- 增加 aws s3 列出功能  
- 增加阿里云 oss 指定 Bucket 的功能  
- 增加阿里云 ecs exec 指定区域的功能  

**功能优化**  
- 优化权限获取功能  
- 优化程序提示信息  
- 优化配置 AK 的逻辑  
- 增强阿里云 ecs 列出功能  

**Bug 修复**  
- 修复一处由于历史代码造成的 Bug  
- 修复一处配置 AK 时的 Bug

#### [v0.4.1] - 2022-09-20

**新增功能**  
- 增加对象列表导出功能  
- 增加指定查询对象列表数量功能  

**功能优化**  
- 优化接管控制台输出信息

#### [v0.4.0] - 2022-09-07

**新增功能**  
- 增加对已有的访问凭证修改功能  
- 增加控制台接管历史记录查看功能  
- 增加接管控制台指定用户名功能  

**功能优化**  
- 优化阿里云 OSS 相关功能  
- 全面优化配置访问凭证功能  
- 全面优化程序缓存功能

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
