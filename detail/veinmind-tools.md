## veinmind-tools <https://github.com/chaitin/veinmind-tools>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang/Python-blue)
![Author](https://img.shields.io/badge/Author-长亭科技-orange)
![GitHub stars](https://img.shields.io/github/stars/chaitin/veinmind-tools.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1.5-red)
![Time](https://img.shields.io/badge/Join-20220316-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

veinmind-tools 是由长亭科技自研，牧云团队孵化，基于 <a href="https://github.com/chaitin/libveinmind">veinmind-sdk</a> 打造的容器安全工具集

veinmind, 中文名为<b>问脉</b>，寓意 <b>容器安全见筋脉，望闻问切治病害。</b> 旨在成为云原生领域的一剂良方


中文文档 | <a href="README.en.md">English</a>

## 🔥 Demo
![](https://veinmind-cache.oss-cn-hangzhou.aliyuncs.com/img/scan.gif)

问脉已接入 openai, 可以使用 openai 对扫描的结果进行人性化分析，让您更加清晰的了解本次扫描发现了哪些风险。

![](https://veinmind-cache.oss-cn-hangzhou.aliyuncs.com/img/ai.png)

## 🕹️ 快速开始
### 1. 确保机器上正确安装 docker
```
docker info
```
### 2. 安装 [veinmind-runner](https://github.com/chaitin/veinmind-tools/tree/master/veinmind-runner) 镜像
```
docker pull registry.veinmind.tech/veinmind/veinmind-runner:latest
```
### 3. 下载 [veinmind-runner](https://github.com/chaitin/veinmind-tools/tree/master/veinmind-runner) 平行容器启动脚本
```
wget -q https://download.veinmind.tech/scripts/veinmind-runner-parallel-container-run.sh -O run.sh && chmod +x run.sh
```
### 4. 快速扫描本地镜像/容器
```
./run.sh scan [image/container]
```
### 5. 使用 openAI 智能分析
```
./run.sh scan [image/container] --enable-analyze --openai-token  <your_openai_token>
```
> 注: 使用 openAI 时，请确保当前网络能够访问openAI
> 平行容器启动时，需要手动通过 docker run -e http_proxy=xxxx -e https_proxy=xxxx 设置代理（非全局代理的场景下）

## 🔨 工具列表

| 工具                                                                        | 功能                | 
|---------------------------------------------------------------------------|-------------------|
| [veinmind-runner](https://github.com/chaitin/veinmind-tools/blob/master/veinmind-runner/README.md)                              | 扫描工具运行宿主          |
| [veinmind-malicious]https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-malicious)                       | 扫描容器/镜像中的恶意文件     |
| [veinmind-weakpass](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-weakpass)                         | 扫描容器/镜像中的弱口令      |
| [veinmind-log4j2](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-log4j2)                             | 扫描容器/镜像中的log4j2漏洞 |
| [veinmind-minio](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-minio)                               | 扫描容器/镜像中的minio漏洞  |
| [veinmind-sensitive](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-sensitive)                       | 扫描镜像中的敏感信息        |
| [veinmind-backdoor](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-backdoor)                         | 扫描镜像中的后门          |
| [veinmind-history](https://github.com/chaitin/veinmind-tools/blob/master/plugins/python/veinmind-history)                       | 扫描镜像中的异常历史命令      |
| [veinmind-vuln](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-vuln)                                 | 扫描容器/镜像中的资产信息和漏洞  |
| [veinmind-webshell](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-webshell)                         | 扫描镜像中的 Webshell   |
| [veinmind-unsafe-mount](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-unsafe-mount)                 | 扫描容器中的不安全挂载目录     |
| [veinmind-iac](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-iac)                                   | 扫描镜像/集群的IaC文件     |
| [veinmind-escape](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-escape)                             | 扫描容器/镜像中的逃逸风险     |
| [veinmind-privilege-escalation](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-privilege-escalation) | 扫描容器/镜像中的提权风险     |
| [veinmind-trace](https://github.com/chaitin/veinmind-tools/blob/master/plugins/go/veinmind-trace)                               | 扫描容器中的入侵痕迹        |

PS: 目前所有工具均已支持平行容器的方式运行

## 🧑‍💻 编写插件

可以通过 example 快速创建一个 veinmind-tools 插件, 具体查看 [veinmind-example](https://github.com/chaitin/veinmind-tools/blob/master/example)  

## ☁️ 云原生设施兼容性
| 名称                                                          | 类别    | 是否兼容 |
|-------------------------------------------------------------|-------|------|
| [Jenkins](https://github.com/chaitin/veinmind-jenkins)      | CI/CD | ✔️   |
| [Gitlab CI](https://veinmind.chaitin.com/docs/ci/gitlab/)   | CI/CD | ✔️   |
| [Github Action](https://github.com/chaitin/veinmind-action) | CI/CD | ✔️   |
| DockerHub                                                   | 镜像仓库  | ✔️   |
| Docker Registry                                             | 镜像仓库  | ✔️   |
| Harbor                                                      | 镜像仓库  | ✔️   |
| Docker                                                      | 容器运行时 | ✔️   |
| Containerd                                                  | 容器运行时 | ✔️   |
| Kubernetes                                                  | 集群    | ✔️   |

## 🛴 工作原理
![](https://github.com/chaitin/veinmind-tools/raw/master/docs/architecture.png)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v2.1.5] - 2023-07-26

**新增**  
- 新增 veinmind-trace 插件检查容器的攻击痕迹  
- 使用 golang 重构 veinmind-backdoor 插件  
- veinmind-backdoor 插件增加 rootkit 扫描  

**其他**  
- 更新 libveinmind 至 1.9.42 版本

#### [v2.1.4] - 2023-07-04

**新增**  
- 添加 veinmind-privilege-escalation 插件，用于检测权限升级风险(包括suid/sudo)  

**修复**  
- 修复libveinmind步行数据竞争错误  
- veinmind-weakpass 添加错误检查  
- 修复文档中有关如何初始化插件的描述错误  
- 修复 README 格式  

**其他**  
- libveinmind 更新至 1.9.21  
- CI 添加自动同步到 harbor

#### [v2.1.3] - 2023-05-23

**新增**  
- 新增 mysql5 弱口令扫描  
- 使用 bullseye 和 libveinmind-dev 更新至 1.9.15   
- 新增 caching_sha2_password 插件  
- 新增 kubernetes iac 策略插件  
- 新增对 env/docker 历史命令扫描  

**修复**  
- 修复 libveinmind 遍历数据竞争的问题  
- 优化 veinmind-malicious 代码  
- 修复 mysql8 弱口令检查

#### [v2.1.2] - 2023-04-25

**新增**  
- veinmind-weakpass 添加支持 ftp  
- veinmind-iac 添加 dockerfile 安全检测  

**修复**  
- AI模块忽略基本分析内容  
- makefile 添加 CGO_ENBALED 参数和依赖更新  
- 优化 CI/CD 的代理设置

#### [v2.1.0] - 2023-03-27

**更新**  
- 支持使用 openai 分析扫描结果

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
