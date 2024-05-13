## Viper <https://github.com/FunnyWolf/Viper>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![Author](https://img.shields.io/badge/Author-FunnyWolf-orange)
![GitHub stars](https://img.shields.io/github/stars/FunnyWolf/Viper.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.3.0-red)
![Time](https://img.shields.io/badge/Join-20210323-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


- Viper(炫彩蛇)是一款图形化内网渗透工具,将内网渗透过程中常用的战术及技术进行模块化及武器化.
- Viper(炫彩蛇)集成杀软绕过,内网隧道,文件管理,命令行等基础功能.
- Viper(炫彩蛇)当前已集成70+个模块,覆盖初始访问/持久化/权限提升/防御绕过/凭证访问/信息收集/横向移动等大类.
- Viper(炫彩蛇)目标是帮助红队工程师提高攻击效率,简化操作,降低技术门槛.
- Viper(炫彩蛇)支持在浏览器中运行原生msfconsole,且支持多人协作.

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
![image.png](https://cdn.nlark.com/yuque/0/2020/png/159259/1609217723155-f57417f1-2229-4386-888a-c8608449643c.png#align=left&display=inline&height=511&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1022&originWidth=2028&size=296317&status=done&style=none&width=1014)
<br>

# 官网

- [https://www.yuque.com/vipersec](https://www.yuque.com/vipersec)

# 安装

- [安装](https://www.yuque.com/vipersec/help/olg1ua)

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

#### [v2.3.0] - 2024-05-09

**优化**  
* 调整互联网攻击面整体架构  
* 优化网络资产搜索功能  
* 优化互联网攻击面数据存储效率  
* 适配Quake新API接口  

**Bugfix**  
* fix 模块无法使用新建立的监听问题  
* fix 无法使用反溯源  
* fix 主机性能不足时新建监听超时问题

#### [v2.2.1] - 2024-04-21

**新功能**  
- 新增通用配置界面,可以配置网络搜索引擎,wafw00f相关配置  

**优化**  
- 服务状态新增wafw00f检查  
- 未登录时访问导航页自动跳转  
- nuclei支持设置漏洞级别及并发数  
- 更新360 Quake接口  
- 优化wafw00f性能(gevent)  
- 优化模块报错时前端错误提示  
- 解释器更新到python3.12及pip依赖包更新到最新版本  
- 合并metasploit-framework 6.4.6版本  

**Bugfix**  
- fix 扫描模块异常的错误  
- fix 低概率生成C代码时出现编码错误

#### [v2.1] - 2024-03-29

**新功能**  
- 新增通用配置界面,可以配置网络搜索引擎,wafw00f相关配置  

**优化**  
- 优化wafw00f和nuclei的相关接口及模块代码  

**Bugfix**  
- fix `自动化信息收集(通过公司名称)` 结果不全问题

#### [v20231125] - 2023-11-25

**修复**  
- 修复渗透服务连接失败,请检查MSFRPC状态的问题  
- 修复安装完成后访问Web页面时报502错误的问题

#### [v20230924] - 2023-09-24

**新功能**  
- 自动编排新增Session定时任务功能  
- 新增TCPLOG服务器模块  
- 新增Last日志删除模块  

**优化**  
- 前端界面支持OSX的Payload和Handler生成  
- Session展示区域支持伸缩(点击右侧按钮扩大缩小)  
- 合并metasploit-framework 6.3.35版本  

**Bugfix**  
- fix 监听通信通道选择Session后不显示问题  
- fix 内存执行C#可执行文件模块报错问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
