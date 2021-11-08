## frida-skeleton <https://github.com/Margular/frida-skeleton>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-Margular-orange)
![GitHub stars](https://img.shields.io/github/stars/Margular/frida-skeleton.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.0.0-red)
![Time](https://img.shields.io/badge/Join-20201221-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


### 简介

`frida-skeleton`是基于frida的安卓hook框架，提供了很多frida自身不支持的功能，将hook安卓变成简单便捷，人人都会的事情，主要有：

- 根据正则表达式批量hook安卓应用，支持多线程，可同时hook多个设备互不影响
- 针对不同的应用可以同时加载不同的hook脚本，且支持优先级配置
- 自动将手机上的所有TCP流量重定向到PC上的抓包工具如BurpSuite，无需手动配置，且自动绕过证书绑定机制
- 丰富的日志记录功能，让你的hook历史永不丢失
- 自动识别当前使用的frida版本并下载对应版本的frida-server到/data/local/tmp运行
- 提供封装好的实用API以减少日常工作中的重复劳动

### 上手指南

###### 开发前的配置要求

- Python3

###### 安装步骤

1. 克隆本项目到本地

```sh
git clone https://github.com/Margular/frida-skeleton.git
```

2. 安装第三方依赖库

```sh
pip install -r requirements.txt
```

###### 查看说明

```sh
python frida-skeleton.py -h
```

详细说明请移步[WIKI](https://github.com/Margular/frida-skeleton/wiki)

### 文件目录说明

```
文件目录 
├── CHANGELOG.md              项目改动记录
├── LICENSE                   许可证
├── README.md                 本文档
├── /assets/                  下载的frida-server存放的位置
├── frida-skeleton.py         项目入口
├── /images/                  本项目用到的图像资源文件
├── /lib/                     Python库文件，frida-skeleton核心实现部分
├── /logs/                    hook日志记录文件夹
├── /projects/                hook脚本存放的文件夹，以目录区分项目
├── requirements.txt          三方库需求列表
├── /scripts/                 封装好的实用API
└── /tests/                   提供测试的安卓项目
```

### 如何参与开源项目

贡献使开源社区成为一个学习、激励和创造的绝佳场所。你所作的任何贡献都是**非常感谢**的。


1. Fork本项目
2. 创建开发分支 (`git checkout -b dev`)
3. 提交更改 (`git commit -m 'Add something'`)
4. 推送到分支 (`git push origin dev`)
5. 提[Pull Request](https://github.com/Margular/frida-skeleton/compare)

### 版本控制

该项目使用Git进行版本管理。您可以在repository参看当前可用版本。

### 版权说明

该项目签署了MIT 授权许可，详情请参阅 [LICENSE](https://github.com/Margular/frida-skeleton/blob/master/LICENSE)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
