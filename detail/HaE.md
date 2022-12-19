## HaE <https://github.com/gh0stkey/HaE>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-gh0stkey-orange)
![GitHub stars](https://img.shields.io/github/stars/gh0stkey/HaE.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.4.5-red)
![Time](https://img.shields.io/badge/Join-20210120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


## 项目介绍

**HaE**是基于 `BurpSuite Java插件API` 开发的请求高亮标记与信息提取的辅助型框架式插件，该插件可以通过自定义正则的方式匹配响应报文或请求报文，并对满足正则匹配的报文进行信息高亮与提取。

现代化Web应用走上前后端分离开发模式，这就导致在日常测试时候会有许多的流量，如果你想要尽可能全面的对一个Web应用进行测试评估，将花费大量精力浪费在无用的报文上；**HaE的出现正是为了解决这一类似场景**，借助HaE你可以**有效的减少**测试的时间，将更多的精力放在**有价值、有意义**的报文上，**提高漏洞挖掘效率**。

**注**: 要想灵活的使用`HaE`，你需要掌握正则表达式阅读、编写、修改能力；由于`Java`正则表达式的库并没有`Python`的优雅或方便，所以HaE要求使用者必须用`()`将所需提取的表达式内容包含；例如你要匹配一个**Shiro应用**的响应报文，正常匹配规则为`rememberMe=delete`，如果你要提取这段内容的话就需要变成`(rememberMe=delete)`。

## 使用方法

插件装载: `Extender - Extensions - Add - Select File - Next`

初次装载`HaE`会初始化配置文件，默认配置文件内置一个正则: `Email`，初始化的配置文件会放在的`/用户根目录/.config/HaE/`目录下。

![-w477](https://github.com/gh0stkey/HaE/raw/master/images/show_config.png)

除了初始化的配置文件外，还有`Setting.yml`，该文件用于存储配置文件路径与排除后缀名；`HaE`支持自定义配置文件路径，你可以通过点击`Select File`按钮进行选择自定义配置文件。

## 优势特点

1. **精细化配置项**：高自由度配置更适配精细化场景需求；
2. **简洁可视界面**：简洁的可视化界面让你更加清晰了解HaE的各项配置，操作更轻松，使用更简单；
3. **颜色升级算法**：内置颜色升级算法，避免“屠龙者终成恶龙”场景，突出最具价值的请求；
4. **标签化规则项**：标签化你的正则规则，让规则可分类，让管理更轻松；
5. **数据集合面板**：将所有匹配数据集合到Databoard中，使得测试、梳理更高效；
6. **高亮标记一体**：在Proxy - History页面你可以通过颜色高亮与Comment判断请求价值；
7. **实战化官方库**：基于实战化场景、案例进行输出的官方规则库，提升测试实战性；
8. **配置文件易读**：配置文件使用YAML格式存储，更加便于阅读与修改。

| 界面名称                  | 界面展示                                              |
| ------------------------- | ----------------------------------------------------- |
| Rules（规则信息管理）     | <img src="https://github.com/gh0stkey/HaE/raw/master/images/rules.png" style="width: 80%" />     |
| Config（配置信息管理）    | <img src="https://github.com/gh0stkey/HaE/raw/master/images/config.png" style="width: 80%" />    |
| Databoard（数据集合面板） | <img src="https://github.com/gh0stkey/HaE/raw/master/images/databoard.png" style="width: 80%" /> |



## 实际使用

使用 RGPerson 生成测试数据，放入网站根目录文件中: 

![-w467](https://github.com/gh0stkey/HaE/raw/master/images/16000719723284.jpg)

访问该地址，在`Proxy - HTTP History`中可以看见高亮请求，响应标签页中含有`MarkINFO`标签，其中将匹配到的信息提取了出来。

![-w1047](https://github.com/gh0stkey/HaE/raw/master/images/16000720732854.png)


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v2.4.5] - 2022-12-18

**更新**  
- 在线更新配置信息功能添加提示框, 防止用户误触导致配置被更新  
- 数据聚合查询面板添加支持通配符域名查找  
- 数据聚合查询面板添加清空数据功能, 便于用户查看最新数据  
- 新增规则作用域: any header(请求与响应头)/any body(请求与响应主体)

#### [v2.4.2] - 2022-07-15

**更新**  
- 由于原按钮的鼠标点击监听不灵敏，所以将该监听修改为动作监听  
- 在 issue 发布「HaE公共规则」征集活动  
- 公共规则库新增7条规则

#### [v2.4.1] - 2022-06-29

**更新**  
- 采用全局ArrayList的方式遍历删除Tab，以此应对BurpSuite缓存机制导致的MarkInfo UI错误展示  
- 移除Select File自定义选择配置文件功能，固定配置文件路径，不再支持自定义  
- 新增Online Update功能，单击按钮可在线更新官方配置库

#### [v2.4] - 2022-06-23

**更新**  
- 修复规则导入问题  
- 配置文件初始化默认路径切换到用户根目录/.config/HaE/目录下  
- 新增Databoard功能用于HaE规则匹配数据集中化查询  
- 优化README文档，去除非必要内容，直观展示项目相关信息  
- 发布HaE项目Logo及项目口号：赋能白帽，高效作战！提升项目品牌影响力与辨识度

#### [v2.3] - 2022-05-27

**更新**  
- HaE规则增加sensitive字段，用于NFA引擎正则大小写敏感(更新后建议从HaE规则库中拉取最新规则)  
- 公共规则库增加Dos Paramters、Create Script、Password Field、Username Field规则  
- 兼容性：HaE将同时发布JDK8、9打包的Release版本

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
