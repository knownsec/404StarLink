## HaE <https://github.com/gh0stkey/HaE>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-gh0stkey-orange)
![GitHub stars](https://img.shields.io/github/stars/gh0stkey/HaE.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V3.0.2-red)
![Time](https://img.shields.io/badge/Join-20210120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## 项目介绍

**HaE**是一款网络安全（数据安全）领域下的辅助型框架式项目，旨在实现对HTTP消息（包含WebSocket）的高亮标记和信息提取。本项目通过自定义正则表达式匹配响应报文或请求报文，并对匹配成功的报文进行标记和提取。

> 随着现代化Web应用采用前后端分离的开发模式，日常漏洞挖掘的过程中，捕获的HTTP请求流量也相应增加。若想全面评估一个Web应用，会花费大量时间在无用的报文上。**HaE的出现旨在解决这类情况**，借助HaE，您能够**有效减少**测试时间，将更多精力集中在**有价值且有意义**的报文上，从而**提高漏洞挖掘效率**。

**注意事项**: 

1. 由于HaE 3.0版本开始采用`Montoya API`进行开发，因此使用新版HaE需要升级你的BurpSuite版本（>=2023.12.1）。
2. 由于HaE 2.6版本后对规则字段进行了更新，因此无法适配<=2.6版本的规则，请用户自行前往[规则转换页面](https://gh0st.cn/HaE/ConversionRule.html)进行转换。
3. HaE官方规则库存放在[Github](https://raw.githubusercontent.com/gh0stkey/HaE/gh-pages/Rules.yml)上，因此默认加载HaE官方规则库需使用代理（BApp审核不允许使用CDN）。
4. 自定义HaE规则必须用左右括号`()`将所需提取的表达式内容包含，例如你要匹配一个**Shiro应用**的响应报文，正常匹配规则为`rememberMe=delete`，在HaE的规则中就需要变成`(rememberMe=delete)`。

### 使用方法

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

### 优势特点

1. 精细配置：高度自由的配置选项，以满足各类精细化场景需求。
2. 分类标签：使用标签对规则进行分类，便于管理和组织规则。
3. 高亮标记：在HTTP History页面，通过颜色高亮和注释判断请求的价值。
4. 易读配置：使用易读的YAML格式存储配置文件，方便阅读和修改。
5. 数据集合：将匹配到的数据、请求和响应集中在数据面板中，提高测试和梳理效率。
6. 简洁可视：清晰可视的界面设计，更轻松地了解和配置HaE，操作简单、使用便捷。
7. 颜色升级：内置颜色升级算法，避免“屠龙者终成恶龙”场景，突出最具价值的请求。
8. 实战规则：官方规则库是基于实战化场景总结输出，提升数据发现的有效性、精准性。

| 界面名称                  | 界面展示                                              |
| ------------------------ | ---------------------------------------------------- |
| Rules（规则管理）     | <img src="https://github.com/gh0stkey/HaE/raw/master/images/rules.png" style="width: 80%" />     |
| Config（配置管理）    | <img src="https://github.com/gh0stkey/HaE/raw/master/images/config.png" style="width: 80%" />    |
| Databoard（数据集合） | <img src="https://github.com/gh0stkey/HaE/raw/master/images/databoard.png" style="width: 80%" /> |
| MarkInfo（数据展示） | <img src="https://github.com/gh0stkey/HaE/raw/master/images/markinfo.png" style="width: 80%" /> |


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v3.0.2] - 2024-05-12

**更新**  
* 修复Databoard中当规则作用域为request line/response line时候数据无法定位问题  
* 修复Databoard中数据的查询错乱问题

#### [v3.0.1] - 2024-05-09

**更新**  
* 修复因HaE导致的BurpSuite整体卡顿问题  
* 修复HaE的MarkInfo复制数据失效问题  
* 新增HaE规则作用域2个分别是：请求行(request line)、响应行(response line)

#### [v3.0.0] - 2024-05-06

**更新**  
* 基于Montoya API进行重构，完美支持BurpSuite新版本  
* 新增Databoard端口形式的数据查询，为80/443端口则不显示  
* 新增对Websocket消息的HaE功能作用，支持高亮、注释、数据展示  
* 删除Databoard中**双星号形式的数据查询功能  
* 新版HaE需要升级你的BurpSuite版本(>=2023.12.1)

#### [v2.6.1] - 2024-03-22

**更新**  
- 修复DFA模式下数据提取错位问题  
- 修复DFA模式下中文不匹配问题

#### [v2.6.0] - 2024-02-02

**更新**  
- 支持双正则匹配，第一次正则(F-Regex)匹配结果可以通过第二次正则(S-Regex)进行二次匹配  
- 支持格式化输出，在NFA引擎的正则表达式中，我们可以通过`{0}、{1}、{2}…`的方式进行取分组格式化输出  
- DFA引擎支持大小写敏感配置项(即Sensitive可为Flase/True)，有效减少正则长度  

**修复**  
- 修复Databoard面板展示UI的布局大小失效BUG

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
