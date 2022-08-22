## veinmind-tools <https://github.com/chaitin/veinmind-tools>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang/Python-blue)
![Author](https://img.shields.io/badge/Author-长亭科技-orange)
![GitHub stars](https://img.shields.io/github/stars/chaitin/veinmind-tools.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.0-red)
![Time](https://img.shields.io/badge/Join-20220316-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

veinmind-tools 是由长亭科技自研，基于<a href="https://github.com/chaitin/libveinmind">veinmind-sdk</a>打造的容器安全工具集


## 🔥 Demo
![](https://dinfinite.oss-cn-beijing.aliyuncs.com/image/20220415144819.gif)


## 🕹️ 快速开始
### 1. 确保机器上正确安装 docker
```
docker info
```
### 2. 安装 [veinmind-runner](https://github.com/chaitin/veinmind-tools/tree/master/veinmind-runner) 镜像
```
docker pull veinmind/veinmind-runner:latest
```
### 3. 下载 [veinmind-runner](https://github.com/chaitin/veinmind-tools/tree/master/veinmind-runner) 平行容器启动脚本
```
wget -q https://download.veinmind.tech/scripts/veinmind-runner-parallel-container-run.sh -O run.sh && chmod +x run.sh
```
### 4. 快速扫描本地镜像
```
./run.sh scan-host
```


## 🔨 工具列表

|  工具 | 功能  | 
|---|---|
|  [veinmind-runner](https://github.com/chaitin/veinmind-tools/tree/master/veinmind-runner) | 扫描工具运行宿主 |
|  [veinmind-malicious](https://github.com/chaitin/veinmind-tools/tree/master/plugins/go/veinmind-malicious) | 扫描镜像中的恶意文件  |
|  [veinmind-weakpass](https://github.com/chaitin/veinmind-tools/tree/master/plugins/go/veinmind-weakpass)  | 扫描镜像中的弱口令  |
|  [veinmind-sensitive](https://github.com/chaitin/veinmind-tools/tree/master/plugins/python/veinmind-sensitive) | 扫描镜像中的敏感信息  |
|  [veinmind-backdoor](https://github.com/chaitin/veinmind-tools/tree/master/plugins/python/veinmind-backdoor) | 扫描镜像中的后门 |
|  [veinmind-history](https://github.com/chaitin/veinmind-tools/tree/master/plugins/python/veinmind-history) | 扫描镜像中的异常历史命令 |
|  [veinmind-asset](https://github.com/chaitin/veinmind-tools/tree/master/plugins/go/veinmind-asset) | 扫描镜像中的资产信息 |
    
PS: 目前所有工具均已支持平行容器的方式运行



<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.5.0] - 2022-08-19

**更新**  
- 新增 veinmind-webshell 检测插件

#### [v1.4.2] - 2022-08-12

**更新**  
- 支持插件依赖服务管理机制  
- veinmind-runner 镜像支持使用 veinmind-malicious 扫描恶意文件

#### [v1.4.0] - 2022-07-15

**更新**  
- 更新 veinmind-asset 依赖  
- 修复 veinmind-asset 文件处理 bug  
- 提高 veimind-asset 运行速度  
- 支持使用 helm 安装并部署 veinmind-runner  
- veinmind-runner 支持镜像阻断功能

#### [v1.3.5] - 2022-07-07

**更新**  
- 修复远程仓库扫描未解析 tag 的问题  
- 支持英文文档

#### [v1.3.3] - 2022-06-21

**Feature**  
- 适配 harbor 镜像扫描  
- 弱口令扫描增加单元测试  

**Bug**  
- 修复弱口令扫描无镜像 ID 问题  
- 修复敏感信息扫描文件读取问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
