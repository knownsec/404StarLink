## geacon_pro <https://github.com/H4de5-7/geacon_pro>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-H4de5-orange)
![GitHub stars](https://img.shields.io/github/stars/H4de5-7/geacon_pro.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.1-red)
![Time](https://img.shields.io/badge/Join-20221117-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

本项目基于[geacon](https://github.com/darkr4y/geacon)项目对cobaltstrike的beacon进行了重构，并适配了大部分Beacon的功能。

**该项目会持续跟进免杀的技术，保持项目的免杀性，并将免杀的技术与工具集成进来，希望未来可以做成不仅限cs功能的跨平台后渗透免杀工具。如果师傅们有相关的需求或者想法，欢迎一起来讨论。师傅们的支持与讨论是我们前进的动力。**

**后续可能会考虑hook服务端jar包，类似冰蝎4.0让用户可以自定义流量的加密方式。**

**该项目仅用于对CobaltStrike协议的学习测试。请勿使用于任何非法用途，由此产生的后果自行承担。**

本项目与好兄弟Z3ratu1共同开发，他实现了一版支持4.0版本的[geacon_plus](https://github.com/Z3ratu1/geacon_plus)，我这边实现了一版支持4.1及以上版本的beacon，大致功能类似，有部分功能不同。

传统cs的免杀偏向于如何加载上线，但是杀软对beacon的特征查得非常严，尤其是卡巴这种查内存的，因此不如自己重构一个。

免杀主要体现在三个方面:
* 由于是重构的，因此没有beacon的特征，针对beacon特征的杀软是检测不出来的。
* golang本身具备一定的免杀性
* 针对各功能实现了免杀，cs部分不免杀的功能得到了更换

**在师傅们的帮助下测试了4.3、4.4、4.5、4.7版本，理论上来说4.1+版本均支持，如果有不支持的版本请及时通知我。**

**如果有不免杀的地方请及时通知我。**

**由于项目刚做出来，目前的版本存在部分功能不完善的地方，如有需求请师傅们提出。**

目前实现的功能具备免杀性，可过Defender、360核晶（除powershell）、卡巴斯基（除内存操作外，如注入原生cs的dll）、火绒

上述测试环境均为实体机

**为了规避360对fork&&run操作的监控，本项目目前采用注入自己的方式来执行cs原生的dll，但是测试发现cs原生powerpick在注入自己执行的时候有时候会拿不到回显，在fork&&run模式下正常。因此可用execute-assembly执行我这里另一个powershell免杀的[小工具](https://github.com/H4de5-7/powershell-bypass)，可绕过Defender、360等。**

若想使用免杀bypassUAC的话，请execute-assembly执行[该项目](https://github.com/0xlane/BypassUAC/)的Csharp版本，尽管Csharp程序不免杀，但是execute-assembly之后可过Defender与360。该项目dll版本自己编译一下是可以免杀的，但是需要落地并且需要用rundll32执行，因此并不推荐。

若想用免杀捆绑器的话可以参考我的这个[小项目](https://github.com/H4de5-7/Bundler-bypass)

若想用免杀计划任务的话可以参考我的这个[小项目](https://github.com/H4de5-7/schtask-bypass)以及一个师傅的这个[项目](https://github.com/0x727/SchTask_0x727)（不过这个项目需要用execute-assembly来内存执行）。

开发的过程中参考了鸡哥的数篇文章以及许许多多的项目，同时抓包对服务端返回的内容进行猜测，并对服务端java代码进行了部分的理解。

由于本人对二进制方向接触的不多，希望师傅们多多包涵，欢迎师傅们交流，欢迎指出问题。

**如果有师傅对堆内存加密有好的解决思路欢迎来讨论，我的实现思路在实现细节里面**

## 更新的情况
11.10更新：

实现了exit时自删除的功能，可通过设置config.go中的DeleteSelf来设置，默认为false。

11.9更新：

实现了dllinject、cna等用户自定义反射型dll注入，将shinject和dllinject的注入方法改为remote，修改了rsa解密的bug，对x86进行了部分功能的适配，对cna进行了适配（即新支持反射型dll注入）。

感谢timwhitez师傅及[该项目](https://github.com/timwhitez/Doge-RL)的帮助！

11.2更新：

修正了中文乱码的问题。

10.31更新

新增了C2profile功能

1、适配了metadata的header、parameter、uri-append形式，暂时不支持print，不过要注意**prepend与parameter同时存在的时候好像会解析不了**，请避免同时使用。

2、适配了http-post的id的prepend、append以及parameter、header形式。

3、适配了http-post的output的parameter、header、print形式，暂时不支持uri-append形式。

## 使用方法
本项目支持windows、linux、mac平台的使用。

基础的使用方法可参考原项目，windows有三种推荐的编译方式：

1、go build

2、go build -ldflags "-H windowsgui" 去除黑框

3、go build -ldflags "-H windowsgui -w" 缩小体积并去除黑框

4、go build -ldflags "-H windowsgui -s -w" 缩小体积并去除黑框

**360对部分编译参数有监控，可以尝试用go-strip等项目混淆编译参数，或者尝试用伪造签名等方法，后续我们会考虑增加隐藏黑框的代码，避免使用编译参数来隐藏黑框。**

linux和mac编译的时候添加-ldflags "-s -w"减小程序体积，然后后台运行。

目前项目有部分控制台输出内容，若想删除可在代码中删除。

**最简单的使用方法即为修改config.go中的公钥（此公钥是cs的公钥，不是https的公钥，提取方法可参考[geacon](https://github.com/darkr4y/geacon)介绍）以及C2服务器地址（注意是listener地址，如果是http的listener的话需要将sslHTTP改为plainHTTP），然后C2profile更换为下面的示例即可**

**可以支持域前置，因为只是模拟了cs的发包的协议，把C2地址更改为域前置回连的域名和端口，然后把config.go里面req.Header的host更改为域前置域名，profile不用变，谢谢帮忙测试了的师傅。**

**geacon_pro目前是免杀的。不过如果使用的人较多，会被杀软盯上，我们会尽量保持免杀性，师傅们可尝试用[garble](https://github.com/burrowers/garble)这个项目混淆一下源码。**

**出于免杀性考量，暂时删除掉powershell-import代码，师傅们若想使用可以将commands_windows.go中的PowershellPort注释恢复。**

**部分cs二开版本由于修改了48879该特征，可能会认证失败，如果失败的话可以尝试将meta.go中的0xBEEF更改为jar包二开后的值。可参考鸡哥的这篇[文章](https://bbs.pediy.com/thread-267208.htm)来找jar包中二开后的值。**


## 实现功能
### windows平台支持的功能：
sleep、shell、upload、download、exit、cd、pwd、file_browse、ps、kill、getuid、mkdir、rm、cp、mv、run、execute、drives、powershell-import、powershell、execute-assembly（不落地执行c#）、多种线程注入的方法（可自己更换源码）、spawn、shinject、dllinject（反射型dll注入）、管道的传输、多种cs原生反射型dll注入（mimikatz、portscan、screenshot、keylogger等）、令牌的窃取与还原、令牌的制作、代理发包、自删除等功能。支持cna自定义插件的reflectiveDll、execute-assembly、powershell、powerpick、upload and execute等功能。

由于要规避杀软对fork&&run的检测，暂时令反射型dll注入注入到自身进程中，暂时拿不到回显，请师傅们注意，如果师傅们对如何从CreateThread中拿回显有想法请联系我。

目前由于对其他进程进行反射型dll注入有一些问题，目前无论将反射型dll注入到哪个进程都默认为注入到自身进程，请师傅们注意。

若想再派生一个会话的话，不建议使用spawn，因为spawn派生的是原生cs的beacon，并且为了规避杀软对fork&&run的检测，目前spawn是注入了自身，建议直接用run或者execute执行geacon_pro.exe。

### linux和mac平台支持的功能：
sleep、shell、upload、download、exit、cd、pwd、file_browse、ps、kill、getuid、mkdir、rm、cp、mv、自删除
后续会添加linux与mac平台下后渗透功能

进程管理部分、文件管理部分支持图形化交互

### C2profile：

适配了C2profile流量侧的设置与部分主机侧的设置，支持的算法有base64、base64url、mask、netbios、netbiosu、详情见config.go，这里给出示例C2profile，修改完C2profile后请不要忘记在config.go中对相应位置进行修改：
```
# default sleep time is 60s
set sleeptime "3000";

https-certificate {
    set C "KZ";
    set CN "foren.zik";
    set O "NN Fern Sub";
    set OU "NN Fern";
    set ST "KZ";
    set validity "365";
}

# define indicators for an HTTP GET
http-get {

	set uri "/www/handle/doc";

	client {
		#header "Host" "aliyun.com";
		# base64 encode session metadata and store it in the Cookie header.
		metadata {
			base64url;
			prepend "SESSIONID=";
			header "Cookie";
		}
	}

	server {
		# server should send output with no changes
		#header "Content-Type" "application/octet-stream";
		header "Server" "nginx/1.10.3 (Ubuntu)";
    		header "Content-Type" "application/octet-stream";
        	header "Connection" "keep-alive";
        	header "Vary" "Accept";
        	header "Pragma" "public";
        	header "Expires" "0";
        	header "Cache-Control" "must-revalidate, post-check=0, pre-check=0";

		output {
			mask;
			netbios;
			prepend "data=";
			append "%%";
			print;
		}
	}
}

# define indicators for an HTTP 
http-post {
	# Same as above, Beacon will randomly choose from this pool of URIs [if multiple URIs are provided]
	set uri "/IMXo";
	client {
		#header "Content-Type" "application/octet-stream";				

		# transmit our session identifier as /submit.php?id=[identifier]
		
		id {				
			mask;
			netbiosu;
			prepend "user=";
			append "%%";
			header "User";
		}

		# post our output with no real changes
		output {
			mask;
			base64url;
			prepend "data=";
			append "%%";		
			print;
		}
	}

	# The server's response to our HTTP POST
	server {
		header "Server" "nginx/1.10.3 (Ubuntu)";
    		header "Content-Type" "application/octet-stream";
        	header "Connection" "keep-alive";
       	 	header "Vary" "Accept";
        	header "Pragma" "public";
        	header "Expires" "0";
        	header "Cache-Control" "must-revalidate, post-check=0, pre-check=0";

		# this will just print an empty string, meh...
		output {
			mask;
			netbios;
			prepend "data=";
			append "%%";
			print;
		}
	}
}

post-ex {
    set spawnto_x86 "c:\\windows\\syswow64\\rundll32.exe";
    set spawnto_x64 "c:\\windows\\system32\\rundll32.exe";
    
    set thread_hint "ntdll.dll!RtlUserThreadStart+0x1000";
    set pipename "DserNamePipe##, PGMessagePipe##, MsFteWds##";
    set keylogger "SetWindowsHookEx";
}

```

### 目前需要改进的地方：
* ~~dllinject的BUG（正在修改中）~~
* 堆内存加密目前不稳定，暂未正式使用
* ~~修改部分功能下中文乱码的问题~~
* ~~部分功能暂未支持x86系统（最近太忙了，会尽快改出来）~~

### 未来打算做的：
* 适配更多功能
* 集成免杀工具
* 增加Linux和Mac平台下后渗透功能
* 增加代码混淆
* hook服务端jar包类似冰蝎4.0让用户自定义流量加密特征
* 增加混淆的流量

### 主体代码结构
#### config
* 公钥、C2服务器地址、https通信、超时的时间、代理等设置
* C2profile设置
#### crypt
* 通信需要的AES、RSA加密算法
* C2profile中加密算法的实现
#### packet
* commands为各个平台下部分功能的实现
* execute_assembly为windows平台下内存执行不落地c#的代码
* heap为windows平台下堆内存加密代码
* http为发包的代码
* inject为windows平台下进程注入的代码
* jobs为windows平台下注入cs原生反射型dll并管道回传的代码
* packet为通信所需的部分功能
* token为windows平台下令牌相关的功能
#### services
对packet里面的功能进行了跨平台封装，方便main.go调用
#### sysinfo
* meta为元信息的处理
* sysinfo为不同平台下有关进程与系统的判断及处理
#### main.go
主方法对各个命令进行了解析与执行，以及对结果和错误进行了返回

## 部分功能的实现细节
### shell
shell之前直接调用了golang的os/exec库，现在更改为底层CreateProcess的实现，与run的区别仅在于shell调用了cmd。

### run && execute
run和execute的区别在于，run可以返回执行的结果而execute无回显。底层的实现差别就在于run会通过管道回传执行的结果而execute不会。

shell、run和execute的实现在没有窃取令牌的时候调用了CreateProcess，窃取令牌后调用CreateProcessWithTokenW以令牌权限来执行命令。
### powershell-import
powershell-import部分的实现与cs的思路一样，先把输入的powershell module保存，之后在执行powershell命令的时候本地开一个端口并把module放上去，powershell直接请求该端口进行不落地的powershell module加载，不落地加载powershell module可以对部分杀软进行绕过。

### powershell
powershell命令直接调用了powershell，会被360监控，可以尝试用免杀的方式执行。

### execute-assembly
execute-assembly的实现与cs原生的实现不太一样，cs的beacon从服务端接收的内容的主体部分是c#的程序以及开.net环境的dll。cs的beacon首先拉起来一个进程（默认是rundll32），之后把用来开环境的dll注入到该进程中，然后将c#的程序注入到该进程并执行。考虑到步骤过于繁琐，并且容易拿不到执行的结果，我这里直接用[该项目](https://github.com/timwhitez/Doge-CLRLoad)实现了execute-assembly的功能，但未对全版本windows进行测试。

### 进程注入
进程注入shinject和dllinject采用的是remote注入。

**目前dllinject只支持注入自身的进程，shinject若注入到其他的进程的话要注意杀软对远程线程注入的检测。**

不过如果想执行自己的shellcode的话建议用shspawn，在当前实现中shspawn会注入geacon_pro本身，因此不会被杀软报远程线程注入。

### 反射型dll注入
cs原生反射型dll注入的思路是先拉起来一个rundll32进程，之后把dll注进去执行，但是会被360核晶报远程线程注入。我尝试使用了native或者unhook等方法均失败，最后发现了将dll注入自己是不会被查杀的，因此考虑将cs的fork&run的方式改为注入自己的方式。
由于cs是fork&&run的形式,因此部分dll在结束的时候要执行ExitProcess。

![1666934161850](https://user-images.githubusercontent.com/48757788/198508271-5be424b8-f34c-404b-9646-0e1027713476.png)

但是我们注入自己的话就会把木马主线程退出，因此需要对下发的dll进行简单的修改，将dll中的ExitProcess字符串替换为ExitThread+\x00即可。

dll通过管道将结果异步地回传给服务端。目前的dll反射注入采用了注入自己的方法，后续会实现用户可通过配置文件进行注入方式的更改。

### 令牌
令牌的部分目前实现了令牌的窃取、还原、制作。

### 上线内网不出网主机
考虑到渗透中常常存在着内网主机上线的情况，即边缘主机出网，内网主机不出网的情况。目前实现的木马暂不支持代理转发的功能，但是可以通过设置config.go中的proxy参数，通过边缘主机的代理进行木马的上线。即如果在边缘主机的8080端口开了个http代理，那么在config.go中设置ProxyOn为true，Proxy为`http://ip:8080`即可令内网的木马上线我们的C2服务器。

### 堆内存加密
堆内存加密的方法实现参考了[该文章](https://cloud.tencent.com/developer/article/1949555) 。在sleep之前先将除主线程之外的线程挂起，之后遍历堆对堆内存进行加密。sleep结束后解密并将线程恢复。不过该功能较为不稳定，有时在进行堆遍历的时候会突然卡住或者直接退出，并且考虑到后台可能会有keylogger或portscan这种的持久任务，将线程全部挂起有些不合适，如果有师傅有好的想法欢迎来讨论。同时我不太理解为什么go的time.Sleep函数在其他线程都挂起之后调用会一直沉睡，而调用windows.SleepEx就不会有问题，还望师傅们解答。

### 字符集
由于golang默认对UTF-8进行处理，因此我们对协议协商的字符集进行了统一，windows、linux、mac平台下均为UTF-8，然后将部分返回格式为GBK的数据转为UTF之后再回传，避免了中文乱码问题。



<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.0.1] - 2022-12-11

**更新**  
- 新增了时间反沙箱的设置  
- 优化了部分job的输出  
- 修正了部分情况下分辨率导致的screenshot不完整的BUG  
- 修正了部分情况下linux和mac权限获取错误的BUG

#### [v1.0] - 2022-12-03

**更新**  
- 新增了将geacon_pro转成反射型dll/shellcode的方法  
- 新增了异步执行命令、内置消除黑框、适配cna、自删除、getpriv、timestomp功能  
- 新增了自定义设置使用说明、Remark备注设置、ExecuteKey反沙箱设置、jitter设置  
- 修复了dllinject、inject、drives、内网地址获取等BUG  


<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
