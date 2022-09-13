## Viper <https://github.com/FunnyWolf/Viper>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![Author](https://img.shields.io/badge/Author-FunnyWolf-orange)
![GitHub stars](https://img.shields.io/github/stars/FunnyWolf/Viper.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.24-red)
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

#### [v1.5.24] - 2022-09-11

**新功能**  
- 新增UI提示框获取用户输入的密码模块  

**优化**  
- mitmproxy开放公网访问,添加http代理认证  
- msfrpc web组件由puma替换为thin,减少cpu占用  
- msfrpc默认开启cpulimit 50%  
- msfrpc使用OJ为默认json组件,替换yajl  
- 更新Django 4.0  
- 合并metasploit-framework 6.2.18版本

#### [v1.5.23] - 2022-08-07

**优化**  
- 合并 metasploit-framework 6.2.12版本  

**Bugfix**  
- 修复yajl-ruby bug导致的渗透服务无响应问题  
- 修复msf cpu占用100%问题  
- 修复内存占用过高问题

#### [v1.5.21] - 2022-05-21

**优化**  
- 更新内网代理提示  
- 优化被动扫描模块加载逻辑,提高性能  
- 合并metasploit-framework 6.1.44版本  

**Bugfix**  
- FOFA报错问题issues#87

#### [v1.5.19] - 2022-03-28

**优化**  
- Session文件管理增加缓存,优化首次打开速度  
- 合并metasploit-framework 6.1.36版本  

**Bugfix**  
- 修复无法使用migrate命令问题  
- 修复无法创建虚拟监听问题  
- 修复Windows UAC绕过运行报错问题

#### [v1.5.18] - 2022-03-11

**优化**  
- Viper重启后不再自动加载历史监听,而是生成对应的虚拟监听并加入备份标签,便于用户手动恢复  
- 调用jemalloc编译ruby解释器,优化MSF内存占用  
- 合并metasploit-framework 6.1.34版本  

**Bugfix**  
- 修复reverse_https监听关闭后端口占用问题  
- to_handler生成的监听当前在WEBUI正确显示

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
