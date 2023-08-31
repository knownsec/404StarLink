## ysomap <https://github.com/wh1t3p1g/ysomap>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-wh1t3p1g-orange)
![GitHub stars](https://img.shields.io/github/stars/wh1t3p1g/ysomap.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.1.3-red)
![Time](https://img.shields.io/badge/Join-20211122-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


Ysomap是一款适配于各类实际复杂环境的Java反序列化利用框架，可动态配置具备不同执行效果的Java反序列化利用链payload，以应对不同场景下的反序列化利用。

此外，ysomap支持多种exploits，用于生成或配置一些evil server，或者是常见漏洞的exp。
```
[+] exploits(11) payloads(31) bullets(28)
```
## #1 如何使用

### 生成
由于最新版XStream的payload需要JDK8的环境进行编译，所以后续运行需在JDK8的环境下运行

使用`mvn clean package -DskipTests`

生成的jar位于`cli/target/ysomap.jar`

版本>=v0.0.1支持两种运行模式

1. cli模式
执行`java -jar ysomap.jar cli`,终端模式
   
2. script模式
执行`java -jar ysomap.jar script /path/to/script.yso`，脚本模式

ps: 后续版本为了适配XStream的相关gadget加入了很多jdk的对象，所以如果要使用xstream的gadget，ysomap最好运行在jdk8的环境下。
### 基础使用方法

参见[YSOMAP食用指北](https://github.com/wh1t3p1g/ysomap/wiki/YSOMAP%E9%A3%9F%E7%94%A8%E6%8C%87%E5%8C%97)

## #2 当前进度

### DONE

- [x] 支持CommonsCollections系列payload
- [x] 支持执行效果bullet：远程jar载入、命令执行、代码执行、发起jndi效果、tomcat内存马、延时判断、文件写入、socket shell。
- [x] 支持现有RMI系列攻击包 [原理1](http://blog.0kami.cn/2020/02/06/rmi-registry-security-problem/) [原理2](http://blog.0kami.cn/2020/02/09/jndi-with-rmi/) [原理3](https://mogwailabs.de/blog/2020/02/an-trinhs-rmi-registry-bypass/)
- [x] 支持现有LDAP系列攻击包 [原理](http://blog.0kami.cn/2020/03/01/jndi-with-ldap/)
- [x] 支持HTTP服务动态挂载恶意的class文件或jar文件
- [x] 支持URLDNS
- [x] 支持现有JMX系列攻击包 [原理](http://blog.0kami.cn/2020/03/10/java-jmx-rmi/)
- [x] 支持fastjson JdbcRowSetImpl、TemplatesImpl gadget [原理](http://blog.0kami.cn/2020/04/13/talk-about-fastjson-deserialization/)
- [x] 支持现有XStream系列payload包 [原理](http://blog.0kami.cn/2020/04/18/talk-about-xstream-deserialization/)
- [x] 支持weblogic XMLDecoder payloads

### TODO

- [ ] 支持weblogic系列攻击包
- [ ] 支持websphere系列攻击包

## #3 由来

在实际分析ysoserial的利用链时，有时候会觉得框架写的太死，有以下几个缺点：

1. 同一个利用链如果想改变一下最后的利用效果，如命令执行改成代码执行，我们需要改写这个利用链或者是重新增加一个利用链。这时，我们其实可以看到利用链的前半部分是不变的，变的只是后续的利用效果。
2. ysoserial仅实现了常规的序列化利用链，对于类似JSON格式的序列化利用链，以当前的这个框架扩展起来会比较麻烦

所以萌生了开发一个更加灵活的框架来扩展反序列化利用链，也就是当前这个试验品ysomap。

PS：YSOMAP项目为另一个项目的子项目，后续将开源该项目，敬请期待......

## #4 原理

我将利用链切分成了两个部分**payload**和**bullet**：

1. payload：指代利用链的前序部分
2. bullet：指代最终利用链可达成的效果

#### 实际案例分析

CommonsCollection1和3，在分析时我们可以看到实际1和3的区别在于1使用的是`InvokerTransformer`，而3使用的是`templatesImpl`的方式。那么提取相同的前序payload部分，我们只需写两个不同的bullet即可。而且这两个bullet也同样能被用在其他的payload上。

实际还有就是我在写RMIRegistryExploit时，也有这种可将不变部分重用的地方，而无需2,3之类的出现。


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2021-11-24 发布文章[《ysomap : Java反序列化利用框架》](https://mp.weixin.qq.com/s/WluThXve9hLoJQ8hnyfLgA)

## 最近更新

#### [v0.1.3] - 2022-04-15

**更新**  
- 新增若干payloads、bullets，目前共计 [+] exploits(12) payloads(31) bullets(36)  
- 支持设置编码器、输出方式、serialVersionUid、序列器类型，具体方法见wiki

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
