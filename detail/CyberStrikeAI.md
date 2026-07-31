## CyberStrikeAI <https://github.com/Ed1s0nZ/CyberStrikeAI>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-go-blue)
![Author](https://img.shields.io/badge/Author-Ed1s0nZ-orange)
![GitHub stars](https://img.shields.io/github/stars/Ed1s0nZ/CyberStrikeAI.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.7.11-red)
![Time](https://img.shields.io/badge/Join-20251229-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->





<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.7.11] - 2026-07-28
将最终回复从“模型文本判断”升级为“结构化 finalization 协议 + 显式执行证据策略”，避免过程输出误当结论。

#### [v1.6.47] - 2026-06-27
修复同一对话中重复发送相同用户提示词时，因历史去重逻辑误判而不再追加本轮 user 消息、导致请求以 assistant 结尾并触发 Claude 4.6+ 返回 400（assistant-prefill final message is not supported）的问题；现仅在尾部已是相同 user 内容时才跳过追加，重复提示词可正常续聊。

#### [v1.3.23] - 2026-03-10

 - 更新 config.yaml


#### [v0.0.11] - 2025-12-28


<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
