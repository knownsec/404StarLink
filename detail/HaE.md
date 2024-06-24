## HaE <https://github.com/gh0stkey/HaE>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-gh0stkey-orange)
![GitHub stars](https://img.shields.io/github/stars/gh0stkey/HaE.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V3.2.2-red)
![Time](https://img.shields.io/badge/Join-20210120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## 项目介绍

**HaE**是一款网络安全（数据安全）领域下的辅助型框架式项目，旨在实现对HTTP消息（包含WebSocket）的高亮标记和信息提取。本项目通过自定义正则表达式匹配响应报文或请求报文，并对匹配成功的报文进行标记和提取。

> 随着现代化Web应用采用前后端分离的开发模式，日常漏洞挖掘的过程中，捕获的HTTP请求流量也相应增加。若想全面评估一个Web应用，会花费大量时间在无用的报文上。**HaE的出现旨在解决这类情况**，借助HaE，您能够**有效减少**测试时间，将更多精力集中在**有价值且有意义**的报文上，从而**提高漏洞挖掘效率**。

**注意事项**: 

1. 由于HaE 3.0版本开始采用`Montoya API`进行开发，因此使用新版HaE需要升级你的BurpSuite版本（>=2023.12.1）。
2. 由于HaE 2.6版本后对规则字段进行了更新，因此无法适配<=2.6版本的规则，请用户自行前往[规则转换页面](https://gh0st.cn/HaE/ConversionRule.html)进行转换。
3. HaE官方规则库存放在[Github](https://raw.githubusercontent.com/gh0stkey/HaE/gh-pages/Rules.yml)上，因此点击`Update`升级HaE官方规则库时需使用代理（BApp审核考虑安全性，不允许使用CDN）。
4. 自定义HaE规则必须用左右括号`()`将所需提取的表达式内容包含，例如你要匹配一个**Shiro应用**的响应报文，正常匹配规则为`rememberMe=delete`，在HaE的规则中就需要变成`(rememberMe=delete)`。

## 使用方法

插件装载: `Extender - Extensions - Add - Select File - Next`

初次装载`HaE`会自动获取官方规则库`https://raw.githubusercontent.com/gh0stkey/HaE/gh-pages/Rules.yml`，配置文件（`Config.yml`）和规则文件（`Rules.yml`）会放在固定目录下：

1. Linux/Mac用户的配置文件目录：`~/.config/HaE/`
2. Windows用户的配置文件目录：`%USERPROFILE%/.config/HaE/`

除此之外，您也可以选择将配置文件存放在`HaE Jar包`的同级目录下的`/.config/HaE/`中，**以便于离线携带**。

### 规则释义

HaE目前的规则一共有8个字段，详细的含义如下所示：

| 字段      | 含义                                                                                                                                                                                                   |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name      | 规则名称，主要用于简短概括当前规则的作用。                                                                                                                                                               |
| F-Regex     | 规则正则，主要用于填写正则表达式。在HaE中所需提取匹配的内容需要用`(`、`)`将正则表达式进行包裹。|
| S-Regex     | 规则正则，作用及使用同F-Regex。S-Regex为二次正则，可以用于对F-Regex匹配的数据结果进行二次的匹配提取，如不需要的情况下可以留空。|
| Format     | 格式化输出，在NFA引擎的正则表达式中，我们可以通过`{0}`、`{1}`、`{2}`…的方式进行取分组格式化输出。默认情况下使用`{0}`即可。          |
| Scope     | 规则作用域，主要用于表示当前规则作用于HTTP报文的哪个部分。支持请求、响应的行、头、体，以及完整的报文。                                                                                                                                               |
| Engine    | 正则引擎，主要用于表示当前规则的正则表达式所使用的引擎。**DFA引擎**：对于文本串里的每一个字符只需扫描一次，速度快、特性少；**NFA引擎**：要翻来覆去标注字符、取消标注字符，速度慢，但是特性（如:分组、替换、分割）丰富。 |
| Color     | 规则匹配颜色，主要用于表示当前规则匹配到对应HTTP报文时所需标记的高亮颜色。在HaE中具备颜色升级算法，当出现相同颜色时会自动向上升级一个颜色进行标记。                                                                                                                               |
| Sensitive | 规则敏感性，主要用于表示当前规则对于大小写字母是否敏感，敏感（`True`）则严格按照大小写要求匹配，不敏感（`False`）则反之。                                                                                      |


## 优势特点

1. **功能**：通过对HTTP报文的颜色高亮、注释和提取，帮助使用者获取有意义的信息，**聚焦高价值报文**。
2. **界面**：清晰可视的界面设计，以及**简洁的界面交互**，帮助使用者更轻松的了解和配置项目，**避免`多按钮`式的复杂体验**。
3. **查询**：将HTTP报文的高亮、注释和提取到的相关信息**集中在一个数据面板**，可以一键查询、提取信息，从而提高测试和梳理效率。
4. **算法**：内置高亮颜色的升级算法，当出现相同颜色时**会自动向上升级一个颜色**进行标记，**避免`屠龙者终成恶龙`场景**。
5. **管理**：支持对数据的一键导出、导入，以**自定义`.hae`文件的方式**进行项目数据存储，**便于存储和共享项目数据**。
6. **实战**：官方规则库和规则字段作用功能，都是**基于实战化场景总结输出**的，**以此提高数据的有效性、精准性发现**。

| 界面名称                  | 界面展示                                              |
| ------------------------ | ---------------------------------------------------- |
| Rules（规则管理）     | <img src="https://github.com/gh0stkey/HaE/raw/master/images/rules.png" style="width: 80%" />     |
| Config（配置管理）    | <img src="https://github.com/gh0stkey/HaE/raw/master/images/config.png" style="width: 80%" />    |
| Databoard（数据集合） | <img src="https://github.com/gh0stkey/HaE/raw/master/images/databoard.png" style="width: 80%" /> |
| MarkInfo（数据展示） | <img src="https://github.com/gh0stkey/HaE/raw/master/images/markinfo.png" style="width: 80%" /> |

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v3.2.2] - 2024-06-19

**更新**  
- 修复Databoard长时间查询界面错乱问题  
- 修复Databoard在Windows下复制截断问题  
- 修复Databoard查询数据数量随机问题  
- 优化Databoard清空数据逻辑  
- 优化HTTP消息处理逻辑

#### [v3.2.1] - 2024-05-30

**更新**  
* 修复多屏时HaE的信息窗口不跟随问题  
* 修复Databoard删除数据后空数据列表保留问题  
* 优化Databoard数据查询体验，增加底部数据加载等待条  
* 优化Databoard数据导出、导入功能，支持大数据内容的处理

#### [v3.2] - 2024-05-24

**更新**  
* 修复Databoard查询数据缺少问题  
* 修复Databoard删除数据失效问题  
* 优化Config配置数据插入逻辑，支持回车键  
* 新增Databoard数据导出、导入功能

#### [v3.1] - 2024-05-23

**更新**  
* 修复后缀名匹配失效问题  
* 优化HaE MarkInfo调用逻辑，减少UI重复创建  
* 优化缓存池逻辑，基于Caffeine进行生命周期管理  
* 优化HaE初始化逻辑，内置官方规则，初始化将不再依赖于网络  
* 改进HaE Config布局，基于表格方式进行配置信息管理  
* 新增HaE Config配置，可以设置Block host黑名单方式禁止HaE匹配

#### [v3.0.2] - 2024-05-12

**更新**  
* 修复Databoard中当规则作用域为request line/response line时候数据无法定位问题  
* 修复Databoard中数据的查询错乱问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
