## HaE <https://github.com/gh0stkey/HaE>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-gh0stkey-orange)
![GitHub stars](https://img.shields.io/github/stars/gh0stkey/HaE.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.5.0-red)
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

#### [v2.5.0] - 2023-10-12

**功能升级**  
- 将所有匹配到的数据、HTTP请求和响应集中到Databoard中，实现一体化查询功能  
- 在Databoard中支持双击匹配到的数据并展示相应的HTTP报文条目，简化繁琐的搜索过程  

**性能优化**  
- 建立缓存池，利用HTTP请求和响应作为索引来缓存匹配数据，减少重复匹配，提高效率倍速  
- 对于Databoard中的HTTP报文，采用预加载UI显示，在后台线程加载报文，减少超大报文导致的卡顿问题  

**其他改进**  
- 修复了一系列的BUG，包括但不限于Databoard查询数据缺失和通配符查询逻辑缺陷

#### [v2.4.8] - 2023-10-01

**更新**  
- HaE初始化自动加载官方规则库，让用户体验更佳  
- 规则文件层次结构发生变化：rules -> group -> rule -> xxx  
- 优化项目代码、调整项目目录结构，通俗易懂更便于阅读和二次开发  
- Databoard新增`**`查询条件，可以查看所有数据，并以域名的方式单独展示对应数据  
- 命名规范统一化：原`Config.yml`修改为`Rules.yml`，原`Setting.yml`修改为`Config.yml`

#### [v2.4.7] - 2023-09-28

**更新**  
- 新增MarkInfo/Databoard数据展示表单表头排序功能  
- 新增数据匹配量显示功能，作用于Comment及MarkInfo、Databoard数据展示表单  
- 新增Databoard数据查询全量信息，在搜索框中输入*号即可查看HaE匹配到的所有数据  
- 解决Databoard数据全局Map直接引用修改导致数据不全问题  
- 解决Databoard数据存储非二级域名、非域名的模糊条件问题

#### [v2.4.6] - 2023-02-22

**更新**  
- 加入多线程对数据进行匹配和提取，减少卡顿现象  
- 变更配置文件更新地址为jsdelivr的CDN节点地址，优化国内用户体验

#### [v2.4.5] - 2022-12-18

**更新**  
- 在线更新配置信息功能添加提示框, 防止用户误触导致配置被更新  
- 数据聚合查询面板添加支持通配符域名查找  
- 数据聚合查询面板添加清空数据功能, 便于用户查看最新数据  
- 新增规则作用域: any header(请求与响应头)/any body(请求与响应主体)

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
