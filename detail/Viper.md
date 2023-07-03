## Viper <https://github.com/FunnyWolf/Viper>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![Author](https://img.shields.io/badge/Author-FunnyWolf-orange)
![GitHub stars](https://img.shields.io/github/stars/FunnyWolf/Viper.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.6.0-red)
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


## 最近更新

#### [v1.6.0] - 2023-07-01

**优化**  
- 优化反溯源方案  
- 优化内存执行C#可执行文件(Bypass)模块  
- 关于VIPER中可以快捷查看最新版本  
- 合并metasploit-framework 6.3.24版本

#### [v1.5.30] - 2023-06-17

**新功能**  
- Viper所有功能都可通过右下角链接跳转到对应文档  

**优化**  
- 监听防火墙前端UI优化  
- 只显示Session功能可在主页面使用  
- 合并metasploit-framework 6.3.22版本  

**Bugfix**  
- 修复python类型payload断线后无法重连及无法清理历史网络连接问题

#### [v1.5.29] - 2023-05-22

**优化**  
- 端口转发记录新增连接提示  
- 模块运行结果记录运行模块的sessionid  
- 适配reverse_tcp_ssl类型payload  
- 合并metasploit-framework 6.3.18版本  

**Bugfix**  
- 修复sock4a/socks5代理无法使用问题  
- 修复session长时间运行导致内存占用过高问题

#### [v1.5.28] - 2023-05-06

**新功能**  
- 新增只显示Session功能(首页和网络拓扑更简洁)  
- 面向互联网的handler被扫描(网络测绘)时会在Notice提示  

**优化**  
- 合并metasploit-framework 6.3.16版本  

**Bugfix**  
- 修复无法修改包含中文内容的文件问题  
- 修复文件管理无法上传文件问题

#### [v1.5.27] - 2023-04-29

**新功能**  
- 新增基础LoaderShellcode分离免杀(Linux)模块  

**优化**  
- 合并metasploit-framework 6.3.15版本

**Bugfix**  
- 修复Python类型payload无法上线问题
- 修复命令终端输出中文报错问题(提示执行超时)
- 修复Session通信信道功能无法使用问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
