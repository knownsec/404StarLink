## antSword <https://github.com/AntSwordProject/antSword>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Nodejs-blue)
![Author](https://img.shields.io/badge/Author-AntSwordProject-orange)
![GitHub stars](https://img.shields.io/github/stars/AntSwordProject/antSword.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1.15-red)
![Time](https://img.shields.io/badge/Join-20201120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


> 一剑在手，纵横无忧！

**中国蚁剑是一款开源的跨平台网站管理工具，它主要面向于合法授权的渗透测试安全人员以及进行常规操作的网站管理员。**    
**任何人不得将其用于非法用途以及盈利等目的，否则后果自行承担并将追究其相关责任！**

[English][url-docen] / [文档][url-document] / [更新日志][url-changelog]

## 开发栈
 - [Electron][url-electron]
 - [ES6][url-es6]
 - [dhtmlx][url-dhtmlx]
 - [Nodejs][url-nodejs]
 * 以及其他在项目中调用到的库

中国蚁剑推崇模块化的开发思想，遵循**开源，就要开得漂亮**的原则，致力于为不同层次的人群提供最简单易懂、方便直接的代码展示及其修改说明，努力让大家可以一起为这个项目贡献出力所能及的点滴，让这款工具真正能让大家用得顺心、舒适，让它能为大家施展出最人性化最适合你的能力！

## 软件截图

![][url-mainui]

<details>

<summary>更多截图</summary>

![][url-filemanager]
![][url-terminal]
![][url-database]
![][url-pluginstore]

</details>

## 快速入门

参见文档 [快速入门][url-quickstart]

## 如何贡献

参见文档 [支持蚁剑][url-contribute]

## 致敬感谢
> 中国蚁剑的核心代码模板均改自伟大的**中国菜刀**，在此向作者感谢以及致敬！致敬每一位为网络安全做出点滴贡献的新老前辈！

**一路走来，得到了很多朋友的参与开发以及点滴赞助，在此感谢陪伴，感谢你们能让它越走越远！**

[url-docen]: https://github.com/AntSwordProject/antSword/blob/master/README.md
[url-changelog]: https://github.com/AntSwordProject/antSword/blob/master/CHANGELOG.md
[url-document]: https://www.yuque.com/antswordproject/antsword/
[url-release]: https://github.com/AntSwordProject/AntSword/releases/
[url-electron]: http://electron.atom.io/
[url-es6]: http://es6.ruanyifeng.com/
[url-dhtmlx]: http://dhtmlx.com/
[url-nodejs]: https://nodejs.org/
[url-homepage]: http://uyu.us
[url-release]: https://github.com/AntSwordProject/AntSword/releases
[url-quickstart]: https://www.yuque.com/antswordproject/antsword/lmwppk
[url-contribute]: https://doc.u0u.us/zh-hans/contribute_docs.html
[url-mainui]: https://cdn.nlark.com/yuque/0/2021/png/1592179/1611820109032-b563426e-015c-4afe-a905-70e878fdcdb6.png
[url-filemanager]: https://cdn.nlark.com/yuque/0/2021/png/1592179/1611823243564-26e964c2-6d38-421a-8543-5f1f082a6bbd.png
[url-terminal]: https://cdn.nlark.com/yuque/0/2021/png/1592179/1611823538382-50fba630-3bd9-4205-b5dd-9cc054da79a8.png
[url-database]: https://cdn.nlark.com/yuque/0/2021/png/1592179/1611825612518-ca1c4fcc-98a6-4fa3-b55d-f25619c86380.png
[url-pluginstore]: https://cdn.nlark.com/yuque/0/2021/png/1592179/1611907520850-040bffb1-5bc3-4c1c-a8d1-1e69712f7684.png

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2022-07-18 发布文章[《AntSword v2.1.15 更新汇总》](https://mp.weixin.qq.com/s/QzbREMp8JaQiP9qo48OyHg)
- 2021-11-15 发布文章[《蚁剑绕WAF进化图鉴》](https://mp.weixin.qq.com/s/EYP1ANj7pxM8_NX_7R9WjA)

## 最近更新

#### [v2.1.15] - 2022-07-17

**核心**  
- 修复 PHP/PHP4 当前目录不可写时 bypass open_basedir 失败的 Bug  
- 新增 PHPRAW/ASPXCSharp/PSWindows 类型  

**数据管理**  
- 修复 JSP/MySQL类型在表名中有特殊字符时执行异常的 Bug  
- 新增配置选项「Body 设置为 RAW 模式」  

**文件管理**  
- 新增 FileHash 计算目标文件 hash 功能  

**后端模块**  
- 支持自定义 Content-Type, 默认是 form  
- 支持 WebSocket 连接  

**设置模块**  
- 优化全局代理设置  

**其他**  
- 更多详细更新内容，见 release v2.1.15  


<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
