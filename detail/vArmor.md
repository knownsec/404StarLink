## vArmor <https://github.com/bytedance/vArmor>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-bytedance-orange)
![GitHub stars](https://img.shields.io/github/stars/bytedance/vArmor.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.5.11-red)
![Time](https://img.shields.io/badge/Join-20230831-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

vArmor 是一个云原生容器沙箱系统，它借助 Linux 的 [AppArmor LSM](https://en.wikipedia.org/wiki/AppArmor), [BPF LSM](https://docs.kernel.org/bpf/prog_lsm.html) 和 [Seccomp](https://en.wikipedia.org/wiki/Seccomp) 技术实现强制访问控制器（即 enforcer），从而对容器进行安全加固。它可以用于增强容器隔离性、减少内核攻击面、增加容器逃逸或横行移动攻击的难度与成本。

您可以借助 vArmor 在以下场景对 Kubernetes 集群中的容器进行沙箱防护
* 业务场景存在多租户（多租户共享同一个集群），由于成本、技术条件等原因无法使用硬件虚拟化容器（如 Kata Container）
* 需要对关键的业务进行安全加固，增加攻击者权限提升、容器逃逸、横向渗透的难度与成本
* 当出现高危漏洞，但由于修复难度大、周期长等原因无法立即修复时，可以借助 vArmor 实施漏洞利用缓解（具体取决于漏洞类型或漏洞利用向量。缓解代表阻断利用向量、增加利用难度）

*注意：如果需要高强度的隔离方案，建议优先考虑使用硬件虚拟化容器（如 Kata Container）进行计算隔离，并借助 CNI 的 NetworkPolicy 进行网络隔离。*

**vArmor 的特色**
* **Cloud-Native**. vArmor 遵循 Kubernetes Operator 设计模式，用户可通过操作 [CRD API](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) 对特定的 Workloads 进行加固。从而以更贴近业务的视角，实现对容器化微服务的沙箱加固。
* **Multiple Enforcers**. vArmor 将 AppArmor、BPF、Seccomp 抽象为 Enforcer，并支持单独或组合使用，从而对容器的文件访问、进程执行、网络外联、系统调用等进行访问控制。
* **Allow-by-Default**. vArmor 当前重点支持此安全模型。即只有显式声明的行为会被阻断，从而减少性能损失和增加易用性。
* **Built-in Rules**. vArmor 提供了一系列开箱即用的内置规则。这些规则为 Allow-by-Default 安全模型设计，从而极大降低对用户专业知识的要求。
* **Behavior Modeling**. vArmor 支持对工作负载进行行为建模。这可用于开发白名单安全策略、分析哪些内置规则可用于加固应用、指导工作负载的配置遵循权限最小化原则。
* **Deny-by-Default**. vArmor 可以基于行为模型创建白名单安全策略，从而确保仅显式声明的行为被允许。

vArmor 由字节跳动终端安全团队的 **Elkeid Team** 研发，目前该项目仍在积极迭代中。


## 文档
您可以访问 [varmor.org](https://varmor.org) 查看 vArmor 的文档。

👉 **[快速上手](https://www.varmor.org/docs/introduction#quick-start)**

👉 **[安装指引](https://www.varmor.org/docs/getting_started/installation)**

👉 **[使用手册](https://www.varmor.org/docs/getting_started/usage_instructions)**

👉 **[策略与规则](https://www.varmor.org/docs/guides/policies_and_rules)**

👉 **[性能说明](https://www.varmor.org/docs/guides/performance)**


## 贡献
感谢您有兴趣为 vArmor 做出贡献！以下是帮助您入门的一些步骤：

✔ 阅读并遵循社区[行为准则](https://github.com/bytedance/vArmor/blob/main/CODE_OF_CONDUCT.md).

✔ 阅读[开发指引](https://github.com/bytedance/vArmor/blob/main/docs/development_guide.md).

✔ 加入 vArmor [飞书群](https://applink.larkoffice.com/client/chat/chatter/add_by_link?link_token=ae5pfb2d-f8a4-4f0b-b12e-15f24fdaeb24&qr_code=true).

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v0.5.11] - 2024-07-09

**更新**  
- 发生冲突时重试删除ArmorProfile finalizers  
- Gin logger现在仅记录未成功的请求  
- 修复容器启动时加载BPF配置文件  
- 修复当服务响应未经授权时返回错误

#### [v0.5.10] - 2024-06-25

**修复**  
- 修正功能中的拼写错误

#### [v0.5.9] - 2024-06-15

**更新**  
- 为 Seccomp enforcer 添加了 disable-chmod-s-bit 内置规则  
- 重构 Seccomp enforcer，并尽可能合并规则  
- 为 Seccomp enforcer 添加了 AlwaysAllow 和 RuntimeDefault 模式  
- 将来自 containerd 的上游规则同步到 AppArmor 配置文件模板  
- 为 AppArmor enforcer 合并相同的子配置文件  
- 为 AppArmor enforcer 引入了违规审计功能  
- 支持修改现有策略并动态添加执行器  
- 优化 VarmorClusterPolicy/VarmorPolicy CR 的状态以显示更多错误信息  
- 为 ArmorProfile CR 添加了ownerReference 和 finalizers 以防止意外删除  
- 策略顾问现在可以使用行为模型数据生成策略模板  
- 更新文档  
- 修复：CI 工作流登录使用 docker/login-action  
- 修复：忽略 Seccomp enforcer 的 enhancedProtect 特权选项  
- 修复：确保正确执行 CR 的清理逻辑  
- 修复：更新图表模板以生成 k8s 资源的固定全名  
- 修复：建模完成后更新 ArmorProfileModel CR

#### [v0.5.8] - 2024-04-24

**更新**  
- 添加`disable-cap-all-except-net-bind-service`内置规则以符合Pod安全标准的限制策略  
- 已弃用 AppArmor 和 BPF 强制执行器的 `disallow-create-user-ns` 内置规则  
- 添加了策略顾问以帮助使用上下文信息生成策略模板

#### [v0.5.7] - 2024-04-16

**更新**  
- 添加了 Seccomp 强制执行器的预检查  
- 将基础镜像升级为 Debian bookworm  
- 将apparmor用户组件升级到3.1  
- 为 Seccomp 强制执行器添加了禁用 chmod-x-bit 内置规则  
- 优化的 CI 工作流程  
- 为Agent添加readinessProbe，优化启动流程  
- 统一日志格式  
- 为演示添加了注释

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
