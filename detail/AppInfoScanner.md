## AppInfoScanner <https://github.com/kelvinBen/AppInfoScanner>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-kelvinBen-orange)
![GitHub stars](https://img.shields.io/github/stars/kelvinBen/AppInfoScanner.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.9-red)
![Time](https://img.shields.io/badge/Join-20210120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


### AppInfoScanner

一款适用于以HW行动/红队/渗透测试团队为场景的移动端(Android、iOS、WEB、H5、静态网站)信息收集扫描工具，可以帮助渗透测试工程师、攻击队成员、红队成员快速收集到移动端或者静态WEB站点中关键的资产信息并提供基本的信息输出,如：Title、Domain、CDN、指纹信息、状态信息等。

### 前言
- 本项目的开发者目前为个人开发者同时有自己的工作，新的功能或者需求会在闲暇时间进行开发，BUG会优先进行处理。
- 如果在使用中遇到问题或者有新的需求，请在[](https://github.com/kelvinBen/AppInfoScanner/issues)提交BUG反馈，提交BUG前请先阅读最后的"常见问题"。
- 如果您觉得这个项目对您有用，请点击本项目右上角的"star"按钮。
- 如果您想持续跟进新的版本情况，请点击本项目右上角的"Watch"按钮。
- 如果您想参与本项目的开发，请点击本项目右上角的"Fork"按钮,否则请勿点击"Fork"按钮。

### 免责声明
请勿将本项目技术或代码应用在恶意软件制作、软件著作权/知识产权盗取或不当牟利等**非法用途**中。实施上述行为或利用本项目对非自己著作权所有的程序进行数据嗅探将涉嫌违反《中华人民共和国刑法》第二百一十七条、第二百八十六条，《中华人民共和国网络安全法》《中华人民共和国计算机软件保护条例》等法律规定。本项目提及的技术仅可用于私人学习测试等合法场景中，任何不当利用该技术所造成的刑事、民事责任均与本项目作者无关。

### 适用场景
- 日常渗透测试中对APP中进行关键资产信息收集，比如URL地址、IP地址、关键字等信息的采集等。
- 大型攻防演练场景中对APP中进行关键资产信息收集，比如URL地址、IP地址、关键字等信息的采集等。
- 对WEB网站源代码进行URL地址、IP地址、关键字等信息进行采集等(可以是开源的代码也可以是右击网页源代码另存为)。
- 对H5页面进行进行URL地址、IP地址、关键字等信息进行采集等。
- 对某个APP进行定相信息收集等

### 功能介绍:
- [x] 支持目录级别的批量扫描
- [x] 支持DEX、APK、IPA、MACH-O、HTML、JS、Smali、ELF等文件的信息收集
- [x] 支持APK、IPA、H5等文件自动下载并进行一键信息收集
- [x] 支持自定义请求头、请求报文、请求方法
- [x] 支持规则自定义，随心自定义扫描规则
- [x] 支持自定义忽略资源文件
- [x] 支持自定义配置Android壳规则
- [x] 支持自定义配置中间件规则
- [x] 支持Android加固壳、iPA官方壳的检测
- [x] 支持IP地址、URL地址、中间件(json组件和xml组件)的信息采集
- [x] 支持Android对应包名下内容的采集
- [x] 支持网络嗅探功能，可以提供基本的信息输出
- [x] 支持Windows系统、MacOS系统、*nux系列的系统
- [x] 具备简单的AI识别功能，可以快速过滤三方URL地址
- [ ] 指纹识别模块
- [ ] 添加国际化语言包
- [ ] 一键对APK文件进行自动修复
- [ ] 识别到壳后自动进行脱壳处理

### 部分截图

![](https://github.com/kelvinBen/AppInfoScanner/raw/master/result.png)

### 环境说明
- Apk文件解析需要使用JAVA环境,JAVA版本1.8及以下
- Python3的运行环境

### 目录说明
```
AppInfoScanner
    |-- libs  程序的核心代码
        |-- core
            |-- __init__.py 全局配置信息
            |-- parses.py 用于解析文件中的静态信息
            |-- download.py 用于自动下载APP或者H5页面
            |-- net.py 用于进行网络嗅探，并获取基本信息
        |-- task
            |-- __init__.py 目录初始化文件
            |-- base_task.py 统一任务调度中心
 			|-- android_task.py 用于处理Android相关的任务
            |-- download_task.py 用于处理自动下载APP或者H5的任务            
​			 |-- ios_task.py 用于处理iOS相关的任务
            |-- net_task.py 用于处理网络嗅探相关任务
​            |-- web_task.py 用于处理Web相关的任务，比如网页右键源代码、H5相关的静态信息
​    |-- tools 程序需要依赖的工具
​        |-- apktool.jar 用于反编译apk文件，不同平台可能需要进行自我切换
​        |-- baksmali.jar 用于反编译dex文件，不同平台可能需要进行自我切换
​        |-- strings.exe 用于windows 32下获取iPA的字符串信息
​        |-- strings64.exe 用于windows 64的系统获取iPA的字符串信息
​    |-- __init__.py 目录初始化文件 
    |-- app.py 主运行程序
​    |-- config.py 整个程序的配置文件
​    |-- README.md  程序使用说明
    |-- requirements.txt 程序中需要安装的依赖库
    |-- update.md 程序历史版本信息
```
### 使用说明

1. 下载
```
    git clone https://github.com/kelvinBen/AppInfoScanner.git
    
    或者复制以下链接到浏览器下载最新正式版本
    
    https://github.com/kelvinBen/AppInfoScanner/releases/latest

    国内快速下载通道:

    git clone https://gitee.com/kelvin_ben/AppInfoScanner.git

```

2. 安装依赖库
```
    cd AppInfoScanner
    python3 -m pip install -r requirements.txt
```

3. 运行(基础版)

- 扫描Android应用的APK文件、DEX文件、需要下载的APK文件下载地址、保存需要扫描的文件的目录

```
    python3 app.py android -i <Your APK File or DEX File or APK Download Url or Save File Dir>
```

- 扫描iOS应用的IPA文件、Mach-o文件、需要下载的IPA文件下载地址、保存需要扫描的文件目录

```
    python3 app.py ios -i <Your IPA file or Mach-o File or IPA Download Url or Save File Dir>
```

- 扫描Web站点的文件、目录、需要缓存的站点URl

```
    python3 app.py web -i <Your Web file or Save Web Dir or Web Cache Url>
```

### 进阶操作指南

#### 基本命令格式
```
python3 app.py [TYPE] [OPTIONS] <The URL or directory to scan>
```

#### 符号信息说明

```
<> 代表需要扫描的文件或者目录或者URL地址
| 或的关系，只能选择一个
[] 代表需要输入的参数
```

#### TYPE参数详细说明
此参数类型对应基本命令格式中的[TYPE],目前仅支持[android/ios/web]三种类型形式，三种类型形式必须指定一个。

```
android: 用于扫描Android应用相关的文件的内容
ios: 用于扫描iOS应用相关的文件内容
web: 用于扫描WEB站点或者H5相关的文件内容
```

支持自动根据后缀名称进行修正，即便输入的是ios，实际上-i 输入的参数的文件名为XXX.apk，则会执行android相关的扫描。


#### OPTIONS参数详细说明
该参数类型对应基本命令格式中的[OPTIONS]，支持多个参数共同使用

```
-i 或者 --inputs: 输入需要进行扫描的文件、目录或者需要自动下载的文件URL地址，如果路径过长请加"进行包裹，此参数为必填项。
-r 或者 --rules: 输入需要扫描文件内容的临时扫描规则。
-s 或者 --sniffer: 开启网络嗅探功能，默认为开启状态。
-n 或者 --no-resource: 忽略所有的资源文件，包含网络嗅探功能中的资源文件(需要先在config.py中配置sniffer_filter相关规则)，默认为不忽略资源。
-a 或者 --all: 输出所有符合扫描规则的结果集合，默认为开启状态。
-t 或者 --threads: 设置线程并发数量，默认为10个线程并发。
-o 或者 --output: 指定扫描结果和扫描过程中产生的临时文件的输出目录，默认为脚本所在的目录。
-p 或者 -- package: 指定Android的APK文件或者DEX文件需要扫描的JAVA包名信息。此参数只能在android类型下使用。
```

#### 具体使用方法

##### Android相关基本操作
- 对本地APK文件进行扫描
```
python3 app.py android -i <Your apk file>  

例:

python3 app.py android -i  C:\Users\Administrator\Desktop\Demo.apk
```

- 对本地Dex文件进行扫描
```
python3 app.py android -i <Your DEX file>  

例:

python3 app.py android -i  C:\Users\Administrator\Desktop\Demo.dex

```
- 对URL地址中包含的APK文件进行扫描
```
python3 app.py android -i <APK Download Url>  

例:

python3 app.py android -i "https://127.0.0.1/Demo.apk" 

```
需要注意此处如果URL地址过长需要使用双引号(")进行包裹

##### iOS相关基本操作
- 对本地IPA文件进行扫描
```
python3 app.py ios -i <Your ipa file>

例:

python3 app.py ios -i "C:\Users\Administrator\Desktop\Demo.ipa" 
```

- 对本地Macho文件进行扫描
```
python3 app.py ios -i <Your Mach-o file>

例:

python3 app.py ios -i "C:\Users\Administrator\Desktop\Demo\Payload\Demo.app\Demo" 
```

- 对URL地址中包含的IPA文件进行扫描
```
python3 app.py ios -i <IPA Download Url>  

例:

python3 app.py ios -i "https://127.0.0.1/Demo.ipa" 

```
需要注意此处如果URL地址过长需要使用双引号(")进行包裹,暂时不支持对Apple Store中的IPA文件进行扫描

##### Web相关基本操作

- 对本地WEB站点进行扫描
```
python3 app.py web -i <Your web file>

例:

python3 app.py web -i "C:\Users\Administrator\Desktop\Demo.html" 
```
- 对URL地址中包含的WEB站点文件进行扫描
```
python3 app.py web -i <Web Download Url>  

例:

python3 app.py web -i "https://127.0.0.1/Demo.html" 

```

##### 具有共同性的操作

以下操作均以android类型为例：

- 对一个本地的目录进行扫描
```
python3 app.py android -i <Your Dir>

例：

python3 app.py android -i C:\Users\Administrator\Desktop\Demo
```

- 添加临时规则或者关键字

```
python3 app.py android -i <Your apk> -r <the keyword | the rules>

例：
添加对百度域名的扫描

python3 app.py android -i C:\Users\Administrator\Desktop\Demo.apk -r ".*baidu.com.*"
```

- 关闭网络嗅探功能
```
python3 app.py android -i <Your apk> -s

例：
python3 app.py android -i C:\Users\Administrator\Desktop\Demo.apk -s

```
- 忽略所有的资源文件
```
python3 app.py android -i <Your apk> -n

例：
python3 app.py android -i C:\Users\Administrator\Desktop\Demo.apk -n

```

- 关闭输出所有符合扫描规则内容的功能
```
python3 app.py android -i <Your apk> -a

例：

python3 app.py android -i C:\Users\Administrator\Desktop\Demo.apk -a
```

- 设置并发数量
```
python3 app.py android -i <Your apk> -t 20

例：
设置20个并发线程
python3 app.py android -i C:\Users\Administrator\Desktop\Demo.apk -t 20 
```
- 指定结果集和缓存文件输出目录
```
python3 app.py android -i <Your apk> -o <output path>

例：
比如输出到桌面的Temp目录
python3 app.py android -i C:\Users\Administrator\Desktop\Demo.apk -o C:\Users\Administrator\Desktop\Temp
```

- 对指定包名下的文件内容进行扫描，该功能仅支持android类型

```
python3 app.py android -i <Your apk> -p <Java package name>

例：
比如需要过滤com.baidu包名下的内容

python3 app.py android -i C:\Users\Administrator\Desktop\Demo.apk -p "com.baidu"
```

### 高级版使用说明
该项目中的程序仅作为一个基本的架子，会内置一些基本的规则，并不是每一个输入的内容都可以完成相关的扫描工作。所以可以根据自己的需要进行相关规则的配置，优秀的配置内容可以达到质的的效果。


- 配置文件路径为 根目录下的config.py文件，即README.md的同级目录

#### 配置项说明
```
filter_components: 此配置项用于配置相关组件内容，包括Json组件或者XML组件等
filter_strs: 用于配置需要进行扫描的文件内容，比如需要扫描端口号，则配置为："r'.*://([\d{1,3}\.]{3}\d{1,3}).*'"
filter_no: 用于忽略扫描文件中不想要的内容
shell_list: 用于配置Android相关的壳特征
web_file_suffix: 此处配置需要进行扫描的WEB文件后缀名称
sniffer_filter: 此处用于配置需要进行忽略网络嗅探的文件后缀名称
headers: 用于配置自动下载过程中需要的请求头信息
data: 用于配置自动下载过程中需要的请求报文体
method: 用于配置自动下载过程中需要的请求方法
```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.0.9] - 2022-10-23

**更新**  
- 更新apktool为最新版本  
- 优化部分环节流程  
- 修复excle文件导出时超时行数限制  
- 修复脚本执行时卡顿的问题  
- 修复Mac下Playload文件权限不足的问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
