## ServerScan <https://github.com/Adminisme/ServerScan>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-Adminisme-orange)
![GitHub stars](https://img.shields.io/github/stars/Adminisme/ServerScan.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.2-red)
![Time](https://img.shields.io/badge/Join-20210223-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


```shell
███████╗███████╗██████╗ ██╗   ██╗███████╗██████╗     ███████╗ ██████╗ █████╗ ███╗   ██╗
██╔════╝██╔════╝██╔══██╗██║   ██║██╔════╝██╔══██╗    ██╔════╝██╔════╝██╔══██╗████╗  ██║
███████╗█████╗  ██████╔╝██║   ██║█████╗  ██████╔╝    ███████╗██║     ███████║██╔██╗ ██║
╚════██║██╔══╝  ██╔══██╗╚██╗ ██╔╝██╔══╝  ██╔══██╗    ╚════██║██║     ██╔══██║██║╚██╗██║
███████║███████╗██║  ██║ ╚████╔╝ ███████╗██║  ██║    ███████║╚██████╗██║  ██║██║ ╚████║
╚══════╝╚══════╝╚═╝  ╚═╝  ╚═══╝  ╚══════╝╚═╝  ╚═╝    ╚══════╝ ╚═════╝╚═╝  ╚═╝╚═╝  ╚═══╝
                                                                                By:Trim   
```

一款使用**Golang**开发且适用于攻防演习**内网横向信息收集**的**高并发**网络扫描、服务探测工具。

## 🍭Property
- 多平台支持（Windows、Mac、Linux、Cobalt Strike）
- 存活IP探测（支持TCP、ICMP两种模式）
- 超快的端口扫描
- 服务和应用版本检测功能，内置指纹探针采用:[nmap-service-probes](https://raw.githubusercontent.com/nmap/nmap/master/nmap-service-probes)
- Web服务（http、https）信息探测
- ~~扫描结果兼容INFINITY攻防协同平台~~（暂不公开）

## 🎉First Game

​	总结诸多实战经验，考虑到实战过程中会出现和存在复杂的环境、红蓝对抗过程中常用的内存加载无文件落地执行等，因此**ServerScan**设计了**轻巧版**、**专业版**、支持**Cobalt Strike跨平台beacon:[Cross C2](https://github.com/gloxec/CrossC2)的动态链接库**，**~~以及支持INFINITY攻防协同平台的专用版~~**。便于在不同的Shell环境中可以轻松自如地使用：如：Windows Cmd、Linux Console、远控Console、WebShell等，以及Cobalt Strike联动使用cna脚本文件加载，实现内网信息快速收集，为下一步横向移动铺路。

**轻巧版：**

 参数形式简单、扫描速度快、耗时短、文件体积小、适合在网络情况较好的条件情况下使用。

**专业版：**

 支持参数默认值、支持自定义扫描超时时长、支持扫描结果导出、适合在网络条件较苛刻的情况下使用。

**动态链接库：**

 为支持Cobalt Strike跨平台beacon，无文件落地执行，无文件执行的进程信息，基于轻巧版本进行动态链接库编译，扫描超时时长为1.5秒。

### 💻for  Linux or Windows

  * #### 轻巧版
  
    * ***for PortScan***
    
      **Usage：**
    
      ![Air_scan_use](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/Linux/Air_scan_use.png)
    
      **Scanning：**
    
      ![Air_scan1](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/Linux/Air_scan.png)
    
    * ***for Service and Version Detection***
    
      **Usage：**
    
      ![Air_scan_probes_use](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/Windows/Air_scan_probes_use.png)
    
      **Scanning：**
    
      ![Air_scan_probes](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/Windows/Air_scan_probes.png)
  
  * #### 专业版

    * ***for PortScan***

      **Usage：**

      ![Pro_scan_use](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/Linux/Pro_scan_use.png)

      **Scanning：**
    
      ![Pro_scan](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/Linux/Pro_scan.png)
    
    * ***for Service and Version Detection***
    
      **Usage：**
    
      ![Pro_scan_probes_use](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/Windows/Pro_scan_probes_use.png)
    
      **Scanning：**
    
      ![Pro_scan_probes](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/Windows/Pro_scan_probes.png)


### 🎮for Cobalt Strike

  * ***Windows***

       	由于Cobalt Strike已经内置了PortScan，因此目前Windows仅支持利用cna上传对应版本的ServerScan可执行文件到服务器进行扫描。

      * ***for Service and Version Detection***

        Interact:

        ![serverscan_windows](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/CobaltStrike/serverscan_windows.jpg)

        ![serverscan2_windows](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/CobaltStrike/serverscan2_windows.jpg)


  * ***Cobalt Strike跨平台beacon***

    ​        ServerScan的优势在于跨平台，在Hook师傅的帮（jiān）助（dū）下目前已经基本适配了[Cross C2](https://github.com/gloxec/CrossC2)的Linux、Mac OS两大平台，为了提高隐匿性减少文件特征，目前支持内存加载可执行程序和动态链接库调用，您只需在安装了Cross C2的Cobalt Strike中导入对应的.cna脚本，即可实现ServerScan与Cobalt Strike跨平台beacon联动，具体使用参考[Usage](#usage)。

      * ***for PortScan***

        Interact:

        ![portscan_console](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/CobaltStrike/portscan_console.jpg)

        Targets结果集自动导入:

        ![portscan_targets](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/CobaltStrike/portscan_targets.jpg)

        services结果集自动导入:

        ![portscan_services](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/CobaltStrike/portscan_services.jpg)

      * ***for Service and Version Detection***

        Interact:

        ![serverscan_console](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/CobaltStrike/serverscan_console.png)

        Targets结果集自动导入:

        ![serverscan_targets](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/CobaltStrike/serverscan_targets.jpg)

        services结果集自动导入:

        ![serverscan_services](https://github.com/Adminisme/ServerScan/raw/master/img/serverscan/CobaltStrike/serverscan_services.jpg)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
