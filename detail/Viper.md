## Viper <https://github.com/FunnyWolf/Viper>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![Author](https://img.shields.io/badge/Author-FunnyWolf-orange)
![GitHub stars](https://img.shields.io/github/stars/FunnyWolf/Viper.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V3.0.0-red)
![Time](https://img.shields.io/badge/Join-20210323-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

- Viper(炫彩蛇)是一款图形化互联网攻击面管理&红队模拟平台.
- Viper(炫彩蛇)覆盖红队模拟的常用功能(杀软绕过,内网隧道,文件管理,命令行等).
- Viper(炫彩蛇)红队模拟当前已集成100+个模块,覆盖MITRE ATT&CK的所有战术大类.
- Viper(炫彩蛇)红队模拟支持基于LLM的智能体,用户可以用自然语言调用系统功能.
- Viper(炫彩蛇)攻击面管理支持备案\域名\IP\公众号小程序\CDN\WAF\漏洞等采集及管理功能.
<br>

![image.png](https://cdn.nlark.com/yuque/0/2021/png/159259/1631687579184-a2603220-9009-4240-9709-76b503fe8174.png?x-oss-process=image%2Fresize%2Cw_1504%2Climit_0)
<br>
<br>
<br>
![image.png](https://cdn.nlark.com/yuque/0/2021/png/159259/1628573079014-871d0573-ef2a-4267-974b-1026d6ed2466.png?x-oss-process=image%2Fresize%2Cw_1504%2Climit_0)
<br>
<br>
<br>
![image.png](https://cdn.nlark.com/yuque/0/2020/png/159259/1609217703998-8bebe969-7a26-4f75-b2cb-6dca34a39951.png#align=left&display=inline&height=511&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1022&originWidth=2028&size=191127&status=done&style=none&width=1014)
<br>
<br>
<br>
![image.png](https://cdn.nlark.com/yuque/0/2024/png/159259/1725593479768-b315a2a1-596d-4407-84a9-d643751c7520.png?x-oss-process=image%2Fformat%2Cwebp)
<br>

# 官网

- [https://www.yuque.com/vipersec](https://www.yuque.com/vipersec)

# 安装

- [安装](https://www.yuque.com/vipersec/help/olg1ua)

# 友情链接

[使用Cloudflare Argo隐藏VIPER后台](https://tokisaki.top/blog/viper-via-cloudflare-argo/)

[msf http使用cloudflare argo上线](https://tokisaki.top/blog/meterpreter-via-cloudflare-argo/)

# 常见问题

- [FAQ](https://www.yuque.com/vipersec/faq)

# 问题反馈

- github issues : [https://github.com/FunnyWolf/Viper/issues](https://github.com/FunnyWolf/Viper/issues)

# 模块列表

- [文档链接](https://www.yuque.com/vipersec/module)

# 系统架构图

![viper.png](https://cdn.nlark.com/yuque/0/2021/png/159259/1627364231093-768d3b07-e044-4a2d-a3fa-e9ebd92a0828.png)

# 开发手册

- [开发手册](https://www.yuque.com/vipersec/code)

# 源代码

- viperjs (前端)

[https://github.com/FunnyWolf/viperjs](https://github.com/FunnyWolf/viperjs)

- viperpython (后台)

[https://github.com/FunnyWolf/viperpython](https://github.com/FunnyWolf/viperpython)

- vipermsf (渗透服务)

[https://github.com/FunnyWolf/vipermsf](https://github.com/FunnyWolf/vipermsf)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2023-02-14 发布演示视频[404星链计划开源安全工具演示——Viper](https://www.bilibili.com/video/BV1zv4y1s7xv)

## 最近更新

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

#### [v2.3.1] - 2024-07-08

**新功能**  
- 新增V-GPT,AI驱动的攻击型智能体框架  
- 新增数据分析智能体 数据分析多角色智能体模块  
- 新增OpenAI集成  

**优化**  
- 调整平台设置部分UI

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
