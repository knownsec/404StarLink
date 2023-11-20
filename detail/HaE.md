## HaE <https://github.com/gh0stkey/HaE>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-gh0stkey-orange)
![GitHub stars](https://img.shields.io/github/stars/gh0stkey/HaE.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.5.8-red)
![Time](https://img.shields.io/badge/Join-20210120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## 项目介绍

**HaE**是一个基于`BurpSuite Java插件API`开发的辅助型框架式插件，旨在实现对HTTP消息的高亮标记和信息提取。该插件通过自定义正则表达式匹配响应报文或请求报文，并对匹配成功的报文进行标记和提取。

随着现代化Web应用采用前后端分离的开发模式，日常漏洞挖掘的过程中，捕获的HTTP请求流量也相应增加。若想全面评估一个Web应用，会花费大量时间在无用的报文上。**HaE的出现旨在解决这类情况**，借助HaE，您能够**有效减少**测试时间，将更多精力集中在**有价值且有意义**的报文上，从而**提高漏洞挖掘效率**。

**注**: 要想灵活的使用`HaE`，你需要掌握正则表达式阅读、编写、修改能力；由于`Java`正则表达式的库并没有`Python`的优雅或方便，所以HaE要求使用者必须用`()`将所需提取的表达式内容包含；例如你要匹配一个**Shiro应用**的响应报文，正常匹配规则为`rememberMe=delete`，如果你要提取这段内容的话就需要变成`(rememberMe=delete)`。

## 使用方法

插件装载: `Extender - Extensions - Add - Select File - Next`

初次装载`HaE`会自动获取官方规则库`https://raw.githubusercontent.com/gh0stkey/HaE/gh-pages/Rules.yml`，配置文件（`Config.yml`）和规则文件（`Rules.yml`）会放在固定目录下：

1. Linux/Mac用户的配置文件目录：`~/.config/HaE/`
2. Windows用户的配置文件目录：`%USERPROFILE%/.config/HaE/`

除此之外，您也可以选择将配置文件存放在`HaE Jar包`的同级目录下的`/.config/HaE/`中，**以便于离线携带**。

### 规则释义

HaE目前的规则一共有6个字段，分别是规则名称、规则正则、规则作用域、正则引擎、规则匹配颜色、规则敏感性。

详细的含义如下所示：

| 字段      | 含义                                                                                                                                                                                                   |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name      | 规则名称，主要用于简短概括当前规则的作用。                                                                                                                                                               |
| Regex     | 规则正则，主要用于填写正则表达式。在HaE中所需提取匹配的内容需要用`(`、`)`将正则表达式进行包裹。                                                                                                            |
| Scope     | 规则作用域，主要用于表示当前规则作用与HTTP报文的哪个部分。                                                                                                                                               |
| Engine    | 正则引擎，主要用于表示当前规则的正则表达式所使用的引擎。**DFA引擎**：对于文本串里的每一个字符只需扫描一次，速度快、特性少；**NFA引擎**：要翻来覆去标注字符、取消标注字符，速度慢，但是特性（如:分组、替换、分割）丰富。 |
| Color     | 规则匹配颜色，主要用于表示当前规则匹配到对应HTTP报文时所需标记的高亮颜色。                                                                                                                               |
| Sensitive | 规则敏感性，主要用于表示当前规则对于大小写字母是否敏感，敏感（`True`）则严格按照大小写要求匹配，不敏感（`False`）则反之。                                                                                      |


## 优势特点

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
| Rules（规则信息管理）     | <img src="https://github.com/gh0stkey/HaE/raw/master/images/rules.png" style="width: 80%" />     |
| Config（配置信息管理）    | <img src="https://github.com/gh0stkey/HaE/raw/master/images/config.png" style="width: 80%" />    |
| Databoard（数据集合面板） | <img src="https://github.com/gh0stkey/HaE/raw/master/images/databoard.png" style="width: 80%" /> |

## 实际使用

使用 RGPerson 生成测试数据，放入网站根目录文件中: 

![-w467](https://github.com/gh0stkey/HaE/raw/master/images/rgperson.jpg)

访问该地址，在`Proxy - HTTP History`中可以看见高亮请求，响应标签页中含有`MarkInfo`标签，其中将匹配到的信息提取了出来。

![-w1047](https://github.com/gh0stkey/HaE/raw/master/images/markinfo.png)


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v2.5.8] - 2023-11-16

**更新**  
- 修复Databoard输入框卡顿问题  
- 修复Databoard消息内容表单数据展示不完全问题

#### [v2.5.7] - 2023-11-13

**更新**  
- 在MarkInfo表单中，新增展示全部数据功能  
- 修复Databoard中双击数据时匹配错误的问题  
- 修复Databoard中清空数据不完全的问题

#### [v2.5.6] - 2023-11-07

**更新**  
- MarkInfo数据提取表单增加搜索框，便于寻找想要的数据信息  
- 数据表单增加#（即ID字段），便于清晰数据展示的具体条数  
- 数据表单增加滑动滚轮加载数据模式，大于3000条则需要滚轮进行加载  
- 消息内容表单过滤超大HTTP消息，当消息包大于3MB时则只截取3MB大小内容返回  
- 修复Databoard数据展示表单监听逻辑错误，不再需要两个TabbedPane进行轮换

#### [v2.5.5] - 2023-10-26

**更新**  
- 优化Databoard匹配数据表单搜索大小写敏感问题  
- 修复Databoard消息内容表单表头排序错乱问题

#### [v2.5.4] - 2023-10-24

**更新**  
- 修复Databoard中HTTP消息内容框自动去重不完整问题  
- 修复BurpSuite暗黑主题下Databoard下拉框消失问题  
- UI界面进行小幅度调整，主要加入了HaE的Logo与标语

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
