## AiPy <https://github.com/knownsec/aipyapp>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-Knownsec-orange)
![GitHub stars](https://img.shields.io/github/stars/knownsec/aipyapp.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.3.0-red)
![Time](https://img.shields.io/badge/Join-20250415-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

# Python use
AIPy 是 Python-use 概念的一个具体实现，旨在展示该理念的实际价值与应用潜力。

使命: 释放大语言模型的全部潜能
愿景: 能够自主改进和使用 AIPy 的更聪明的LLM

## What
Python use 是把整个 Python 执行环境提供给 LLM 使用，可以想象为 LLM 坐在电脑前用键盘在 Python 命令行解释器里输入各种命令，按回车运行，然后观察执行结果，再输入代码和执行。

和 Agent 的区别是 Python use 不定义任何 tools 接口，LLM 可以自由使用 Python 运行环境提供的所有功能。

## Why
假如你是一个数据工程师，你对下面的场景一定不陌生：
- 处理各种不同格式的数据文件：csv/excel，json，html, sqlite, parquet ...
- 对数据进行清洗，转换，计算，聚合，排序，分组，过滤，分析，可视化等操作

这个过程经常需要：
- 启动 Python，import pandas as pd，输入一堆命令处理数据
- 生成一堆中间临时文件
- 找 ChatGPT / Claude 描述你的需要，手工拷贝生成的数据处理代码运行。

所以，为什么不启动 Python 命令行解释器后，直接描述你的数据处理需求，然后自动完成？好处是：
- 无需手工临时输入一堆 Python 命令
- 无需去找 GPT 描述需求，拷贝程序，然后手工运行

这就是 Python use 要解决的问题！

## How
Python use (aipython) 是一个集成 LLM 的 Python 命令行解释器。你可以：
- 像往常一样输入和执行 Python 命令
- 用自然语言描述你的需求，aipython 会自动生成 Python 命令，然后执行

而且，两种模式可以互相访问数据。例如，aipython 处理完你的自然语言命令后，你可以用标准 Python 命令查看各种数据。

## Interfaces
### ai 对象
- \_\_call\_\_(instruction): 执行自动处理循环，直到 LLM 不再返回代码消息
- save(path): 保存交互过程到 svg 或 html 文件
- llm 属性： LLM 对象
- runner 属性： Runner 对象

### LLM 对象
- history 属性： 用户和LLL交互过程的消息历史

### Runner 对象
- globals: 执行 LLM 返回代码的 Python 环境全局变量
- locals: 执行 LLM 返回代码的 Python 环境局部变量

### runtime 对象
供 LLM 生成的代码调用，提供以下接口：
- install_packages(packages): 申请安装第三方包
- getenv(name, desc=None): 获取环境变量
- display(path=None, url=None): 在终端显示图片

## Usage
AIPython 有两种运行模式：
- 任务模式：非常简单易用，直接输入你的任务即可，适合不熟悉 Python 的用户。
- Python模式：适合熟悉 Python 的用户，既可以输入任务也可以输入 Python 命令，适合高级用户。

默认运行模式是任务模式，可以通过 `--python` 参数切换到 Python 模式。

### 任务模式
`uv run aipython`

```
>>> 获取Reddit r/LocalLLaMA 最新帖子
......
......
>>> /done
```

`pip install aipyapp` ，运行aipy命令进入任务模式

```
-> % aipy
🚀 Python use - AIPython (0.1.22) [https://aipy.app]
请输入需要 AI 处理的任务 (输入 /use <下述 LLM> 切换)
>> 获取Reddit r/LocalLLaMA 最新帖子
......
>>
```

### Python 模式
#### 基本用法
自动任务处理：

```
>>> ai("获取Google官网首页标题")
```

#### 自动申请安装第三方库
```
Python use - AIPython (Quit with 'exit()')
>>> ai("使用psutil列出当前MacOS所有进程列表")

📦 LLM 申请安装第三方包: ['psutil']
如果同意且已安装，请输入 'y [y/n] (n): y

```

## Thanks
- 黑哥: 产品经理/资深用户/首席测试官
- Sonnet 3.7: 生成了第一版的代码，几乎无需修改就能使用。
- ChatGPT: 提供了很多建议和代码片段，特别是命令行接口。
- Codeium: 代码智能补齐
- Copilot: 代码改进建议和翻译 README

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v0.3.0] - 2025-10-28

**优化**  
- 优化 MCP 

#### [v0.2.0] - 2025-06-26

**新增**  
- 全新的GUI客户端2.0  
- 集成MCP一键接入功能

#### [v0.1.28] - 2025-05-21

**新增**  
- Trustoken集成联网搜索功能，新闻、时事查询更快捷，平均用时大幅降低。  
- 任务执行完毕自动上传云端私密存储功能，方便用户案例管理或分享精彩案例给他人，该功能可通过配置关闭。  
- Trustoken新增阿里Qwen、腾讯Hunyuan最新模型，多重选择更智能。  
- GUI客户端可通过“aipyw”命令在终端直接打开。  
- GUI客户端可通过“aipyw”命令在终端直接打开。  
**优化**  
- 新用户首次使用引导流程优化，操作体验更便捷。  
- 大幅改善任务拆解、执行逻辑、内置最佳实践方案，执行复杂任务将用时更短、实现方案更可靠。  
- 任务中Python库安装调整为无需确认方式，任务执行过程全自动完成。  
- 修正多处缺陷。  

#### [v0.1.27] - 2025-04-30

**问题修复**  
- 修复界面显示问题  
- 修复代码重构导致的Bug  

#### [v0.1.25] - 2025-04-24

**更新**  
- 增加了 GUI 图形界面  
- 修复产品Bug  
- 提供 Windows 一键运行包

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
