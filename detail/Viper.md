## Viper <https://github.com/FunnyWolf/Viper>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![Author](https://img.shields.io/badge/Author-FunnyWolf-orange)
![GitHub stars](https://img.shields.io/github/stars/FunnyWolf/Viper.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.5-red)
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

#### [v1.5.6] - 2021-10-31
**新功能**  
- 新增监听防火墙功能  
- 新增直接windows系统调用规避技术模块  
**优化**  
- reverse_http(s)在网络断开时超时时间从21秒(Windows默认)更新为3秒  
- 当前Session默认用不过期,不会自动退出  
- 合并metasploit-framework 6.1.13版本  
**Bugfix**  
- 修复sessionExpirationTimeout为0时reverse_tcp无法连接问题  
- 修复UI界面无法获取默认lhost参数问题

#### [v1.5.5] - 2021-10-24
**新功能**  
- 新增`CVE-2021-40449提权`模块  
- 新增WebUI一键下载Viper所有日志  
**优化**  
- 合并metasploit-framework 6.1.12版本  
**Bugfix**  
- 修复Socks代理关闭后端口占用问题

#### [v1.5.4] - 2021-10-17
**新功能**  
- 新增MS17-010利用(CSharp)模块  
**优化**  
- 合并metasploit-framework 6.1.11版本  
**Bugfix**  
- 修复重复添加reverse_http(s)监听时无法上线Session问题

#### [v1.5.3] - 2021-10-10
**优化**  
- 登录页面多语言支持
  - 优化 msfconsole 用户体验  
- 合并metasploit-framework 6.1.10版本

#### [v1.5.1] - 2021-09-26
**新功能**  
- 新增`获取互联网出口IP`模块  
- session进程列表新增搜索过滤  
**优化**  
- 杀毒软件显示支持英文版  
- 优化内网扫描模块输出格式  
- 优化`运行模块`功能的性能及UI  
- 合并metasploit-framework 6.1.8版本  
**Bugfix**  
- 修复不显示杀毒软件名称问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
