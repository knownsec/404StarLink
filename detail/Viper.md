## Viper <https://github.com/FunnyWolf/Viper>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![Author](https://img.shields.io/badge/Author-FunnyWolf-orange)
![GitHub stars](https://img.shields.io/github/stars/FunnyWolf/Viper.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.16-red)
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

#### [v1.5.16] - 2022-02-26

**优化**  
- 优化部分UI,适配Macox  
- 合并metasploit-framework 6.1.32版本  

**Bugfix**  
- 修复伪造成Word文档的exe文件某些情境下无法清理exe问题  
- 修复Python,Java,Android类型Payload无法上线问题

#### [v1.5.15] - 2022-02-13

**优化**  
- 优化部分UI布局  
- 删除Session增加二次确认  
- 通信通道适配大部分Payload  
- 合并metasploit-framework 6.1.30版本  

**Bugfix**  
- 修复手机摄像头拍照MIUI崩溃问题

#### [v1.5.14] - 2022-02-06

**新功能**  
- 新增三个Android教学演示模块(获取目标手机短信/通话记录/通讯录)(手机摄像头拍照)(手机录制音频)  
- 新增通信通道功能,多级内网渗透更加便捷 readme  

**优化**  
- 合并metasploit-framework 6.1.29版本

#### [v1.5.13] - 2022-01-11

**新功能**  
- 新增Zoomeye API接口
- 新增DNSLog服务器模块

**优化**  
- 删除全网扫描debug接口(手工导入功能可完全代替此接口)
- Log4j Payload回显Java version,OS arch,OS version
- 优化全网扫描流水线逻辑,当前不会影响心跳数据传输
- 合并metasploit-framework 6.1.25版本

**Bugfix**  
- 修复VMware Horizon Log4j Rce超时参数不生效问题

#### [v1.5.10] - 2021-12-16

**新功能**  
- 新增Log4j被动扫描功能  
- VIPER+crawlergo组合使用可实现全自动主动扫描Log4j漏洞  

**Log4j被动扫描**  
- 自动替换GET请求参数为Payload  
- 自动替换POST请求参数为Payload  
- 自动替换POST请求JSON中值为Payload  
- 自动替换跳过密码字段  
- 自动在headers中添加Payload(依据字典轮询)  
- Payload包含原始Payload与绕过WAF的Payload  
- Payload中包含UUID,可根据DNSLOG记录查找具体触发漏洞的请求内容  

**Log4j自动化主动扫描**  
- 通过chrome headless + 爬虫的方式获取自动获取页面所有请求,将请求导入到被动proxy中,实现自动化扫描

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
