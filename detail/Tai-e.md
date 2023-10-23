## Tai-e <https://github.com/pascal-lab/Tai-e>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-pascal_lab-orange)
![GitHub stars](https://img.shields.io/github/stars/pascal-lab/Tai-e.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.2.2-red)
![Time](https://img.shields.io/badge/Join-20230913-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## What is Tai-e?

Tai-e (Chinese: 太阿; pronunciation: [ˈtaɪə:]) is a new static analysis framework for Java (please see our [ISSTA 2023 paper](https://cs.nju.edu.cn/tiantan/papers/issta2023.pdf) for details), which features arguably the "best" designs from both the novel ones we proposed and those of classic frameworks such as Soot, WALA, Doop, and SpotBugs.
Tai-e is easy-to-learn, easy-to-use, efficient, and highly extensible, allowing you to easily develop new analyses on top of it.

Currently, Tai-e provides the following major analysis components (and more analyses are on the
way):

- Powerful pointer analysis framework
  - On-the-fly call graph construction
  - Various classic and advanced techniques of heap abstraction and context sensitivity for pointer analysis
  - Extensible analysis plugin system (allows to conveniently develop and add new analyses that interact with pointer analysis)
- Configurable security analysis
  - Taint analysis, which allows to configure sources, sinks, taint transfers, and sanitizers
  - Detection of various information leakages and injection vulnerabilities
  - Various precision and efficiency tradeoffs (benefit from the pointer analysis framework)
- Various fundamental/utility analyses
  - Fundamental analyses, e.g., reflection analysis and exception analysis
  - Modern language feature analyses, e.g., lambda and method reference analysis, and invokedynamic analysis
  - Utility tools like analysis timer, constraint checker (for debugging), and various graph dumpers
- Control/Data-flow analysis framework
  - Control-flow graph construction
  - Classic data-flow analyses, e.g., live variable analysis, constant propagation
  - Your data-flow analyses
- SpotBugs-like bug detection system
  - Bug detectors, e.g., null pointer detector, incorrect `clone()` detector
  - Your bug detectors

Tai-e is developed in Java, and it can run on major operating systems including Windows, Linux, and macOS.

As a courtesy to the developers, we expect that you **please [cite](https://github.com/pascal-lab/Tai-e/blob/master/CITATION.bib) the paper** from ISSTA 2023 describing the Tai-e framework in your research work:

Tian Tan and Yue Li. 2023.
**Tai-e: A Developer-Friendly Static Analysis Framework for Java by Harnessing the Good Designs of Classics.**
In Proceedings of the 32nd ACM SIGSOFT International Symposium on Software Testing and Analysis (ISSTA '23), July 17–21, 2023, Seattle, WA, USA ([pdf](https://cs.nju.edu.cn/tiantan/papers/issta2023.pdf), [bibtex](https://github.com/pascal-lab/Tai-e/blob/master/CITATION.bib)).

## How to Obtain Runnable Jar of Tai-e?
The simplest way is to download it from [GitHub Releases](https://github.com/pascal-lab/Tai-e/releases).

Alternatively, you might build the latest Tai-e yourself from the source code. This can be simply accomplished via Gradle (be sure that Java 17 (or higher version) is available on your system).
You just need to run command `gradlew fatJar`, and then the runnable jar will be generated in `tai-e/build/`, which includes Tai-e and all its dependencies.

## How to Include Tai-e in Your Project?
Tai-e is designed as a standalone tool, but you also have the option to include it in your project as a dependency.
It is available on Maven repositories, allowing you to easily integrate it into your Java projects using build tools such as Gradle and Maven.
We maintain both stable and latest versions of Tai-e, and here are the corresponding coordinates in Gradle and Maven script formats:

### Stable Version
For Gradle:

```kotlin
dependencies {
    implementation("net.pascal-lab:tai-e:0.2.2")
}
```

For Maven:

```xml

<dependencies>
    <dependency>
        <groupId>net.pascal-lab</groupId>
        <artifactId>tai-e</artifactId>
        <version>0.2.2</version>
    </dependency>
</dependencies>
```

### Latest Version

For Gradle:

```kotlin
repositories {
    mavenCentral()
    maven { url = uri("https://s01.oss.sonatype.org/content/repositories/snapshots/") }
}

dependencies {
    implementation("net.pascal-lab:tai-e:0.5.1-SNAPSHOT")
}
```

For Maven:

```xml
<repositories>
    <repository>
        <id>snapshots</id>
        <name>Sonatype snapshot server</name>
        <url>https://s01.oss.sonatype.org/content/repositories/snapshots/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>net.pascal-lab</groupId>
        <artifactId>tai-e</artifactId>
        <version>0.5.1-SNAPSHOT</version>
    </dependency>
</dependencies>
```

You can use these coordinates in your Gradle or Maven scripts to include the desired version of Tai-e in your project.

## Documentation

### Reference Documentation

We have provided detailed information of Tai-e in the [Reference Documentation](http://tai-e.pascal-lab.net/docs/current/reference/en/index.html), which covers various aspects such as [Setup in IntelliJ IDEA](http://tai-e.pascal-lab.net/docs/current/reference/en/setup-in-intellij-idea.html), [Command-Line Options](http://tai-e.pascal-lab.net/docs/current/reference/en/command-line-options.html), and [Development of New Analysis](http://tai-e.pascal-lab.net/docs/current/reference/en/develop-new-analysis.html).

Please note that the reference documentation mentioned above pertains to *the latest version* of Tai-e.
If you need documentation for a specific stable version, please refer to the [Documentation Index](https://tai-e.pascal-lab.net/docs).
Additionally, the documentation is included within the repository and maintained alongside the source code.
You can access the reference documentation for a particular version of Tai-e (in AsciiDoc format) by exploring the [docs/en](https://github.com/pascal-lab/Tai-e/blob/master/docs/en) directory, starting from [index.adoc](https://github.com/pascal-lab/Tai-e/blob/master/docs/en/index.adoc).
This allows you to access version-specific documentation for Tai-e.

In addition to the reference
documentation, [Javadocs](https://tai-e.pascal-lab.net/docs/current/api/index.html) for Tai-e are
also available as a useful reference resource.

### Changelog
Since we are actively developing and updating Tai-e, we record the notable changes we made, especially the new features and breaking changes, in [CHANGELOG](https://github.com/pascal-lab/Tai-e/blob/master/CHANGELOG.md).
If you find something wrong after updating Tai-e, maybe you could check [CHANGELOG](https://github.com/pascal-lab/Tai-e/blob/master/CHANGELOG.md) for useful information.

## Tai-e Assignments
In addition, we have developed an [educational version of Tai-e](http://tai-e.pascal-lab.net/en/intro/overview.html) where eight programming assignments are carefully designed for systematically training learners to implement various static analysis techniques to analyze real Java programs.
The educational version shares a large amount of code with Tai-e, thus doing the assignments would be a good way to get familiar with Tai-e.

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2023-10-08 发布演示视频[程序分析框架“太阿”与安全漏洞的那些事之Log4Shell篇](https://www.bilibili.com/video/BV1ez4y1F7VB/)

## 最近更新

#### [v0.2.2] - 2023-09-23

**新功能**  
- 添加选项--app-class-path, 指定 application 类的路径  
- 添加选项--keep-results, 支持运行时只保留必要的分析结果, 节省内存  
- 添加选项--output-dir, 可指定分析结果输出目录  
- 添加选项-wc,--world-cache-mode, 可缓存World, 加速多次分析同一程序的启动时间  
- 添加 def-use 分析  
- 添加 dominator-finding 算法  
- 添加类、方法与字段的泛型签名信息  
- 将文档源文件包含进仓库中, 实现文档与代码版本的对应  
- 污点分析  
  - 支持指定方法形参以及实参作为污点源  
  - 支持指定字段读取作为污点源  
  - 支持为方法形参配置污点消毒器(sanitizer)  
  - 自动输出污点流图  
  - 支持加载多个污点配置文件  
  - 支持变量和实例字段/数组元素之间的污点转移  
  - 支持 call-site 模式  
- 指针分析  
  - 支持添加程序的入口点进行分析  
  - 支持设置分析时间限制  
  - 支持原子类型值的传播  
  - 支持基于推导和基于日志的混合反射分析  
  - 添加 Solar 反射分析(TOSEM'19)  
  - 支持以注解的方式注册的调用处理程序  
  - 支持转储 YAML 格式的指针分析结果  
更多详细更新内容:https://github.com/pascal-lab/Tai-e/releases  


<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
