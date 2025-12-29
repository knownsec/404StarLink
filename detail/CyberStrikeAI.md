## CyberStrikeAI <https://github.com/Ed1s0nZ/CyberStrikeAI>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Nodejs-blue)
![Author](https://img.shields.io/badge/Author-xx-orange)
![GitHub stars](https://img.shields.io/github/stars/author/xx.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)
![Time](https://img.shields.io/badge/Join-20200101-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->





<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关
CyberStrikeAI 是一款 **AI 原生安全测试平台**，基于 Go 构建，集成了 100+ 安全工具、智能编排引擎与完整的测试生命周期管理能力。通过原生 MCP 协议与 AI 智能体，支持从对话指令到漏洞发现、攻击链分析、知识检索与结果可视化的全流程自动化，为安全团队提供可审计、可追溯、可协作的专业测试环境。

> 在安全领域，真正稀缺的从来不是工具，而是判断。判断来自经验，而经验往往只能依附在个人身上，难以继承、难以复用。CyberStrikeAI 尝试解决的不是“如何自动化攻击”，而是：在复杂、多变、充满不确定性的环境中，下一步“应该做什么”，以及“为什么”。它不追求更激进的自动化，而是试图把安全专家的思考方式、决策路径与失败经验，转化为一个可约束、可复盘、可演进的系统能力。如果经验可以脱离个人而存在，那么安全，才真正具备了被系统性继承的可能。


## 特性速览

- 🤖 兼容 OpenAI/DeepSeek/Claude 等模型的智能决策引擎
- 🔌 原生 MCP 协议，支持 HTTP / stdio 以及外部 MCP 接入
- 🧰 100+ 现成工具模版 + YAML 扩展能力
- 📄 大结果分页、压缩与全文检索
- 🔗 攻击链可视化、风险打分与步骤回放
- 🔒 Web 登录保护、审计日志、SQLite 持久化
- 📚 知识库功能：向量检索与混合搜索，为 AI 提供安全专业知识
- 📁 对话分组管理：支持分组创建、置顶、重命名、删除等操作
- 🛡️ 漏洞管理功能：完整的漏洞 CRUD 操作，支持严重程度分级、状态流转、按对话/严重程度/状态过滤，以及统计看板

## 工具概览

系统预置 100+ 渗透/攻防工具，覆盖完整攻击链：

- **网络扫描**：nmap、masscan、rustscan、arp-scan、nbtscan
- **Web 应用扫描**：sqlmap、nikto、dirb、gobuster、feroxbuster、ffuf、httpx
- **漏洞扫描**：nuclei、wpscan、wafw00f、dalfox、xsser
- **子域名枚举**：subfinder、amass、findomain、dnsenum、fierce
- **网络空间搜索引擎**：fofa_search、zoomeye_search
- **API 安全**：graphql-scanner、arjun、api-fuzzer、api-schema-analyzer
- **容器安全**：trivy、clair、docker-bench-security、kube-bench、kube-hunter
- **云安全**：prowler、scout-suite、cloudmapper、pacu、terrascan、checkov
- **二进制分析**：gdb、radare2、ghidra、objdump、strings、binwalk
- **漏洞利用**：metasploit、msfvenom、pwntools、ropper、ropgadget
- **密码破解**：hashcat、john、hashpump
- **取证分析**：volatility、volatility3、foremost、steghide、exiftool
- **后渗透**：linpeas、winpeas、mimikatz、bloodhound、impacket、responder
- **CTF 实用工具**：stegsolve、zsteg、hash-identifier、fcrackzip、pdfcrack、cyberchef
- **系统辅助**：exec、create-file、delete-file、list-files、modify-file

## 基础使用

### 快速上手
1. **获取代码并安装依赖**
   ```bash
   git clone https://github.com/Ed1s0nZ/CyberStrikeAI.git
   cd CyberStrikeAI-main
   go mod download
   ```
2. **初始化 Python 虚拟环境（tools 目录所需）**  
   `tools/*.yaml` 中大量工具（如 `api-fuzzer`、`http-framework-test`、`install-python-package` 等）依赖 Python 生态。首次进入项目根目录时请创建本地虚拟环境并安装依赖：
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```
   两个 Python 专用工具（`install-python-package` 与 `execute-python-script`）会自动检测该 `venv`（或已经激活的 `$VIRTUAL_ENV`），因此默认 `env_name` 即可满足大多数场景。
3. **配置模型与鉴权**  
   启动后在 Web 端 `Settings` 填写，或直接编辑 `config.yaml`：
   ```yaml
   openai:
     api_key: "sk-your-key"
     base_url: "https://api.openai.com/v1"
     model: "gpt-4o"
   auth:
     password: ""                 # 为空则首次启动自动生成强口令
     session_duration_hours: 12
   security:
     tools_dir: "tools"
   ```
4. **按需安装安全工具（可选）**
   ```bash
   # macOS
   brew install nmap sqlmap nuclei httpx gobuster feroxbuster subfinder amass
   # Ubuntu/Debian
   sudo apt-get install nmap sqlmap nuclei httpx gobuster feroxbuster
   ```
   未安装的工具会自动跳过或改用替代方案。
5. **启动服务**
   ```bash
   chmod +x run.sh && ./run.sh
   # 或
   go run cmd/server/main.go
   # 或
   go build -o cyberstrike-ai cmd/server/main.go
   ```
6. **浏览器访问** http://localhost:8080 ，使用日志中提示的密码登录并开始对话。

### 常用流程
- **对话测试**：自然语言触发多步工具编排，SSE 实时输出。
- **工具监控**：查看任务队列、执行日志、大文件附件。
- **会话历史**：所有对话与工具调用保存在 SQLite，可随时重放。
- **对话分组**：将对话按项目或主题组织到不同分组，支持置顶、重命名、删除等操作，所有数据持久化存储。
- **漏洞管理**：在测试过程中创建、更新和跟踪发现的漏洞。支持按严重程度（严重/高/中/低/信息）、状态（待确认/已确认/已修复/误报）和对话进行过滤，查看统计信息并导出发现。
- **可视化配置**：在界面中切换模型、启停工具、设置迭代次数等。

### 默认安全措施
- 设置面板内置必填校验，防止漏配 API Key/Base URL/模型。
- `auth.password` 为空时自动生成 24 位强口令并写回 `config.yaml`。
- 所有 API（除登录外）都需携带 Bearer Token，统一鉴权中间件拦截。
- 每个工具执行都带有超时、日志和错误隔离。

## 进阶使用

### 工具编排与扩展
- `tools/*.yaml` 定义命令、参数、提示词与元数据，可热加载。
- `security.tools_dir` 指向目录即可批量启用；仍支持在主配置里内联定义。
- **大结果分页**：超过 200KB 的输出会保存为附件，可通过 `query_execution_result` 工具分页、过滤、正则检索。
- **结果压缩/摘要**：多兆字节日志可先压缩或生成摘要再写入 SQLite，减小档案体积。

**自定义工具的一般步骤**
1. 复制 `tools/` 下现有示例（如 `tools/sample.yaml`）。
2. 修改 `name`、`command`、`args`、`short_description` 等基础信息。
3. 在 `parameters[]` 中声明位置参数或带 flag 的参数，方便智能体自动拼装命令。
4. 视需要补充 `description` 或 `notes`，给 AI 额外上下文或结果解读提示。
5. 重启服务或在界面中重新加载配置，新工具即可在 Settings 面板中启用/禁用。

### 攻击链分析
- 智能体解析每次对话，抽取目标、工具、漏洞与因果关系。
- Web 端可交互式查看链路节点、风险级别及时间轴，支持导出报告。

### MCP 全场景
- **Web 模式**：自带 HTTP MCP 服务供前端调用。
- **MCP stdio 模式**：`go run cmd/mcp-stdio/main.go` 可接入 Cursor/命令行。
- **外部 MCP 联邦**：在设置中注册第三方 MCP（HTTP/stdio），按需启停并实时查看调用统计与健康度。

#### MCP stdio 快速集成
1. **编译可执行文件**（在项目根目录执行）：
   ```bash
   go build -o cyberstrike-ai-mcp cmd/mcp-stdio/main.go
   ```
2. **在 Cursor 中配置**  
   打开 `Settings → Tools & MCP → Add Custom MCP`，选择 **Command**，指定编译后的程序与配置文件：
   ```json
   {
     "mcpServers": {
       "cyberstrike-ai": {
         "command": "/absolute/path/to/cyberstrike-ai-mcp",
         "args": [
           "--config",
           "/absolute/path/to/config.yaml"
         ]
       }
     }
   }
   ```
   将路径替换成你本地的实际地址，Cursor 会自动启动 stdio 版本的 MCP。

#### MCP HTTP 快速集成
1. 确认 `config.yaml` 中 `mcp.enabled: true`，按照需要调整 `mcp.host` / `mcp.port`（本地建议 `127.0.0.1:8081`）。
2. 启动主服务（`./run.sh` 或 `go run cmd/server/main.go`），MCP 端点默认暴露在 `http://<host>:<port>/mcp`。
3. 在 Cursor 内 `Add Custom MCP → HTTP`，将 `Base URL` 设置为 `http://127.0.0.1:8081/mcp`。
4. 也可以在项目根目录创建 `.cursor/mcp.json` 以便团队共享：
   ```json
   {
     "mcpServers": {
       "cyberstrike-ai-http": {
         "transport": "http",
         "url": "http://127.0.0.1:8081/mcp"
       }
     }
   }
   ```


### 知识库功能
- **向量检索**：AI 智能体在对话过程中可自动调用 `search_knowledge_base` 工具搜索知识库中的安全知识。
- **混合检索**：结合向量相似度搜索与关键词匹配，提升检索准确性。
- **自动索引**：扫描 `knowledge_base/` 目录下的 Markdown 文件，自动构建向量嵌入索引。
- **Web 管理**：通过 Web 界面创建、更新、删除知识项，支持分类管理。
- **检索日志**：记录所有知识检索操作，便于审计与调试。

**快速开始（使用预构建知识库）：**
1. **下载知识数据库**：从 [GitHub Releases](https://github.com/Ed1s0nZ/CyberStrikeAI/releases) 下载预构建的知识数据库文件。
2. **解压并放置**：将下载的知识数据库文件（`knowledge.db`）解压后放到项目的 `data/` 目录下。
3. **重启服务**：重启 CyberStrikeAI 服务，知识库即可直接使用，无需重新构建索引。

**知识库配置步骤：**
1. **启用功能**：在 `config.yaml` 中设置 `knowledge.enabled: true`：
   ```yaml
   knowledge:
     enabled: true
     base_path: knowledge_base
     embedding:
       provider: openai
       model: text-embedding-v4
       base_url: "https://api.openai.com/v1"  # 或你的嵌入模型 API
       api_key: "sk-xxx"
     retrieval:
       top_k: 5
       similarity_threshold: 0.7
       hybrid_weight: 0.7
   ```
2. **添加知识文件**：将 Markdown 文件放入 `knowledge_base/` 目录，按分类组织（如 `knowledge_base/SQL注入/README.md`）。
3. **扫描索引**：在 Web 界面中点击"扫描知识库"，系统会自动导入文件并构建向量索引。
4. **对话中使用**：AI 智能体在需要安全知识时会自动调用知识检索工具。你也可以显式要求："搜索知识库中关于 SQL 注入的技术"。

**知识库结构说明：**
- 文件按分类组织（目录名作为分类）。
- 每个 Markdown 文件自动切块并生成向量嵌入。
- 支持增量更新，修改后的文件会自动重新索引。


### 自动化与安全
- **REST API**：认证、会话、任务、监控、漏洞管理等接口全部开放，可与 CI/CD 集成。
- **漏洞管理 API**：通过 `/api/vulnerabilities` 端点管理漏洞：`GET /api/vulnerabilities`（列表，支持过滤）、`POST /api/vulnerabilities`（创建）、`GET /api/vulnerabilities/:id`（获取）、`PUT /api/vulnerabilities/:id`（更新）、`DELETE /api/vulnerabilities/:id`（删除）、`GET /api/vulnerabilities/stats`（统计）。
- **任务控制**：支持暂停/终止长任务、修改参数后重跑、流式获取日志。
- **安全管理**：`/api/auth/change-password` 可即时轮换口令；建议在暴露 MCP 端口时配合网络层 ACL。

## 配置参考

```yaml
auth:
  password: "change-me"
  session_duration_hours: 12
server:
  host: "0.0.0.0"
  port: 8080
log:
  level: "info"
  output: "stdout"
mcp:
  enabled: true
  host: "0.0.0.0"
  port: 8081
openai:
  api_key: "sk-xxx"
  base_url: "https://api.deepseek.com/v1"
  model: "deepseek-chat"
database:
  path: "data/conversations.db"
  knowledge_db_path: "data/knowledge.db"  # 可选：知识库独立数据库
security:
  tools_dir: "tools"
knowledge:
  enabled: false  # 是否启用知识库功能
  base_path: "knowledge_base"  # 知识库目录路径
  embedding:
    provider: "openai"  # 嵌入模型提供商（目前仅支持 openai）
    model: "text-embedding-v4"  # 嵌入模型名称
    base_url: ""  # 留空则使用 OpenAI 配置的 base_url
    api_key: ""  # 留空则使用 OpenAI 配置的 api_key
  retrieval:
    top_k: 5  # 检索返回的 Top-K 结果数量
    similarity_threshold: 0.7  # 相似度阈值（0-1），低于此值的结果将被过滤
    hybrid_weight: 0.7  # 混合检索权重（0-1），向量检索的权重，1.0 表示纯向量检索，0.0 表示纯关键词检索
```

### 工具模版示例（`tools/nmap.yaml`）

```yaml
name: "nmap"
command: "nmap"
args: ["-sT", "-sV", "-sC"]
enabled: true
short_description: "网络资产扫描与服务指纹识别"
parameters:
  - name: "target"
    type: "string"
    description: "IP 或域名"
    required: true
    position: 0
  - name: "ports"
    type: "string"
    flag: "-p"
    description: "端口范围，如 1-1000"
```

## 项目结构

```
CyberStrikeAI/
├── cmd/                 # Web 服务、MCP stdio 入口及辅助工具
├── internal/            # Agent、MCP 核心、路由与执行器
├── web/                 # 前端静态资源与模板
├── tools/               # YAML 工具目录（含 100+ 示例）
├── img/                 # 文档配图
├── config.yaml          # 运行配置
├── run.sh               # 启动脚本
└── README*.md
```

## 基础体验示例

```
扫描 192.168.1.1 的开放端口
对 192.168.1.1 做 80/443/22 重点扫描
检查 https://example.com/page?id=1 是否存在 SQL 注入
枚举 https://example.com 的隐藏目录与组件漏洞
获取 example.com 的子域并批量执行 nuclei
```

## 进阶剧本示例

```
加载侦察剧本：先 amass/subfinder，再对存活主机进行目录爆破。
挂载基于 Burp 的外部 MCP，完成认证流量回放并回传到攻击链。
将 5MB nuclei 报告压缩并生成摘要，附加到对话记录。
构建最新一次测试的攻击链，只导出风险 >= 高的节点列表。
```

## Changelog（近期）
- 2025-12-25 —— 新增漏洞管理功能：完整的漏洞 CRUD 操作，支持跟踪测试过程中发现的漏洞。支持严重程度分级（严重/高/中/低/信息）、状态流转（待确认/已确认/已修复/误报）、按对话/严重程度/状态过滤，以及统计看板。
- 2025-12-25 —— 新增对话分组功能：支持创建分组、将对话移动到分组、分组置顶、重命名和删除等操作，所有分组数据持久化存储到数据库。
- 2025-12-24 —— 重构攻击链生成逻辑，生成速度提升一倍。重构攻击链前端页面展示，优化用户体验。
- 2025-12-20 —— 新增知识库功能：支持向量检索、混合搜索与自动索引，AI 智能体可在对话中自动搜索安全知识。
- 2025-12-19 —— 新增钟馗之眼（ZoomEye）网络空间搜索引擎工具（zoomeye_search），支持 IPv4/IPv6/Web 等资产搜索、统计项查询与灵活的查询参数配置。
- 2025-12-18 —— 优化 Web 前端界面，增加侧边栏导航，提升用户体验。
- 2025-12-07 —— 新增 FOFA 网络空间搜索引擎工具（fofa_search），支持灵活的查询参数与字段配置。
- 2025-12-07 —— 修复位置参数处理 bug：当工具参数使用默认值时，确保后续参数位置正确传递。
- 2025-11-20 —— 支持超大日志/MCP 记录的自动压缩与摘要回写。
- 2025-11-17 —— 上线 AI 驱动的攻击链图谱与风险评分。
- 2025-11-15 —— 提供大结果分页检索与外部 MCP 挂载能力。
- 2025-11-14 —— 工具检索 O(1)、执行记录清理、数据库分页优化。
- 2025-11-13 —— Web 鉴权、Settings 面板与 MCP stdio 模式发布。

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
