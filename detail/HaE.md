## HaE <https://github.com/gh0stkey/HaE>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-gh0stkey-orange)
![GitHub stars](https://img.shields.io/github/stars/gh0stkey/HaE.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.1.2-red)
![Time](https://img.shields.io/badge/Join-20210120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


# HaE - Highlighter and Extractor

核心功能作者: [@EvilChen](https://github.com/gh0stkey)

架构作者: [@0chencc](https://github.com/0Chencc)

## 公共规则网站

https://gh0st.cn/HaE/

## 介绍

**HaE**是基于 `BurpSuite` 插件 `JavaAPI` 开发的请求高亮标记与信息提取的辅助型插件。

![-w1070](https://github.com/gh0stkey/HaE/raw/master/images/16000706401522.jpg)

该插件可以通过自定义正则的方式匹配**响应报文或请求报文**，可以自行决定符合该自定义正则匹配的相应请求是否需要高亮标记、信息提取。

**注**: `HaE`的使用，对测试人员来说需要基本的正则表达式基础，由于`Java`正则表达式的库并没有`Python`的优雅或方便，在使用正则的，HaE要求使用者必须使用`()`将所需提取的表达式内容包含；例如你要匹配一个**Shiro应用**的响应报文，正常匹配规则为`rememberMe=delete`，如果你要提取这段内容的话就需要变成`(rememberMe=delete)`。

## 使用方法

插件装载: `Extender - Extensions - Add - Select File - Next`

初次装载`HaE`会初始化配置文件，默认配置文件内置一个正则: `Email`，初始化的配置文件会放在与`BurpSuite Jar`包同级目录下。

除了初始化的配置文件外，还有`Setting.yml`，该文件用于存储配置文件路径；`HaE`支持自定义配置文件路径，你可以通过点击`Select File`按钮进行选择自定义配置文件。

![-w477](https://github.com/gh0stkey/HaE/raw/master/images/16000710069404.jpg)

## 插件优点

1. 多选项自定义控制适配需求
2. 多颜色高亮分类，将BurpSuite的所有高亮颜色集成: `red, orange, yellow, green, cyan, blue, pink, magenta, gray`
3. **颜色升级算法**: 利用下标的方式进行优先级排序，当满足2个同颜色条件则以优先级顺序上升颜色（例如: **两个正则，颜色为橘黄色，该请求两个正则都匹配到了，那么将升级为红色**）
4. 配置文件采用YAML格式存储，更加便于阅读和修改
5. 内置简单缓存，在“多正则、大数据”的场景下减少卡顿现象
6. **支持标签分页**，点击`...`即可添加新的标签页，对着标签页右键即可删除
7. 高亮信息添加的同时添加Comment，便于查找请求

![-w477](https://github.com/gh0stkey/HaE/raw/master/images/16000720732851.jpg)

## 实际使用

使用 RGPerson 生成测试数据，放入网站根目录文件中: 

![-w467](https://github.com/gh0stkey/HaE/raw/master/images/16000719723284.jpg)

访问该地址，在`Proxy - HTTP History`中可以看见高亮请求，响应标签页中含有`MarkINFO`标签，其中将匹配到的信息提取了出来。

![-w1047](https://github.com/gh0stkey/HaE/raw/master/images/16000720732854.jpg)


## 正则优化

有些正则在实战应用场景中并不理想

在正则匹配手机号、身份证号码的时候（纯数字类）会存在一些误报（这里匹配身份证号码无法进行校验，误报率很高），但手机号处理这一块可以解决: 

原正则: 

```
1[3-9]\d{9}
```

误报场景: `12315188888888123`，这时候会匹配到`15188888888`，而实际上这一段并不是手机号，所以修改正则为: 

```
[^0-9]+(1[3-9]\d{9})[^0-9]+
```

也就是要求匹配的手机号前后不能为0-9的数字。

## 实战用法

1. CMS指纹识别，Discuz正则: `(Powered by Discuz!)`
2. OSS对象存储信息泄露，正则: `([A|a]ccess[K|k]ey[I|i]d|[A|a]ccess[K|k]ey[S|s]ecret)`
3. 内网地址信息提取，正则: `(?:10\.\d{1,3}\.\d{1,3}\.\d{1,3})|(?:172\.(?:(?:1[6-9])|(?:2\d)|(?:3[01]))\.\d{1,3}\.\d{1,3})|(?:192\.168\.\d{1,3}\.\d{1,3})`
4. 实战插件关联搭配，漏洞挖掘案例: https://mp.weixin.qq.com/s/5vNn7dMRZBtv0ojPBAHV7Q

...还有诸多使用方法等待大家去发掘。

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v2.1.2] - 2021-10-22
**优化**  
- 修复/规避一些微不足道的BUG  
- 优化/合并冗余代码  
- 补2.1.1未说明的功能：排除后缀不再仅仅作用于请求报文，也会与Burp的MIME进行匹配作用响应报文

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
