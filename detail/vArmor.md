## vArmor <https://github.com/bytedance/vArmor>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-bytedance-orange)
![GitHub stars](https://img.shields.io/github/stars/bytedance/vArmor.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.5.6-red)
![Time](https://img.shields.io/badge/Join-20230831-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## 简介

**vArmor** 是一个云原生容器沙箱系统，它借助 Linux 的 [AppArmor LSM](https://en.wikipedia.org/wiki/AppArmor), [BPF LSM](https://docs.kernel.org/bpf/prog_lsm.html) 和 [Seccomp](https://en.wikipedia.org/wiki/Seccomp) 技术实现强制访问控制器（即 enforcer），从而对容器进行安全加固。它可以用于增强容器隔离性、减少内核攻击面、增加容器逃逸或横行移动攻击的难度与成本。

你可以借助 vArmor 在以下场景对 Kubernetes 集群中的容器进行沙箱防护
* 业务场景存在多租户（多租户共享同一个集群），由于成本、技术条件等原因无法使用硬件虚拟化容器（如 Kata Container）
* 需要对关键的业务进行安全加固，增加攻击者权限提升、容器逃逸、横向渗透的难度与成本
* 当出现高危漏洞，但由于修复难度大、周期长等原因无法立即修复时，可以借助 vArmor 实施漏洞利用缓解（具体取决于漏洞类型或漏洞利用向量。缓解代表阻断利用向量、增加利用难度）

**vArmor 的特色**
* 云原生。vArmor 遵循 Kubernetes Operator 设计模式，用户可通过操作 [CRD API](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) 对特定的 Workloads 进行加固。从而以更贴近业务的视角，实现对容器化微服务的沙箱加固
* 支持单独或组合使用 AppArmor、BPF、Seccomp enforcer，对容器的文件访问、进程执行、网络外联、系统调用等进行强制访问控制
* 支持 Allow by Default 安全模型，即只有显式声明的行为会被阻断，从而减少性能损失和增加易用性
* 支持行为建模，并基于行为模型进行安全防护，即只有显式声明的行为会被允许
* 开箱即用。vArmor 包含多种内置加固规则供直接使用

vArmor 由字节跳动终端安全团队的 **Elkeid Team** 研发，目前该项目仍在积极迭代中。

*注意：如果需要高强度的隔离方案，建议优先考虑使用硬件虚拟化容器（如 Kata Container）进行计算隔离，并借助 CNI 的 NetworkPolicy 进行网络隔离。*


## 架构
<img src="https://github.com/bytedance/vArmor/raw/main/docs/architecture.png" width="600">


## 前置条件
您可以通过策略对象（[VarmorPolicy](https://github.com/bytedance/vArmor/blob/main/docs/usage_instructions.zh_CN.md#varmorpolicy)/[VarmorClusterPolicy](https://github.com/bytedance/vArmor/blob/main/docs/usage_instructions.zh_CN.md#varmorclusterpolicy)）的 `spec.policy.enforcer` 字段来指定 enforcer。另外，您还可以单独、组合使用不同的 enforcer，例如：AppArmorBPF, AppArmorSeccomp, AppArmorBPFSeccomp。

不同 enforcers 所需要的前置条件如下表所示。

|强制访问控制器|要求|推荐|
|------------|--------------------------------------------|--------|
|AppArmor    |1. Linux Kernel 4.15 及以上版本<br>2. 系统需开启 AppArmor LSM|GKE with Container-Optimized OS<br>AKS with Ubuntu 22.04 LTS<br>[VKE](https://www.volcengine.com/product/vke) with veLinux<br>Debian 10 及以上版本<br>Ubuntu 18.04.0 LTS 及以上版本<br>[veLinux 1.0](https://www.volcengine.com/docs/6396/74967) 等
|BPF         |1. Linux Kernel 5.10 及以上版本 (x86_64)<br>2. containerd v1.6.0 及以上版本<br>3. 系统需开启 BPF LSM|EKS with Amazon Linux 2<br>GKE with Container-Optimized OS<br>AKS with Ubuntu 22.04 LTS <sup>\*</sup><br>ACK with Alibaba Cloud Linux 3 <sup>\*</sup><br>OpenSUSE 15.4  <sup>\*</sup><br>Debian 11 <sup>\*</sup><br>Fedora 37<br>[veLinux 1.0 with 5.10](https://www.volcengine.com/docs/6396/74967) 等<br><br>* *需手动启用节点的 BPF LSM*
|Seccomp     |1. Kubernetes v1.19 及以上版本


## 策略模式与内置规则
vArmor 的策略支持 5 种运行模式：**AlwaysAllow、RuntimeDefault、EnhanceProtect、BehaviorModeling、 DefenseInDepth**。当策略运行在 **EnhanceProtect** 模式时，可使用内置规则和自定义接口对容器进行加固。

更多说明请参见 [策略模式与内置规则](https://github.com/bytedance/vArmor/blob/main/docs/built_in_rules.zh_CN.md)。


## 快速上手
**更多配置项和使用说明详见 [使用说明](https://github.com/bytedance/vArmor/blob/main/docs/usage_instructions.zh_CN.md)**

### Step 1. 拉取 chart 包
```
helm pull oci://elkeid-cn-beijing.cr.volces.com/varmor/varmor --version 0.5.6-rc
```

### Step 2. 安装
```
helm install varmor varmor-0.5.6-rc.tgz \
    --namespace varmor --create-namespace \
    --set image.registry="elkeid-cn-beijing.cr.volces.com"
```

### Step 3. 示例
```
# 创建名为 demo 的命名空间
kubectl create namespace demo

# 创建 VarmorPolicy，对符合 .spec.target.selector 的 Deployment 开启 AlwaysAllow 模式沙箱
kubectl create -f test/demo/1-apparmor/vpol-apparmor-alwaysallow.yaml

# 查看 VarmorPolicy & ArmorProfile 状态
kubectl get VarmorPolicy -n demo
kubectl get ArmorProfile -n demo

# 创建 Deployment
kubectl create -f test/demo/1-apparmor/deploy.yaml

# 获取 Pod name
POD_NAME=$(kubectl get Pods -n demo -l app=demo-1 -o name)

# 在 c1 容器中执行命令，读取 secret token
kubectl exec -n demo $POD_NAME -c c1 -- cat /run/secrets/kubernetes.io/serviceaccount/token

# 更新 VarmorPolicy 策略，禁止 Deployment 读取 secret token
kubectl apply -f test/demo/1-apparmor/vpol-apparmor-enhance.yaml

# 在 c1 容器中执行命令，读取 secret token，验证读取行为被禁止
kubectl exec -n demo $POD_NAME -c c1 -- cat /run/secrets/kubernetes.io/serviceaccount/token

# 删除 VarmorPolicy 和 Deployment
kubectl delete -f test/demo/1-apparmor/vpol-apparmor-alwaysallow.yaml
kubectl delete -f test/demo/1-apparmor/deploy.yaml
```

### Step 4. 卸载
```
helm uninstall varmor -n varmor
```


## 性能说明
详见 [性能说明](https://github.com/bytedance/vArmor/blob/main/docs/performance_specification.zh_CN.md)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v0.5.6] - 2024-02-29

**更新**  
- Agent 和 Manager 现在通过 TLS 进行交互  
- 添加 Seccomp 支持增强保护、行为建模和深度防御模式  
- 集群范围策略 VarmorClusterPolicy 现在支持 BehaviorModeling 模式  
- 支持不同执行器的组合，现在可以组合使用 AppArmor、BPF、Seccomp 执行器  
- 在策略接口中添加 `.spec.updateExistingWorkloads`，允许用户独立控制现有工作负载的保护开关  
- 默认启用 Manager 的 --restartExistWorkloads 开关  
- 将策略接口的特权字段移至 `.spec.policy.enhanceProtect` 内部  
- 添加部分内置规则  
- 添加 CI 工作流程以自动化构建和测试流程  
- 添加更多演示并使它们更容易理解  
- 修复 bugs

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
