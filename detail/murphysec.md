## murphysec <https://github.com/murphysecurity/murphysec>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-murphysecurity-orange)
![GitHub stars](https://img.shields.io/github/stars/murphysecurity/murphysec.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.10.0-red)
![Time](https://img.shields.io/badge/Join-20220914-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

中文 | [EN](https://github.com/murphysecurity/murphysec/blob/v3/README.md)

墨菲安全的 **CLI 工具**，用于在命令行检测指定目录代码的依赖安全问题，也可以基于 CLI 工具实现在 CI 流程的检测。

## 功能
1. 分析项目使用的依赖信息，包含直接和间接依赖
2. 检测项目依赖存在的已知漏洞信息


### 效果截图

- CLI 运行结果

  <img alt="cli output" src="https://github.com/murphysecurity/murphysec/raw/v3/assets/cli.png" width="80%">

- 检测结果页面

  <img alt="scan result" src="https://github.com/murphysecurity/murphysec/raw/v3/assets/scan-result.png" width="80%">
  
  <img alt="scan result" src="https://github.com/murphysecurity/murphysec/raw/v3/assets/scan-detail-result.png" width="80%">

## 目录

1. [支持的语言](#支持的语言)
2. [工作原理](#工作原理)
3. [使用场景](#使用场景)
4. [使用步骤](#使用步骤)
5. [命令介绍](#命令介绍)
6. [交流和问题反馈](#交流和问题反馈)
7. [开源协议](#开源协议)

## 支持的语言

目前支持 Java、JavaScript、Golang、Python、PHP、C#、Ruby、Objective-C、.NET 语言项目的检测，后续会逐渐支持其他的开发语言。

<table>
 <tr>
     <th>语言</th>
     <th>包管理工具</th>
     <th>所需文件</th>
 </tr>
 <tr >
     <td rowspan="2">Java</td>
     <td>Maven</td>
      <td>pom.xml</td>

 </tr>
 <tr>
     <td>Gradle</td>
    <td>build.gradle, build.gradle.kts</td>

 </tr>

  <tr >
     <td>Go</td>
     <td>Go Modules</td>
      <td>go.mod</td>

 </tr>

  <tr >
     <td rowspan="2">JavaScript</td>
     <td>NPM</td>
    <td>package.json, package-lock.json</td>

 </tr>
 <tr>
     <td>Yarn</td>
    <td>yarn.lock, package.json</td>


  <tr >
     <td rowspan="2">Python</td>
     <td>pip</td>
    <td>requirements.txt</td>

 </tr>
 <tr>
     <td>Poetry</td>
    <td>poetry.lock</td>

  <tr >
     <td>PHP</td>
     <td>Composer</td>
      <td>composer.lock</td>

 </tr>

  <tr >
     <td>Ruby</td>
     <td>Bundler</td>
      <td>Gemfile.lock, gems.locked</td>

 </tr>
   <tr >
     <td>.NET</td>
     <td>NuGet</td>
      <td>packages.lock.json</td>

 </tr>
   <tr >
     <td>C#</td>
     <td>NuGet</td>
      <td>packages.lock.json</td>

 </tr>

   <tr >
     <td>Objective-C</td>
     <td>Cocoapods</td>
      <td>Podfile.lock</td>

 </tr>

</table>

详细的支持情况可以[查看文档](https://www.murphysec.com/docs/quick-start/language-support/)

## 工作原理

1. 对于使用不同语言/包管理工具的项目，墨菲安全的 CLI 工具主要采用`项目构建`或直接对`包管理文件`进行解析的方式，来准确获取到项目的依赖信息
2. 项目的依赖信息会上传到服务端，并基于墨菲安全持续维护的`漏洞知识库`来识别项目中存在安全缺陷的依赖

![cli-flowchart](https://github.com/murphysecurity/murphysec/raw/v3/assets/flowchart.png)

> 说明：CLI 工具只会将检测项目的依赖和基本信息发送到墨菲安全服务端，用于识别存在安全缺陷的依赖，不会上传任何本地代码。


## 使用场景
1. 希望在本地环境中检测代码文件
2. 希望集成到 CI 环境中对代码项目进行检测

参考：[墨菲安全 CLI 与 Jenkins CI 的集成](https://www.murphysec.com/docs/integrations/jenkins/)



## 使用步骤
### 1. 安装

访问 [GitHub Releases](https://github.com/murphysecurity/murphysec/releases/latest) 页面下载最新版本的墨菲安全 CLI，或执行以下相关命令：

#### 在 Linux 上安装

```
wget -q https://s.murphysec.com/install.sh -O - | /bin/bash
```

#### 在 OSX 上安装

```
curl -fsSL https://s.murphysec.com/install.sh | /bin/bash
```

#### 在 WINDOWS 上安装

```
powershell -Command "iwr -useb https://s.murphysec.com/install.ps1 | iex"
```

### 2.创建任务

首先登录到墨菲安全控制台，创建任务的方式有以下三种

- 方式1：在项目页面，点击项目右上角的加号选择接入
- 方式2：进入指定项目，点击右上角的创建任务按钮接入
- 方式3：进入指定项目，点击右上角的创建任务按钮，选择其他接入方式通过模板接入

### 3. 获取访问令牌

> CLI 工具需要使用墨菲安全账户的`访问令牌`进行认证才能正常使用。[访问令牌是什么？（点击查看详情）](https://www.murphysec.com/docs/guides/scan-scene/cli.html)

方式1：

进入[墨菲安全控制台](https://www.murphysec.com/)，点击`左下角个人设置`，点击`用户token` 复制`访问令牌`

<img alt="scan result" src="https://github.com/murphysecurity/murphysec/raw/v3/assets/acces-token1.png" width="80%">



方式2： 任务创建页面最下方-->复制token 

<img alt="scan result" src="https://github.com/murphysecurity/murphysec/raw/v3/assets/acces-token2.png" width="80%">



### 4. 认证

目前有两种认证方式可用：命令行交互认证、命令行参数认证

#### 命令行交互认证
执行`murphysec auth login`命令，粘贴访问令牌即可。


> 认证后下次使用墨菲安全 CLI 无需再次执行此操作，如果需要更换访问令牌，可以重复执行此命令来覆盖旧的访问令牌。


#### 命令行参数认证
执行检测命令时，通过增加`--token`参数指定访问令牌进行认证

### 4. 检测

使用`murphysec scan`命令进行检测，可以执行以下命令：

``` bash
murphysec scan [your-project-path]
```

可用的参数
- `--token`：指定访问令牌
- `--log-level`：指定命令行输出流打印的日志级别，默认不打印日志，可选参数为`silent`、`error`、`warn`、`info`、`debug`
- `--json`：指定检测的结果输出为json，默认不展示结果详情


### 5. 查看结果

CLI 工具默认不展示结果详情，可以在[墨菲安全控制台](https://www.murphysec.com/project/list)-`项目`页面查看详细的检测结果



## 命令介绍

### murphysec auth
`murphysec auth` 命令主要是管理 CLI 的认证

```
Usage:
  murphysec auth [command]

Available Commands:
  login
  logout
```

### murphysec scan
`murphysec scan` 命令主要用于执行检测

```
Usage:
  murphysec scan DIR [flags]

Flags:
  -h, --help                帮助
      --task-id string   指定本次检测归属的项目ID

Global Flags:
  -x  --allow-insecure        允许不安全的TLS连接
      --log-level string      指定输出日志信息的级别, 可以为 silent|error|warn|info|debug (默认为 "silent"， 不输出日志)
      --network-log           打印网络数据
      --no-log-file           不输出日志文件
      --server string         指定服务地址
      --token string          指定墨菲安全服务 Token
  -v, --version               输出 CLI 版本
      --write-log-to string   指定日志文件的路径

```

## 常见问题

**1. Windows下安装失败，提示“PowerShell requires an execution policy of 'RemoteSigned'”**

Powershell默认不允许从远程加载安装脚本，需要使用管理员权限打开Powershell窗口，并执行`Set-ExecutionPolicy RemoteSigned -scope CurrentUser`。随后执行安装命令即可成功。

**2. 为什么我的 Java（maven） 项目检测结果依赖信息不完整？**

* 本地是否配置了 Maven 环境，可使用`mvn -v`查看
* 请检查 Maven 的源是否配置正确。如果是企业内部代码，通常需要配置公司的私有源地址。一般情况下可通过修改`~/.m2/settings.xml`进行配置
* 请检查代码目录下是否存在`pom.xml`文件，也可通过 `mvn dependency:tree --file="pom.xml"` 命令测试此项目本地是否可正常获取依赖

**3. 为什么检测完依赖和缺陷组件数量都是0 ？**

* 检查您的项目/文件是否在目前支持的检测范围内

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
