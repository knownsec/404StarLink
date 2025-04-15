## ksubdomain <https://github.com/boy-hack/ksubdomain>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-w8ay-orange)
![GitHub stars](https://img.shields.io/github/stars/boy-hack/ksubdomain.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.2.1-red)
![Time](https://img.shields.io/badge/Join-20200821-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

# KSubdomain: 极速无状态子域名爆破工具

[![Release](https://img.shields.io/github/release/boy-hack/ksubdomain.svg)](https://github.com/boy-hack/ksubdomain/releases) [![Go Report Card](https://goreportcard.com/badge/github.com/boy-hack/ksubdomain)](https://goreportcard.com/report/github.com/boy-hack/ksubdomain) [![License](https://img.shields.io/github/license/boy-hack/ksubdomain)](https://github.com/boy-hack/ksubdomain/blob/main/LICENSE)

**KSubdomain 是一款基于无状态技术的子域名爆破工具，带来前所未有的扫描速度和极低的内存占用。** 告别传统工具的效率瓶颈，体验闪电般的 DNS 查询，同时拥有可靠的状态表重发机制，确保结果的完整性。 KSubdomain 支持 Windows、Linux 和 macOS，是进行大规模DNS资产探测的理想选择。

![](https://raw.githubusercontent.com/boy-hack/ksubdomain/main/image.gif)

## 🚀 核心优势

*   **闪电般的速度:** 采用无状态扫描技术，直接操作网络适配器进行原始套接字发包，绕过系统内核的网络协议栈，实现惊人的发包速率。通过 `test` 命令可探测本地网卡的最大发送速度。
*   **极低的资源消耗:** 创新的内存管理机制，包括对象池和全局内存池，显著降低内存分配和 GC 压力，即使处理海量域名也能保持低内存占用。
*   **无状态设计:** 类似 Masscan 的无状态扫描，不从系统维护状态表，自建轻量状态表，从根本上解决了传统扫描工具的内存瓶颈和性能限制，以及解决了无状态扫描漏包问题。
*   **可靠的重发:** 内建智能重发机制，有效应对网络抖动和丢包，确保结果的准确性和完整性。
*   **跨平台支持:** 完美兼容 Windows, Linux, macOS。
*   **易于使用:** 简洁的命令行接口，提供验证 (verify) 和枚举 (enum) 两种模式，并内置常用字典。

## ⚡ 性能亮点

KSubdomain 在速度和效率上远超同类工具。以下是在 4 核 CPU、5M 带宽网络环境下，使用 10 万字典进行的对比测试：

| 工具         | 扫描模式 | 发包方式     | 命令                                                                       | 耗时           | 成功个数 | 备注                      |
| ------------ | -------- | ------------ | -------------------------------------------------------------------------- | -------------- | -------- | ------------------------- |
| **KSubdomain** | 验证     | pcap 网卡发包 | `time ./ksubdomain v -b 5m -f d2.txt -o k.txt -r dns.txt --retry 3 --np`  | **~30 秒**     | 1397     | `--np` 关闭实时打印       |
| massdns      | 验证     | pcap/socket  | `time ./massdns -r dns.txt -t A -w m.txt d2.txt --root -o L`                 | ~3 分 29 秒    | 1396     |                           |
| dnsx         | 验证     | socket       | `time ./dnsx -a -o d.txt -r dns.txt -l d2.txt -retry 3 -t 5000`             | ~5 分 26 秒    | 1396     | `-t 5000` 设置 5000 并发 |

**结论:** KSubdomain 的速度是 massdns 的 **7 倍**，是 dnsx 的 **10 倍** 以上！
## 🛠️ 技术革新 (v2.0)

KSubdomain 2.0 版本引入了多项底层优化，进一步压榨性能潜力：

1.  **状态表优化:**
    *   **分片锁 (Sharded Lock):** 替代全局锁，大幅减少锁竞争，提高并发写入效率。
    *   **高效哈希:** 优化键值存储，均匀分布域名，提升查找速度。
2.  **发包机制优化:**
    *   **对象池:** 复用 DNS 包结构体，减少内存分配和 GC 开销。
    *   **模板缓存:** 为相同 DNS 服务器复用以太网/IP/UDP 层数据，减少重复构建开销。
    *   **并行发送:** 多协程并行发包，充分利用多核 CPU 性能。
    *   **批量处理:** 批量发送域名请求，减少系统调用和上下文切换。
3.  **接收机制优化:**
    *   **对象池:** 复用解析器和缓冲区，降低内存消耗。
    *   **并行处理管道:** 接收 → 解析 → 处理三阶段并行，提高处理流水线效率。
    *   **缓冲区优化:** 增加内部 Channel 缓冲区大小，避免处理阻塞。
    *   **高效过滤:** 优化 BPF 过滤规则和包处理逻辑，快速丢弃无效数据包。
4.  **内存管理优化:**
    *   **全局内存池:** 引入 `sync.Pool` 管理常用数据结构，减少内存分配和碎片。
    *   **结构复用:** 复用 DNS 查询结构和序列化缓冲区。
5.  **架构与并发优化:**
    *   **动态并发:** 根据 CPU 核心数自动调整协程数量。
    *   **高效随机数:** 使用性能更优的随机数生成器。
    *   **自适应速率:** 根据网络状况和系统负载动态调整发包速率。
    *   **批量加载:** 批量加载和处理域名，降低单个域名处理的固定开销。

## 📦 安装

1.  **下载预编译二进制文件:** 前往 [Releases](https://github.com/boy-hack/ksubdomain/releases) 页面下载对应系统的最新版本。
2.  **安装 `libpcap` 依赖:**
    *   **Windows:** 下载并安装 [Npcap](https://npcap.com/) 驱动 (WinPcap 可能无效)。
    *   **Linux:** 已静态编译打包 `libpcap`，通常无需额外操作。若遇问题，请尝试安装 `libpcap-dev` 或 `libcap-devel` 包。
    *   **macOS:** 系统自带 `libpcap`，无需安装。
3.  **赋予执行权限 (Linux/macOS):** `chmod +x ksubdomain`
4.  **运行!**

### 源码编译 (可选)

确保您已安装 Go 1.23 版本和 `libpcap` 环境。

```bash
go install -v github.com/boy-hack/ksubdomain/cmd/ksubdomain@latest
# 二进制文件通常位于 $GOPATH/bin 或 $HOME/go/bin
```

## 📖 使用说明

```bash
KSubdomain - 极速无状态子域名爆破工具

用法:
  ksubdomain [全局选项] 命令 [命令选项] [参数...]

版本:
  查看版本信息: ksubdomain --version

命令:
  enum, e    枚举模式: 提供主域名进行爆破
  verify, v  验证模式: 提供域名列表进行验证
  test       测试本地网卡最大发包速度
  help, h    显示命令列表或某个命令的帮助

全局选项:
  --help, -h     显示帮助 (默认: false)
  --version, -v  打印版本信息 (默认: false)
```

### 验证模式 (Verify)

验证模式用于快速检查提供的域名列表的存活状态。

```bash
./ksubdomain verify -h # 查看验证模式帮助，可缩写 ksubdomain v

USAGE:
   ksubdomain verify [command options] [arguments...]

OPTIONS:
   --filename value, -f value       验证域名的文件路径
   --domain value, -d value         域名
   --band value, -b value           宽带的下行速度，可以5M,5K,5G (default: "3m")
   --resolvers value, -r value      dns服务器，默认会使用内置dns
   --output value, -o value         输出文件名
   --output-type value, --oy value  输出文件类型: json, txt, csv (default: "txt")
   --silent                         使用后屏幕将仅输出域名 (default: false)
   --retry value                    重试次数,当为-1时将一直重试 (default: 3)
   --timeout value                  超时时间 (default: 6)
   --stdin                          接受stdin输入 (default: false)
   --not-print, --np                不打印域名结果 (default: false)
   --eth value, -e value            指定网卡名称
   --wild-filter-mode value         泛解析过滤模式[从最终结果过滤泛解析域名]: basic(基础), advanced(高级), none(不过滤ne")
   --predict                        启用预测域名模式 (default: false)
   --help, -h                       show help (default: false)

# 示例:
# 验证多个域名解析
./ksubdomain v -d xx1.example.com -d xx2example.com

# 从文件读取域名进行验证，保存为 output.txt
./ksubdomain v -f domains.txt -o output.txt

# 从标准输入读取域名，带宽限制为 10M
cat domains.txt | ./ksubdomain v --stdin -b 10M

# 启用预测模式，泛解析过滤，保存为csv
./ksubdomain v -f domains.txt --predict --wild-filter-mode advanced --oy csv -o output.csv
```

### 枚举模式 (Enum)

枚举模式基于字典和预测算法爆破指定域名下的子域名。

```bash
./ksubdomain enum -h # 查看枚举模式帮助,可简写 ksubdomain e

USAGE:
   ksubdomain enum [command options] [arguments...]

OPTIONS:
   --domain value, -d value         域名
   --band value, -b value           宽带的下行速度，可以5M,5K,5G (default: "3m")
   --resolvers value, -r value      dns服务器，默认会使用内置dns
   --output value, -o value         输出文件名
   --output-type value, --oy value  输出文件类型: json, txt, csv (default: "txt")
   --silent                         使用后屏幕将仅输出域名 (default: false)
   --retry value                    重试次数,当为-1时将一直重试 (default: 3)
   --timeout value                  超时时间 (default: 6)
   --stdin                          接受stdin输入 (default: false)
   --not-print, --np                不打印域名结果 (default: false)
   --eth value, -e value            指定网卡名称
   --wild-filter-mode value         泛解析过滤模式[从最终结果过滤泛解析域名]: basic(基础), advanced(高级), none(不过滤) (default: "none")
   --predict                        启用预测域名模式 (default: false)
   --filename value, -f value       字典路径
   --ns                             读取域名ns记录并加入到ns解析器中 (default: false)
   --help, -h                       show help (default: false)

# 示例:
# 枚举多个域名
./ksubdomain e -d example.com -d hacker.com

# 从文件读取字典枚举，保存为 output.txt
./ksubdomain e -f sub.dict -o output.txt

# 从标准输入读取域名，带宽限制为 10M
cat domains.txt | ./ksubdomain e --stdin -b 10M

# 启用预测模式枚举域名，泛解析过滤，保存为csv
./ksubdomain e -d example.com --predict --wild-filter-mode advanced --oy csv -o output.csv
```

## ✨ 特性与技巧

*   **带宽自动适配:** 只需使用 `-b` 参数指定你的公网下行带宽 (如 `-b 10m`), KSubdomain 会自动优化发包速率。
*   **测试最大速率:** 运行 `./ksubdomain test` 测试当前环境的最大理论发包速率。
*   **自动网卡检测:** KSubdomain 会自动检测可用网卡。可通过环境变量 `KSubdomainEth` 指定网卡，或--eth制定网卡名称。
*   **进度显示:** 实时进度条显示 成功数 / 发送数 / 队列长度 / 接收数 / 失败数 / 已耗时。
*   **参数调优:** 根据网络质量和目标域名数量，调整 `--retry` 和 `--timeout` 参数以获得最佳效果。当 `--retry` 为 -1 时，将无限重试直至所有请求成功或超时。
*   **多种输出格式:** 支持 `txt` (实时输出), `json` (完成后输出), `csv` (完成后输出)。通过 `-o` 指定文件名后缀即可 (如 `result.json`)。
*   **环境变量配置:**
    *   `KSubdomainConfig`: 指定配置文件的路径。
    *   `KSubdomainEth`: 指定使用的网卡名称 (例如 `eth0`)。

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2020-09-02 发布文章[《ksubdomain 无状态域名爆破工具》](https://paper.seebug.org/1325/)
- 2019-10-12 发布文章[《从 Masscan, Zmap 源码分析到开发实践》](https://paper.seebug.org/1052/)

## 最近更新

#### [v2.2.1] - 2025-04-13

**更新**  
1. **状态表优化:**  
  - **分片锁 (Sharded Lock):** 替代全局锁，大幅减少锁竞争，提高并发写入效率。  
  - **高效哈希:** 优化键值存储，均匀分布域名，提升查找速度。  
2. **发包机制优化:**  
  - **对象池:** 复用 DNS 包结构体，减少内存分配和 GC 开销。  
  - **模板缓存:** 为相同 DNS 服务器复用以太网/IP/UDP 层数据，减少重复构建开销。  
  - **并行发送:** 多协程并行发包，充分利用多核 CPU 性能。  
  - **批量处理:** 批量发送域名请求，减少系统调用和上下文切换。  
3. **接收机制优化:**  
  - **对象池:** 复用解析器和缓冲区，降低内存消耗。  
  - **并行处理管道:** 接收 → 解析 → 处理三阶段并行，提高处理流水线效率。  
  - **缓冲区优化:** 增加内部 Channel 缓冲区大小，避免处理阻塞。  
  - **高效过滤:** 优化 BPF 过滤规则和包处理逻辑，快速丢弃无效数据包。  
4. **内存管理优化:**  
  - **全局内存池:** 引入 `sync.Pool` 管理常用数据结构，减少内存分配和碎片。  
  - **结构复用:** 复用 DNS 查询结构和序列化缓冲区。  
5. **架构与并发优化:**  
  - **动态并发:** 根据 CPU 核心数自动调整协程数量。  
  - **高效随机数:** 使用性能更优的随机数生成器。  
  - **自适应速率:** 根据网络状况和系统负载动态调整发包速率。  
  - **批量加载:** 批量加载和处理域名，降低单个域名处理的固定开销。

#### [v1.9.5] - 2022-03-31

**更新**  
- 增加suffix domain指定特定dns的提示  
- 修复verify模式计算域名总量错误

#### [v1.9.3] - 2022-03-24

**更新**  
- 增加编程接口，ksubdomain可作为一个库封装  
- enum模式加入--ns参数，用于添加特定dns  
- 修复域名太多时扫描卡住的问题  


#### [v1.8.5] - 2022-03-06

**优化**  
- 修复高并发下出现的一处内存拷贝问题  
- 优化泛解析时的错误处理

#### [v1.8.1] - 2022-02-13

**重构**  
- 优化了代码结构，优化了go协程组织方式，代码易懂，解决了一些冲突问题  
- 设计了一种新的算法，用来快速发包并且大大减少失败率  
- 获取网卡改为了全自动并可以根据配置文件读取  
- 增加有一个实时的进度条，依次显示成功/发送/队列/接收/失败/耗时信息

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
