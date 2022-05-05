## veinmind-tools <https://github.com/chaitin/veinmind-tools>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang/Python-blue)
![Author](https://img.shields.io/badge/Author-长亭科技-orange)
![GitHub stars](https://img.shields.io/github/stars/chaitin/veinmind-tools.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.2.2-red)
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
|  [veinmind-malicious](https://github.com/chaitin/veinmind-tools/tree/master/veinmind-malicious) | 扫描镜像中的恶意文件  |
|  [veinmind-weakpass](https://github.com/chaitin/veinmind-tools/tree/master/veinmind-weakpass)  | 扫描镜像中的弱口令  |
|  [veinmind-sensitive](https://github.com/chaitin/veinmind-tools/tree/master/veinmind-sensitive) | 扫描镜像中的敏感信息  |
|  [veinmind-backdoor](https://github.com/chaitin/veinmind-tools/tree/master/veinmind-backdoor) | 扫描镜像中的后门 |
|  [veinmind-history](https://github.com/chaitin/veinmind-tools/tree/master/veinmind-history) | 扫描镜像中的异常历史命令 |
    
PS: 目前所有工具均已支持平行容器的方式运行


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.2.2] - 2022-04-26

**更新**  
- 优化 veinmind-runner 处理逻辑  
- 支持指定 veinmind-runner 的 exit-code

#### [v1.2.0] - 2022-04-08

**更新**  
- 所有插件支持基于问脉 SDK 提供的插件系统运行  
- 基于问脉 SDK 编写了事件上报机制，所有插件使用同一 Service 进行事件上报  
- 宿主程序 veinmind-runner 支持扫描远程仓库镜像  
- 宿主程序 veinmind-runner 支持以平行容器模式启动，平行容器内置除 veinmind-malicious 之外的工具  


#### [v1.1.2] - 2022-03-25

**更新**  
- veinmind-sensitive 增加部分规则  
- 所有工具增加平行容器脚本，支持一键运行  


#### [v1.1.0] - 2022-03-18

**更新**  
- 所有工具支持以平行容器模式运行

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
