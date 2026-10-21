## CyberStrikeAI <https://github.com/Ed1s0nZ/CyberStrikeAI>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-go-blue)
![Author](https://img.shields.io/badge/Author-Ed1s0nZ-orange)
![GitHub stars](https://img.shields.io/github/stars/Ed1s0nZ/CyberStrikeAI.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.7.24-red)
![Time](https://img.shields.io/badge/Join-20251229-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->





<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.7.24] - 2026-10-16
本次更新重点优化了长任务执行、上下文恢复和用量统计的可靠性：修复摘要达到输出上限、历史工具参数格式异常导致的对话中断；解决上下文压缩后证据难以追溯、恢复任务时遗漏已有脚本和测试结论的问题，减少重复探索；修复缓存写入 Token 在流式响应、持久化和汇总过程中丢失、DeepSeek 缓存命中用量未正确识别等统计问题，并完善去重及总量缺失时的计算逻辑，新增用量明细与趋势展示。同时修复移动端项目页面遮挡、滚动受限和表格重叠，以及并发创建资产时的数据库锁冲突。

---

This update improves the reliability of long-running tasks, context recovery, and usage tracking. It fixes conversation interruptions caused by summary output limits and malformed historical tool arguments, preserves retrievable evidence after context compaction, and restores existing scripts and test outcomes when resuming tasks to reduce repeated work. It also fixes missing cache-write token counts across streaming, persistence, and aggregation, corrects DeepSeek cache-hit reporting, and improves usage deduplication and total-token fallback calculations, alongside detailed usage views and trends. Additional fixes address overlapping mobile layouts, inaccessible content and cramped tables, as well as database lock conflicts during concurrent asset creation.

#### [v1.7.11] - 2026-07-28
将最终回复从“模型文本判断”升级为“结构化 finalization 协议 + 显式执行证据策略”，避免过程输出误当结论。

#### [v1.6.47] - 2026-06-27
修复同一对话中重复发送相同用户提示词时，因历史去重逻辑误判而不再追加本轮 user 消息、导致请求以 assistant 结尾并触发 Claude 4.6+ 返回 400（assistant-prefill final message is not supported）的问题；现仅在尾部已是相同 user 内容时才跳过追加，重复提示词可正常续聊。

#### [v1.3.23] - 2026-03-10

 - 更新 config.yaml


#### [v0.0.11] - 2025-12-28


<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
