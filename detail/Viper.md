## Viper <https://github.com/FunnyWolf/Viper>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![Author](https://img.shields.io/badge/Author-FunnyWolf-orange)
![GitHub stars](https://img.shields.io/github/stars/FunnyWolf/Viper.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V3.1.1-red)
![Time](https://img.shields.io/badge/Join-20210323-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

<p align="center">
  <img src="https://github.com/FunnyWolf/Viper/raw/master/docs/public/viper.svg" alt="Viper Icon" width="200">
</p>

**VIPER** 是一个强大且灵活的红队平台.平台集成对手模拟及红队行动所需的核心工具和功能,帮助您高效完成网络安全评估工作。

- **直观的操作界面**

  提供易于上手的用户界面，使得红队成员可以迅速开始他们的安全评估任务。

- **多平台支持**

  支持针对多种操作系统进行红队评估，包括 Windows、Linux 和 macOS。

- **开箱即用的红队工具**

  功能设计涵盖了 MITRE ATT&CK 框架的所有阶段，为用户提供了一个全面的攻击模拟解决方案。

- **集成 LLM Agent**

  内置大型语言模型智能体，增强自动化处理能力和智能决策支持。

- **自动化工作流程**

  支持自动化的编排和通知机制，使红队能够全天候监控目标状态。

- **多样化的模块**

  集成后渗透模块、被动扫描模块以及全网扫描模块在内的多种类型，满足不同场景下的需求。

- **自定义扩展能力**

  支持通过 Python 编写自定义模块，满足特定需求或添加额外功能。

- **攻击面管理（Beta）**

  引入攻击面管理功能，帮助团队更好地识别和理解目标企业潜在的风险点。

![img.webp](https://github.com/FunnyWolf/Viper/raw/master/docs/zh/guide/webp/img.webp)
![img_1.webp](https://github.com/FunnyWolf/Viper/raw/master/docs/zh/guide/webp/img_1.webp)
![img_2.webp](https://github.com/FunnyWolf/Viper/raw/master/docs/zh/guide/webp/img_2.webp)
![img_3.webp](https://github.com/FunnyWolf/Viper/raw/master/docs/zh/guide/webp/img_3.webp)
![img_4.webp](https://github.com/FunnyWolf/Viper/raw/master/docs/zh/guide/webp/img_4.webp)
![img_5.webp](https://github.com/FunnyWolf/Viper/raw/master/docs/zh/guide/webp/img_5.webp)

## 官方网站

[https://www.viperrtp.com/zh/](https://www.viperrtp.com/zh/)

## 问题反馈

[https://github.com/FunnyWolf/Viper/issues](https://github.com/FunnyWolf/Viper/issues)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2023-02-14 发布演示视频[404星链计划开源安全工具演示——Viper](https://www.bilibili.com/video/BV1zv4y1s7xv)

## 最近更新

#### [v3.1.1] - 2025-03-30

**更新**  
- 新的官方网站 [viperrtp.com] ，并支持从DockerHub获取镜像。  
- AI Agent更新，现在可以添加多个符合OpenAI标准的key，并根据模型Tag赋予不同的任务，详情见项目Release。  

**优化**  
- 平台现在默认过滤支持多级控制的有效载荷，增强稳定性。  
- 更新了一些 i18n 和文档链接。

#### [v3.0.0] - 2024-12-10

**新功能**  
- screen_share功能支持web端直接预览  
- 攻击面管理新增备案 Favicon等功能  
- viper被暴力破解时自动阻止登陆  

**优化**  
- 更新AI模块提示词  
- 攻击面管理数据存储由sqlite切换为elasticsearch  
- 更新后台服务启动顺序,添加启动失败原因日志  
- 合并metasploit-framework 6.4.40版本

#### [v2.3.5] - 2024-09-29

**新功能**  
- webcam_stream功能支持web端直接预览  

**优化**  
- OPENAI支持输入自定义模型名称  
- OPENAI未配置时错误提示更为友好  
- 获取互联网出口IP模块API为https://ipwho.is/  
- 邮件生成/发送智能体 平台操作智能体提示词更新,引入CoT及Role Play

#### [v2.3.4] - 2024-09-06

**新功能**  
- 新增多用户功能,支持多人协作  

**优化**  
- 智能助手支持Markdown格式输出及展示

#### [v2.3.2] - 2024-08-05

**新功能**  
- 新增SMTP配置,用于发送邮件  
- 数据分析多角色智能体支持session/handler相关信息查询分析 
- 数据分析多角色智能体支持meterpreter相关操作(摄像头/截屏/键盘记录/查看文件)  
- 新增邮件生成/发送智能体,可以根据用户简单描述生成完整的邮件并发送  

**优化**  
- 部分按钮UI调整  
- OpenAI新增gpt-4o-mini模型  
- 渗透服务状态检查新增心跳功能检测  
- 互联网攻击面管理的worker代码合并到主分支  

**Bugfix**  
- fix 部分界面抖动问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
