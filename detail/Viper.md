## Viper <https://github.com/FunnyWolf/Viper>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JS/Python-blue)
![Author](https://img.shields.io/badge/Author-FunnyWolf-orange)
![GitHub stars](https://img.shields.io/github/stars/FunnyWolf/Viper.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V20230831-red)
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

#### [v20230831] - 2023-08-31

**优化**  
- 清除不需要的日志,提高系统运行速度  
- 优化docker logs日志,存储到日志目录便于问题定位  
- docker healthcheck当前检查所有后台服务  

**Bugfix**  
- 修复python payload在心跳发送失败时不会记录错误的问题  
- 修复thin的pid文件未清除的问题

#### [v20230827] - 2023-08-28

**优化**  
- 反溯源脚本nobody.sh可以快速使用初始nginx配置  
- 合并metasploit-framework 6.3.32版本  
- Viper后续使用构建时间作为版本号  

**Bugfix**  
- 修复Session心跳显示999,msfrpc状态正常,界面显示渗透服务心跳异常  
- 修复session文件下载报错的问题  
- 修复多次重启后会重复添加缓存的监听的问题

#### [v1.6.4] - 2023-08-21

**新功能**  
- 新增判断Session是否运行在容器中模块  

**优化**  
- session通过鼠标提示展示英文的地理位置信息  
- Viper通过CI自动更新Geolite数据库  
- Viper当前通过CI自动构建  
- 优化模块运行部分前端提示信息  
- 优化viperpython日志格式  
- 提高运行信息执行速度  
- 渗透服务异常时日志更详细说明异常类型  
- 合并metasploit-framework 6.3.31版本  

**Bugfix**  
- 修复Session心跳显示999,msfrpc状态正常,界面显示渗透服务心跳异常  
- 修复session下载文件时会偶发性的下载了1m中断  
- 修复已经上线的session界面未显示  
- 修复日志逻辑问题

#### [v1.6.3] - 2023-08-12

**优化**  
- 调整vipermsf及viperpython日志级别及格式,便于定位问题  
- 关闭vipermsf的cpulimit  
- 新增vipermsf心跳异常提示  
- 更新沙箱IP列表  
- 优化网络拓扑动态效果  
- 合并metasploit-framework 6.3.30版本  

**Bugfix**  
- 修复session下载文件时会偶发性的下载了1m中断  
- 修复thin的pid文件未清除导致重启msf后台服务无法启动

#### [v1.6.2] - 2023-08-02

**优化**  
- 优化Session Timeout默认值,断线可自动切换传输协议  
- reverse_http监听不再返回404页面,直接关闭连接  
- 优化网络拓扑,根据载荷类型确认方向并动态显示当前存活的连接  
- 合并metasploit-framework 6.3.28版本  

**Bugfix**  
- Socks5代理在存在连接时无法正确关闭问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
