# 404 StarLink Project 2.0 - Galaxy

---

![](./logo.png)



The 404 Starlink Project was started by Knownsec 404Team in 2020. We aim to denfend network and promote the  Instrumentalizing  of security research in different fields through open source or open methods. Just like Starlink, this project will link researchers with different security background.

Not only large tools which break security barriers，various small tools that optimizing the daily experience are included. We will open all tools developed by 404 Team, and continue to collect pain points in the process of security research and penetration testing.  The security field used to have various problems, like   tools jumbled, different levels obvious, and open source be unmaintained. Through the 404 Starlink Project, we wish security field would become a better place where people like to communicate and progress together.

[“404星链计划”](https://github.com/knownsec/404StarLink-Project)是知道创宇404实验室于2020年8月开始的计划，旨在通过开源或者开放的方式，**长期维护**并推进涉及安全研究各个领域不同环节的工具化，就像星链一样，将立足于不同安全领域、不同安全环节的研究人员链接起来。

[“404星链计划”](https://github.com/knownsec/404StarLink-Project)主要目的是改善安全圈内工具庞杂、水平层次不齐、开源无人维护的多种问题，营造一个更好更开放的安全工具促进与交流的技术氛围。

2020年11月，知道创宇404实验室正式推出星链计划2.0。通过星链计划核心社群成员作为核心，筛选**优质、有意义、有趣、坚持维护**的开源项目加入星链计划2.0，由404实验室核心成员及星链计划核心成员作为背书，将优质的开源项目汇聚成星河，为立足于不同安全领域的安全研究人员指明方向。代号**Galaxy**。

同时，真正优质的开源项目将会优先推荐KCON 2021兵器谱，在KCON 2021上获得专属的曝光机会。404实验室也会为优秀的个人开源维护者提供知道创宇的优先内推绿色通道，星链计划的核心成员群也会不定期送出礼品。

星链计划2.0会将开源项目按照两个核心项分类：
- 成熟、有意义的开源项目       Open-Projects
- 有新意、解决痛点的开源项目   Fun-tools

入选星链计划2.0的项目至少需要满足以下四个要求：
- 安全相关的各个环节以及链路
- 开源
- 坚持维护
- 通过由404实验室以及星链计划核心成员组成的审阅组审阅

入选项目将由代码质量、技术难度、新颖度等多个维度评价打分(满分5星)，是否坚持维护将作为最重要的评价标准。超过1年未更新的开源项目不会入选任何一个分类项目，超过6个月未更新的开源项目只能入选Fun-tools分类，且只能获得上限为3星的评价，超过3个月未更新的开源项目只能获得上限为4星的评价。

参与星链计划2.0的开源项目可以借由星链计划社群与开发者直接沟通，真正将研究人员和开发人员连在一起。

希望星链计划2.0能像北斗七星一样，引领安全研究人员前进的方向。



# Rules

- Positivity: 积极度，3个月内存在更新的将被标记为In，3-6个月内存在更新将被标记为TBD，6个月-1年存在更新的被标记为OUT.

- Score: Open-Projects的评分上限为5星，Fun-tools的评分上限为4星.

  

# Contents

- Open-Projects
    
    - [antSword](#antSword)
        - ![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Nodejs-blue)
        - 中国蚁剑是一款开源的跨平台网站管理工具，一个所有安全从业者都不应该错过的开源项目。
    - [kunpeng](#kunpeng)
        - ![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Go-blue)
    - Kunpeng是一个Golang编写的开源POC检测框架。
    - [myscan](#myscan)
        - ![](https://img.shields.io/badge/Positivity-IN-green) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Language-Python-blue)
        - myscan由python3开发而成的被动扫描工具。
    
- Fun-tools
    - [java-object-searcher](#java-object-searcher)
        
        - ![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%E2%98%85-green) ![](https://img.shields.io/badge/Language-Java-blue)
        - java内存对象搜索辅助工具，配合IDEA在Java应用运行时，对内存中的对象进行搜索。比如可以可以用挖掘request对象用于回显等场景。
    - [Juggler](#Juggler)
        - ![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Language-Go-blue)
        - 一个也许能骗到黑客的系统。可以作为WAF等防护体系的一环。
    - [Redis Rogue Server](https://github.com/Dliv3/redis-rogue-server)
        - ![](https://img.shields.io/badge/Positivity-TBD-yellow) ![](https://img.shields.io/badge/Score-%E2%98%85%E2%98%85%e2%98%86-yellow) ![](https://img.shields.io/badge/Language-Python-blue)
        
        - Redis 4.x/Redis 5.x RCE利用脚本. 
        
          

# Community

如果有问题可以在各项目下提交issue，如果有不错的工具推荐，可以向github提交issue, 也可以添加下方的讨论组中参与讨论。

1、Github issue: [https://github.com/knownsec/404StarLink2.0-Galaxy/issues](https://github.com/knownsec/404StarLink2.0-Galaxy/issues)

2、微信群：

微信群有两种添加方式：

(1) 联系Seebug的各位小伙伴拉你入群，如：
![image-20200902105354031](./init1.png)

(2) <del>扫描一下二维码添加我的个人微信</del>，会把大家拉到星链计划交流群中

<img src="./wechat.png" alt="image-20200902105546332" style="zoom:50%;" />