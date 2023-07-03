## cf <https://github.com/teamssix/cf>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-teamssix-orange)
![GitHub stars](https://img.shields.io/github/stars/teamssix/cf.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.5.0-red)
![Time](https://img.shields.io/badge/Join-20220829-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

CF 是一个云环境利用框架，适用于在红队场景中对云上内网进行横向、SRC 场景中对 Access Key 即访问凭证的影响程度进行判定、企业场景中对自己的云上资产进行自检等等。

<details> <summary>CF 命令使用大全</summary><br>

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202307010038925.png)

</details>

当前已支持的云：

- [x] 阿里云
- [x] 腾讯云
- [x] AWS
- [x] 华为云

## 使用手册

使用手册请参见：[wiki.teamssix.com/cf](https://wiki.teamssix.com/cf)

[![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202210121147330.png)](https://wiki.teamssix.com/cf)

## 安装

### HomeBrew 安装

```bash
brew tap teamssix/tap
brew install teamssix/tap/cf
```

### 下载二进制包

直接在 CF 下载地址：[github.com/teamssix/cf/releases](https://github.com/teamssix/cf/releases) 中下载系统对应的压缩文件，解压后在命令行中运行即可。

<details> <summary>目前支持的系统</summary><br>

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

</details>

## 使用案例

|                标题                | 所使用的 CF 版本 |                           文章地址                           |   作者   |  发布时间  |
| :--------------------------------: | :--------------: | :----------------------------------------------------------: | :------: | :--------: |
|    《CF 云环境利用框架最佳实践》    |      v0.4.5      | [wiki.teamssix.com/cf/cases/cf_best_practices](https://wiki.teamssix.com/cf/cases/cf_best_practices.html) | TeamsSix | 2023.6.4 |
|    《记一次打穿云上内网的攻防实战》    |      v0.4.5      | [zone.huoxian.cn/d/2766](https://zone.huoxian.cn/d/2766) | Walker 沃克 | 2023.5.21 |
|    《一次简单的"云"上野战记录》    |      v0.4.2      | [mp.weixin.qq.com/s/wi8CoNwdpfJa6eMP4t1PCQ](https://mp.weixin.qq.com/s/wi8CoNwdpfJa6eMP4t1PCQ) | carrypan | 2022.10.19 |
| 《记录一次平平无奇的云上攻防过程》 |      v0.4.0      | [zone.huoxian.cn/d/2557](https://zone.huoxian.cn/d/2557) | TeamsSix | 2022.9.14  |
|   《我用 CF 打穿了他的云上内网》   |      v0.2.4      | [zone.huoxian.cn/d/1341-cf](https://zone.huoxian.cn/d/1341-cf) | TeamsSix | 2022.7.13  |

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

一键创建 RDS 账号

```bash
cf alibaba rds account
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202307010033313.png)

一键升级 CF 版本

```bash
cf upgrade
```

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202209071737416.png)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v0.5.0] - 2023-07-01

**新增功能**  
- 新增阿里云用户数据后门功能  
- 新增阿里云镜像共享功能  
- 新增阿里云接管控制台时自动创建 AK 功能  
- 新增阿里云 RDS 列出详细信息功能  
- 新增阿里云 RDS 添加账号功能  
- 新增阿里云 RDS 创建公网访问地址的功能  
- 新增阿里云 RDS 添加白名单的功能  
- 新增查询 AK 所属云厂商功能  
- 新增支持 brew 安装  

**功能优化**  
- 优化配置功能，现在能自动识别配置是否处于可用状态  
- 优化实例公网 IP 展示，不存在时会展示为空  
- 优化 OSS 下载功能，现在默认会下载所有文件  
- 优化更新处理逻辑  
- 优化华为云 OBS 列出功能  

**Bug 修复**  
- 修复批量执行命令时，没有安装云助手导致批量执行中断的 Bug  
- 修复 OSS 下载文件无法自动创建目录的 Bug

#### [v0.4.5] - 2023-04-29

**新增功能**  
- 增加华为云控制台接管和权限枚举功能  

**功能优化**  
- 优化错误信息输出  
- 优化更新功能

**Bug 修复**  
- 修复配置令牌功能的 Bug  
- 修复两处缓存功能的 Bug  
- 修复更新功能 Bug  
- 修复腾讯云 cvm 和 lh 无法列全的 Bug

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

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
