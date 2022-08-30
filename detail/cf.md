## cf <https://github.com/teamssix/cf>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-teamssix-orange)
![GitHub stars](https://img.shields.io/github/stars/teamssix/cf.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.3.5-red)
![Time](https://img.shields.io/badge/Join-20220829-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

CF 是一个云环境利用框架，主要用来方便红队人员在获得云服务的访问凭证即 Access Key 的后续工作。

CF 下载地址：[github.com/teamssix/cf/releases](https://github.com/teamssix/cf/releases)

CF 社区地址：[github.com/teamssix/cf/discussions](https://github.com/teamssix/cf/discussions)

![img](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202208251726676.png)

## 使用手册

使用手册请参见：[wiki.teamssix.com/cf](https://wiki.teamssix.com/cf)

[![img](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202207112152449.png)](https://wiki.teamssix.com/cf)

## 简单上手

![](https://cdn.jsdelivr.net/gh/teamssix/BlogImages/imgs/202207180028840.png)

配置 CF

```bash
cf configure
```

一键列出当前访问凭证的云服务资源

```bash
cf alibaba ls
```

一键列出当前访问凭证的权限

```bash
cf alibaba permissions
```

一键接管控制台

```bash
cf alibaba console
```

查看 CF 为实例执行命令的操作的帮助信息

```bash
cf alibaba ecs exec -h
```

一键为所有实例执行三要素，方便 HVV

```
cf alibaba ecs exec -b
```

一键获取实例中的临时访问凭证数据

```bash
cf alibaba ecs exec -m
```

一键查看 VPC 安全组规则

```bash
cf tencent vpc ls
```

如果感觉还不错的话，师傅记得给个 Star 呀 ~，另外 CF 的更多使用方法可以参见使用文档：[wiki.teamssix.com/cf](https://wiki.teamssix.com/cf)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
