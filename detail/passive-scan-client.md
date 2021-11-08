## passive-scan-client <https://github.com/c0ny1/passive-scan-client>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-c0ny1-orange)
![GitHub stars](https://img.shields.io/github/stars/c0ny1/passive-scan-client.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.3.0-red)
![Time](https://img.shields.io/badge/Join-20210120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


## Burp被动扫描流量转发插件


### 0x01 插件简介

```
Q1: 将浏览器代理到被动扫描器上，访问网站变慢，甚至有时被封ip，这该怎么办？
Q2: 需要人工渗透的同时后台进行被动扫描，到底是代理到burp还是被动扫描器？
Q3: ......
```

该插件正是为了解决该问题，将`正常访问网站的流量`与`提交给被动扫描器的流量`分开，互不影响。

![流程图](https://github.com/c0ny1/passive-scan-client/raw/master/doc/process.png)

### 0x02 插件编译

```
mvn package
```

### 0x03 插件演示

可以通过插件将流量转发到各种被动式扫描器中，这里我选`xray`来演示.

![动图演示](https://github.com/c0ny1/passive-scan-client/raw/master/doc/show.gif)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
