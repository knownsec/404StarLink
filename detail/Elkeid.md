## Elkeid <https://github.com/bytedance/Elkeid>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-C/Golang-blue)
![Author](https://img.shields.io/badge/Author-bytedance-orange)
![GitHub stars](https://img.shields.io/github/stars/bytedance/Elkeid.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.0-red)
![Time](https://img.shields.io/badge/Join-20210422-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

[English](README.md) | 简体中文

Elkeid是一个云原生的基于主机的安全(入侵检测与风险识别)解决方案。

## Elkeid Architecture

<img src="https://github.com/bytedance/Elkeid/raw/main/server/docs/server.png"/>

##  Elkeid Host Ability
<img src="https://github.com/bytedance/Elkeid/raw/main/png/Ability_1.png"/>

* **[Elkeid Agent](https://github.com/bytedance/Elkeid/blob/main/agent/README-zh_CN.md)** 用户态 Agent，负责管理各个端上能力组件，与 **Elkeid Server** 通讯
* **[Elkeid Driver](https://github.com/bytedance/Elkeid/blob/main/driver/README-zh_CN.md)** 在 Linux Kernel 层采集数据的组件，兼容容器环境，并能够提供Rootkit检测能力。与Elkeid Agent管理的Driver插件通讯
* **[Elkeid RASP](rasp)** 支持 CPython、Golang、JVM、NodeJS 的运行时数据采集探针，支持动态注入到运行时。
* **Elkeid Agent Plugin List**
  * [Driver Plugin](plugins/driver): 负责与**Elkeid Driver**通信，处理其传递的数据等
  * [Collector Plugin](plugins/collector): 负责端上的资产/关键信息采集工作，如用户，定时任务，包信息等等
  * [Journal Watcher](plugins/journal_watcher): 负责监测systemd日志的插件，目前支持ssh相关日志采集与上报
  * [Scanner Plugin](https://github.com/bytedance/Elkeid/blob/main/plugins/scanner): 负责在端上进行静态检测恶意文件的插件，目前支持yara
  * [RASP Plugin](https://github.com/bytedance/Elkeid/tree/main/rasp/plugin): 分析系统进程运行时，上报运行时信息，处理server下发的 attach 指令，收集各个探针上报的数据，并支持与探针通信。

以上组件可以提供以下数据：
<img src="https://github.com/bytedance/Elkeid/raw/main/png/data_index.png"/>
Driver Data
<img src="https://github.com/bytedance/Elkeid/raw/main/png/data1.png"/>
Other Data
<img src="https://github.com/bytedance/Elkeid/raw/main/png/data2.png"/>


## Elkeid Backend Ability
* **[Elkeid AgentCenter](server/agent_center)** 负责与Agent进行通信，采集Agent数据并简单处理后汇总到消息队列集群，同时也负责对Agent进行管理包括Agent的升级，配置修改，任务下发等
* **[Elkeid ServiceDiscovery](server/service_discovery)** 后台中的各个服务模块都需要向该组件定时注册、同步服务信息，从而保证各个服务模块中的实例相互可见，便于直接通信
* **[Elkeid Manager](server/manager)** 负责对整个后台进行管理，并提供相关的查询、管理接口
* **[Elkeid Console](server/web_console)** Elkeid 前端部分
* **[Elkeid HUB](https://github.com/bytedance/Elkeid-HUB)** Elkeid HIDS RuleEngine，需要注意的是社区版HUB策略仅做示例使用，不保证任何的准确性和覆盖度

## Elkeid Advantage

* **性能优异**：端上能力借助Elkeid Driver与很多定制开发，性能极佳
* **为入侵检测而生**：数据采集以高强度对抗为前提，对如Kernel Rootkit，提权，无文件攻击等众多高级对抗场景均有针对性数据采集
* **支持云原生**：从端上能力到后台部署都支持云原生环境
* **百万级生产环境验证**：整体经过内部百万级验证，从端到Server，稳定性与性能经过考验，Elkeid不仅仅是一个PoC，是生产级的；开源版本即内部Release Version
* **二次开发友好**：Elkeid 方便二次开发与定制化需求增加



## Front-end display
* 主机详情
<img src="https://github.com/bytedance/Elkeid/raw/main/png/console1.png" style="float:left;"/>
* 资产详情
<img src="https://github.com/bytedance/Elkeid/raw/main/png/console2.png" style="float:left;"/>
* 告警详情
<img src="https://github.com/bytedance/Elkeid/raw/main/png/console3.png" style="float:left;"/>
* Allow List Management
<img src="https://github.com/bytedance/Elkeid/raw/main/png/console6.png" style="float:left;"/>
* Agent/Plugin 管理
<img src="https://github.com/bytedance/Elkeid/raw/main/png/console4.png" style="float:left;"/>
* 用户 管理
<img src="https://github.com/bytedance/Elkeid/raw/main/png/console5.png" style="float:left;"/>


## Quick Start
* **[通过Elkeidup部署](elkeidup/README-zh_CN.md)**


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-11-10 发布文章[《抗击黑客：如何利用Elkeid构建入侵检测能力》](https://mp.weixin.qq.com/s/iwvkIdgMblVOH7Agg_wXtQ)

## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
