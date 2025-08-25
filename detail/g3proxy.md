## g3proxy <https://github.com/bytedance/g3>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Rust-blue)
![Author](https://img.shields.io/badge/Author-bytedance-orange)
![GitHub stars](https://img.shields.io/github/stars/bytedance/g3.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.12.2-red)
![Time](https://img.shields.io/badge/Join-20250401-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

# G3 Project

[![minimum rustc: 1.86](https://img.shields.io/badge/minimum%20rustc-1.86-green?logo=rust)](https://www.whatrustisit.com)
[![License: Apache 2.0](https://img.shields.io/badge/license-Apache_2.0-blue.svg)](LICENSE)
[![codecov](https://codecov.io/gh/bytedance/g3/graph/badge.svg?token=TSQCA4ALQM)](https://codecov.io/gh/bytedance/g3)
[![docs](https://readthedocs.org/projects/g3-project/badge)](https://g3-project.readthedocs.io/)

## 关于

本项目用于构建面向企业的通用代理解决方案，包括但不限于代理、反向代理（开发中）、负载均衡（待定）、NAT穿透（待定）等。

## 应用程序

G3项目包含许多应用，每一个应用程序单独一个子目录，包含各自的代码、文档等。

除了应用程序目录，还有一些公共目录：

- [doc](https://github.com/bytedance/g3/blob/master/doc) 包含项目级别文档。
- [sphinx](https://github.com/bytedance/g3/blob/master/sphinx) 用于为各应用生成HTML参考文档。
- [scripts](https://github.com/bytedance/g3/blob/master/scripts) 包含各种辅助脚本，包括覆盖率测试、打包脚本等。

### g3proxy

通用正向代理解决方案，同时带有TCP映射、TLS卸载/封装、透明代理、简单反向代理等功能。

#### 主要特性

- Async Rust: 高效、稳定
- Http1 / Socks5 正向代理协议, SNI Proxy and TCP TPROXY
- 代理串联，动态下一级代理节点选择
- 丰富的出口路由选择方法，支持接入自定义选路Agent
- TCP/TLS反向代理，基础HTTP反向代理
- TLS支持OpenSSL / BoringSSL / AWS-LC / Tongsuo, 部分场景支持rustls
- TLS中间人劫持, 解密流量导出, HTTP1/HTTP2/IMAP/SMTP协议解析
- ICAP审计，支持HTTP1/HTTP2/IMAP/SMTP，无缝集成第三方安全审计/杀毒产品
- 优雅重载 & 热升级
- 灵活的负载均衡&容灾策略
- 用户认证，且支持丰富的配置选项
- 用户配置下可细化进行差异化站点配置
- 丰富的ACL/限流限速策略，包括入口/出口/用户维度
- 丰富的监控指标，包括入口/出口/用户/用户站点维度
- 多种日志 & 监控解决方案集成能力

详细功能介绍及用户指南请看 [g3proxy](https://github.com/bytedance/g3/blob/master/g3proxy/README.md)。

可在 [Read the Docs](https://g3-project.readthedocs.io/projects/g3proxy/en/latest/) 线上查看使用sphinx生成的g3proxy参考文档，
包括详细配置格式、日志格式、监控打点定义、协议定义等。

### g3tiles

通用反向代理解决方案，开发中。

可在 [Read the Docs](https://g3-project.readthedocs.io/projects/g3tiles/en/latest/) 线上查看使用sphinx生成的g3tiles参考文档，
包括详细配置格式、日志格式、监控打点定义等。

### g3bench

压测工具，支持 HTTP/1.x、HTTP/2、HTTP/3、TLS握手、DNS、Cloudflare Keyless 。

更多详情参考 [g3bench](https://github.com/bytedance/g3/blob/master/g3bench/README.md)。

### g3mkcert

用来生成 根CA / 中间CA / TLS服务端证书 / TLS客户端证书 的工具。

### g3fcgen

适用于g3proxy TLS劫持功能的伪造证书生成服务应用。

### g3iploc

适用于g3proxy GeoIP功能的IP Location查找服务应用。

### g3keymess

Cloudflare Keyless Server的简单实现。

## 支持平台

目前仅提供对Linux系统的完整支持，其他系统如FreeBSD、NetBSD、macOS、Windows可以编译，但是未测试过功能。

如果需要支持其他系统，欢迎提交PR。

## 开发环境搭建

参考 [Dev-Setup](https://github.com/bytedance/g3/blob/master/doc/dev-setup.md)。

## 标准及约定

参考 [Standards](https://github.com/bytedance/g3/blob/master/doc/standards.md)。

## 发布及打包

每个应用程序的每个发布版本都会有对应的tag，格式为 *\<name\>-v\<version\>* 。
使用对应的tag生成源码tar包，该tar包可以用于生成deb、rpm等发行版原生包文件。

如果需要对正式发布的版本打包:

1. 生成版本发布包

   ```shell
   ./scripts/release/build_tarball.sh <name>-v<version>
   ```

   所有引用第三方源码都会放在tar包的vendor目录下，打包时只需要在目标机器上安装好编译器及系统依赖库即可，无需额外的网络连接。

2. 打包指令

   deb包:
   ```shell
   tar xf <name>-<version>.tar.xz
   cd <name>-<version>
   ./build_deb_from_tar.sh
   ```

   rpm包:
   ```shell
   rpmbuild -ta ./<name>-<version>.tar.xz
   # 如果失败，可以手动执行以下指令：
   tar xvf <name>-<version>.tar.xz ./<name>-<version>/<name>.spec
   cp <name>-<version>.tar.xz ~/rpmbuild/SOURCES/
   rpmbuild -ba ./<name>-<version>/<name>.spec
   ```

如果需要直接从git打包:

- deb包:

  ```shell
  ./build_deb_from_git.sh <name>
  ```

- rpm包:

  ```shell
  ./build_rpm_from_git.sh <name>
  ```

### 预构建安装包

如需在生产环境使用，建议自行打包。

测试环境的话，部分包已经编译上传到
[cloudsmith](https://cloudsmith.io/~g3-oqh/repos/), 可参考该链接页面的说明进行安装。

### 制作Docker镜像

每个应用的*docker*文件夹下有可参考的Dockerfile(s)，命令如下：

```shell
# 在源码根目录可执行
docker build -f <app>/docker/debian.Dockerfile . -t <app>:<tag>
# 本地没有源码时，可用远程URL执行
docker build -f <app>/docker/debian.Dockerfile github.com/bytedance/g3 -t <app>:<tag>
# 如果已经制作了源码tar包，也可以把URL路径换成源码tar包路径
```

### 静态链接

参考 [Static Linking](https://github.com/bytedance/g3/blob/master/doc/static-linking.md)。

### 使用OpenSSL变种编译

参考 [OpenSSL Variants](https://github.com/bytedance/g3/blob/master/doc/openssl-variants.md)。

### 长期支持版本

参考 [Long-Term Support](https://github.com/bytedance/g3/blob/master/doc/long-term_support.md).

## 贡献指南

参考 [Contributing](https://github.com/bytedance/g3/blob/master/CONTRIBUTING.md)。



<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.12.2] - 2025-08-20

This is a minor for v1.12 LTS branch:
support to build rpm package on OpenSUSE
Prebuilt rpm and deb packages can be found at cloudsmith.

#### [v1.10.7] - 2025-07-22

**修复**  
- 修复检测 DNS over TLS 流量时的崩溃  
- 修复 c-ares 解析器中的默认最小 ttl 值

#### [v1.10.6] - 2025-06-26

**修复**  
- 修复 H2 零大小主体帧的读取  
- 修复 HTTP 1 OPTIONS 头行格式  
- 修复发送给客户端的 h2 最大并发流设置  
- 修复 h2 连接级别 IDLE 检查  
- 使用更合理的 h2 默认设置值

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
