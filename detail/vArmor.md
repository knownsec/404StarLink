## vArmor <https://github.com/bytedance/vArmor>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-bytedance-orange)
![GitHub stars](https://img.shields.io/github/stars/bytedance/vArmor.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.5.5-red)
![Time](https://img.shields.io/badge/Join-20230831-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## 简介

**vArmor** 是一个云原生容器沙箱系统，它借助 Linux 的 LSM 技术（AppArmor & BPF）实现强制访问控制器（即 enforcer），从而对容器进行安全加固。它可以用于增强容器隔离性、减少内核攻击面、增加容器逃逸或横行移动攻击的难度与成本。**vArmor** 遵循 Kubernetes Operator 设计模式，用户可通过操作 CRD API 对特定的 Workload 进行加固。从而以更贴近业务的视角，实现对容器化微服务的沙箱加固。此外 **vArmor** 还包含多种内置加固规则，具备开箱即用的特性。

你可以借助 **vArmor** 在以下场景对 Kubernetes 集群中的容器进行沙箱防护
* 业务场景存在多租户（多租户共享同一个集群），由于成本、技术条件等原因无法使用硬件虚拟化容器（如 Kata Container）
* 需要对关键的业务进行安全加固，增加攻击者权限提升、容器逃逸、横向渗透的难度与成本
* 当出现高危漏洞，但由于修复难度大、周期长等原因无法立即修复时，可以借助 **vArmor** 实施漏洞利用缓解（具体取决于漏洞类型或漏洞利用向量。缓解代表阻断利用向量、增加利用难度）

**vArmor** 通过以下技术实现云原生容器沙箱
* 借助 Linux 的 AppArmor 或 BPF LSM，在内核中对容器进程进行强制访问控制（文件、程序、网络外联等）
* 为减少性能损失和增加易用性，**vArmor** 的安全模型为 Allow by Default，即只有显式声明的行为会被阻断
* 用户通过操作自定义对象（参见 [Custom Resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)）实现对指定 Workloads 中的容器进行沙箱加固
* 用户可以通过选择和配置沙箱规则（内置规则、自定义规则）来对容器进行强制访问控制。内置规则包含一些常见的提权阻断、渗透入侵防御策略。

**vArmor** 由字节跳动终端安全团队的 **Elkeid Team** 研发，目前该项目仍在积极迭代中。

*注意：如果需要高强度的隔离方案，建议优先考虑使用硬件虚拟化容器（如 Kata Container）进行计算隔离，并借助 CNI 的 NetworkPolicy 进行网络隔离。*


## 架构
<img src="https://github.com/bytedance/vArmor/raw/main/docs/architecture.png" width="600">


## 前置条件
|强制访问控制器|要求|推荐|
|------------|--------------------------------------------|--------|
|AppArmor    |1. Linux Kernel 4.15 及以上版本<br>2. 系统需开启 AppArmor LSM|GKE with Container-Optimized OS<br>AKS with Ubuntu 22.04 LTS<br>[VKE](https://www.volcengine.com/product/vke) with veLinux<br>Debian 10 及以上版本<br>Ubuntu 18.04.0 LTS 及以上版本<br>[veLinux](https://www.volcengine.com/docs/6396/74967) 等
|BPF         |1. Linux Kernel 5.7 及以上版本<br>2. containerd v1.6.0 及以上版本<br>3. 系统需开启 BPF LSM|EKS with Amazon Linux 2<br>GKE with Container-Optimized OS<br>AKS with Ubuntu 22.04 LTS <sup>\*</sup><br>ACK with Alibaba Cloud Linux 3 <sup>\*</sup><br>OpenSUSE 15.4  <sup>\*</sup><br>Debian 11 <sup>\*</sup><br>Fedora 37 等<br><br>* *需手动启用节点的 BPF LSM*


## 内置规则
**vArmor** 提供 5 种类型的[内置规则](https://github.com/bytedance/vArmor/blob/main/docs/built_in_rules.zh_CN.md#%E5%86%85%E7%BD%AE%E8%A7%84%E5%88%99)和自定义接口，以满足不同的防护需求。

|类型|说明|
|-------------------------|----------------------------------------------------------------------------------|
| Always Allow            | 在容器启动时不对其施加任何限制，可在稍后变更配置，从而在无需重启工作负载的情况下动态调整防护策略。|
| Runtime Default         | 使用与容器运行时组件相同的默认规则进行基础防护，防护强度较弱。（如 containerd 的 [cri-containerd.apparmor.d](https://github.com/containerd/containerd/blob/main/contrib/apparmor/template.go)）|
| Hardening               | 对容器进行加固，减少攻击面的规则。包括：<br>* 阻断特权容器的常见逃逸向量<br>* 禁用 capabilities<br>* 阻断部分内核漏洞利用向量|
| Attack Protection       | 针对黑客渗透入侵手法进行防护的规则。从而增加攻击的难度和成本，进行纵深防御。包括：<br>* 容器信息泄露缓解<br>* 禁止执行敏感行为<br>* 对特定可执行文件进行沙箱限制（仅限 AppArmor enforcer）|
| Vulnerability Mitigation| 针对由不安全配置导致的漏洞、特定 0day 漏洞、由软件 feature 导致的安全漏洞，在漏洞被修复前提供防护，阻断或增加漏洞利用的难度<br>（注：取决于漏洞类型或漏洞利用向量）。|


## 快速上手
**更多配置项和使用说明详见 [使用说明](https://github.com/bytedance/vArmor/blob/main/docs/usage_instructions.zh_CN.md)**

### Step 1. 拉取 chart 包
```
helm pull oci://elkeid-cn-beijing.cr.volces.com/varmor/varmor --version 0.5.4
```

### Step 2. 安装
```
helm install varmor varmor-0.5.4.tgz \
    --namespace varmor --create-namespace \
    --set image.registry="elkeid-cn-beijing.cr.volces.com"
```

### Step 3. 示例
```
# 创建 VarmorPolicy，对符合 .spec.target.selector 的 Deployment 开启 AlwaysAllow 模式沙箱
kubectl create -f test/demo/disable-shell/policy-init.yaml

# 查看 VarmorPolicy & ArmorProfile 状态
kubectl get VarmorPolicy -n demo
kubectl get ArmorProfile -n demo

# 创建 Deployment
kubectl create -f test/demo/1/deploy.yaml

# 获取 Pod name
POD_NAME=$(kubectl get Pods -n demo -l app=demo-1 -o name)

# 在 c1 容器中执行命令，读取 secret token
kubectl exec -n demo $POD_NAME -c c1 -- cat /run/secrets/kubernetes.io/serviceaccount/token

# 更新 VarmorPolicy 策略，禁止 Deployment 读取 secret token
kubectl apply -f test/demo/1/policy.yaml

# 在 c1 容器中执行命令，读取 secret token，验证读取行为被禁止
kubectl exec -n demo $POD_NAME -c c1 -- cat /run/secrets/kubernetes.io/serviceaccount/token

# 删除 VarmorPolicy 和 Deployment
kubectl delete -f test/demo/disable-shell/policy-init.yaml
kubectl create -f test/demo/1/deploy.yaml
```

### Step 4. 卸载
```
helm uninstall varmor -n varmor
```


## 性能说明
详见 [性能说明](https://github.com/bytedance/vArmor/blob/main/docs/performance_specification.zh_CN.md)


## 许可证
vArmor 采用 Apache License, Version 2.0 许可证，受不同许可证约束的第三方组件除外。具体请参考代码文件中的代码头信息。

将 vArmor 集成到您自己的项目中应遵守 Apache 2.0 许可证以及适用于 vArmor 中包含的第三方组件的其他许可证。

vArmor 所使用的 eBPF 代码位于 [vArmor-ebpf](https://github.com/bytedance/vArmor-ebpf.git) 项目，并且使用 GPL-2.0 许可证。


## 致谢
vArmor 使用 [cilium/ebpf](https://github.com/cilium/ebpf) 来管理 eBPF 程序。

vArmor 在研发初期参考了 [Nirmata](https://nirmata.com/) 开发的 [kyverno](https://github.com/kyverno/kyverno) 的部分实现。 


## 演示
下面是一个使用 vArmor 对 Deployment 进行加固，防御 CVE-2021-22555 攻击的演示（Exploit 修改自 [cve-2021-22555](https://github.com/google/security-research/tree/master/pocs/linux/cve-2021-22555)）。<br>
![image](https://github.com/bytedance/vArmor/raw/main/test/demo/kernel-exp/CVE-2021-22555/demo.zh_CN.gif)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v0.5.5] - 2024-01-11

**更新**  
- 重构 AppArmor 执行器的行为建模功能  
- 引入BehaviorModeling模式来收集应用行为并生成模型  
- 优化 BPF 强制执行器的安装访问控制原语以解决绕过问题  
- 修复异常节点影响策略状态的问题  
- 升级到1.20版本并在容器内构建BPF程序  
- 支持拉取亚太东南地区的镜像和图表

#### [v0.5.4] - 2023-10-19

**更新**  
- 为 BPF 强制访问控制器增加 mount 系统调用的强制访问控制原语  
- 为 BPF 强制访问控制器添加新的内置规则，包括 disallow-mount、disallow-umount 等  
- 微调部分强制访问控制器的内置规则，使其更加精确并避免非预期行为  
- 默认情况下在 RuntimeDefault 规则之上构建增强的保护规则  
- 改进 BPF 强制执行器的 RuntimeDefault 模式  
- 引入集群范围的策略接口：VarmorClusterPolicy CR  
- 文档优化

#### [v0.5.3] - 2023-09-12

**更新**  
- 优化容器 manager 选举逻辑  
- 添加 webhook matchlabel 和 BPF 强制执行器独占模式配置选项  
- 引入 ptrace 原语和 BPF 强制执行器的内置规则  
- 优化文档

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
