## geacon_pro <https://github.com/H4de5-7/geacon_pro>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-H4de5-orange)
![GitHub stars](https://img.shields.io/github/stars/H4de5-7/geacon_pro.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.3.0-red)
![Time](https://img.shields.io/badge/Join-20221117-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

本项目基于[geacon](https://github.com/darkr4y/geacon)项目对cobaltstrike的beacon进行了重构，并适配了大部分Beacon的功能，支持4.1+版本。

目前实现的功能具备免杀性，可过Defender、360核晶、卡巴斯基（除注入原生cs的dll、可注入无特征dll）、火绒

上述测试环境均为实体机

**为了预防杀软对本项目的部分特征进行监控，推荐师傅们使用garble对本项目进行混淆，使用注意事项请见下面的使用方法介绍。同时我们会实时跟踪杀软的动向并尽快更新，如果有杀软查杀了还望师傅们提issue说明。**

**该项目会持续跟进免杀的技术，保持项目的免杀性，并将免杀的技术与工具集成进来，希望未来可以做成不仅限cs功能的跨平台后渗透免杀工具。如果师傅们有相关的需求或者想法，欢迎一起来讨论。师傅们的支持与讨论是我们前进的动力。**

本项目与好兄弟Z3ratu1共同开发，他实现了一版支持4.0版本的[geacon_plus](https://github.com/Z3ratu1/geacon_plus)，我这边实现了一版支持4.1及以上版本的beacon，大致功能类似，有部分功能不同。

由于本人对二进制方向接触的不多，希望师傅们多多包涵，欢迎师傅们交流，欢迎指出问题。

## 二、免责声明
**该项目仅用于对CobaltStrike协议的学习测试以及合法的渗透测试。请勿使用于任何非法用途，由此产生的后果自行承担。**

## 三、实现功能
本项目支持windows、linux、mac平台的使用。
### windows平台支持的功能：
sleep、shell、upload、download、exit、cd、pwd、file_browse、ps、kill、getuid、mkdir、rm、cp、mv、run、execute、drives、powershell-import、powershell命令混淆、powerpick、psinject、免杀bypassuac（uac-token-duplication）、免杀系统服务提权（svc-exe）、execute-assembly、多种线程注入的方法（可自己更换源码）、spawn、inject、shinject、dllinject、管道的传输、多种cs原生反射型dll注入（mimikatz、portscan、screenshot、keylogger等）、令牌的窃取与还原、令牌的制作、权限的获取、runu父进程欺骗、argue欺骗、代理发包、自删除、timestomp更改文件时间、unhook等功能。支持cna自定义插件的reflectiveDll、execute-assembly、powershell、powerpick、upload and execute等功能。

目前powershell命令的混淆可过defender、卡巴等，过不了360，若想使用原生非混淆powershell请使用shell powershell。

### linux和mac平台支持的功能：
sleep、shell、upload、download、exit、cd、pwd、file_browse、ps、kill、getuid、mkdir、rm、cp、mv、自删除、timestomp
后续会添加linux与mac平台下后渗透功能

进程管理部分、文件管理部分支持图形化交互

### C2profile：

适配了C2profile流量侧的设置与部分主机侧的设置，支持的算法有base64、base64url、mask、netbios、netbiosu、详情见config.go。


## 四、使用方法

有以下两种使用的方法，师傅们可以根据自己的喜好来灵活地使用：

### 第一种使用方法：直接编译成exe执行

#### 1、修改公钥
修改config.go中的公钥RsaPublicKey（此公钥是cs的公钥，不是https的公钥，提取方法可参考[geacon](https://github.com/darkr4y/geacon)介绍。

#### 2、修改C2地址
修改config.go中的C2地址（注意是listener地址，如果是http的listener的话需要将sslHTTP改为plainHTTP）。

域前置设置（可选）：把C2地址更改为域前置回连的域名和端口，然后把config.go里面req.Header的host更改为域前置域名。

#### 3、适配C2profile
config.go中设置了大部分C2profile流量端设置与部分主机端设置。

C2profile暂时不要设置post-ex中的obfuscation以及data_jitter。

如果快速使用的话可以直接使用示例的c2profile（其实示例c2profile流量侧已经配置了不少东西了）不需要修改config.go。如果自己配置可以根据config.go中具体的字段名称来对应，比如说Http_post_id_crypt=[]string{"mask", "netbiosu"}对应着c2profile中的http-post中的id里面的mask;和netbiosu;。我们下个阶段主要的任务是简化配置的过程。

**修改完C2profile后请不要忘记在config.go中对相应位置进行修改。下面给出示例C2profile，默认config.go适配该C2profile：**

```
# default sleep time is 60s
set sleeptime "3000";
set jitter "7";

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

#### 4、编译成exe并执行
windows有三种推荐的编译方式：

注意已实现了内置去黑框功能，不需要"-H windowsgui"参数了，但是目前仍有一闪而过的黑框。

* go build

* go build -ldflags "-H windowsgui" 去除黑框（已内置代码）

* go build -ldflags "-s -w" 缩小体积

**360对部分编译参数如-s -w有监控，可以在linux或mac平台下交叉编译exe，经测试不会被360监控。推测360对符号表这些进行了监控，如果不存在则报，但不知道为啥交叉编译之后就可以。。**

**如果想混淆的话推荐使用garble项目对变量名、函数名、字符串进行混淆，但最好在linux或mac平台下交叉编译，因为garble自带-s -w会被360监控。**

linux和mac编译的时候添加-ldflags "-s -w"减小程序体积，然后后台运行。

### 第二种使用方法：转成反射型dll/shellcode的形式以加载器方式来灵活加载

前三步与第一种方法相同。

#### 编译为反射型dll/shellcode
师傅们如果不想局限于使用geacon_pro生成的exe，可以使用[该项目](https://github.com/WBGlIl/go-ReflectiveDLL)将geacon_pro转换成反射型dll/shellcode的形式后使用加载器来加载，进而达成千人千面的免杀形式。师傅们若觉得转换后的体积较大，可以用下载器的方式来远程stager加载。将geacon_pro目录下文件移到该项目目录下之后，将main.go原本的main函数更名为OnPorcessAttach并标注导出函数export，之后添加import "C"并新增main()函数即可，最后用x64.bat编译（可以自定义编译的参数）并生成反射型dll。main.go示例如下：

```
package main

import "C"
import (
	"bytes"
	"errors"
	"fmt"
	"main/config"
	"main/crypt"
	"main/packet"
	"main/services"
	"os"
	"strings"
	"time"
)

func main() {
    //fmt.Println("123")
}
//export OnProcessAttach
func OnProcessAttach() {
	......//原本main函数里面的内容
	......
	......
}

```

### 自定义设置

config.go中有一些自定义的设置：

* Proxy设置代理发包的功能，详情见实现细节。
* Remark可以在上线的时候备注机子，方便区分不同应用场景。即如果Remark=“test”，上线机子的名称会被设置成为 ComputerName [test]。
* ExecuteKey可以进行简单的反沙箱，若密钥值为password，设置后执行的时候需要geacon_pro.exe password才可执行成功，沙箱或蓝队成员由于不知道密钥，因此无法执行。
* ExecuteTime可以进行简单的反沙箱，若当前时间晚于设置的时间则执行失败，师傅们注意该设置是UTC时区。
* DeleteSelf设置是否自删除。
* HideConsole设置是否内置隐藏黑框。
* CommandReadTime设置异步实时回显长命令的间隔时间。

## 五、其他注意事项与免杀手段

1、geacon_pro基于原生cs进行的开发，部分二开的版本可能会兼容错误，需要在geacon_pro中修改代码以适配二开的版本。

2、若想用免杀捆绑器的话可以参考我的这个[小项目](https://github.com/H4de5-7/Bundler-bypass)。

3、若想用免杀计划任务的话可以参考我的这个[小项目](https://github.com/H4de5-7/schtask-bypass)以及一个师傅的这个[项目](https://github.com/0x727/SchTask_0x727)（不过这个项目需要用execute-assembly来内存执行）。

4、如果师傅们对堆内存加密或者dllinject注入自己拿回显有想法，欢迎来交流。

## 六、开发的思路
<details><summary>点击展开</summary>

### 整体的思路
传统cs的免杀偏向于如何加载上线，但是杀软对beacon的特征查得非常严，尤其是卡巴这种查内存的，因此不如自己重构一个。

免杀主要体现在三个方面:
* 由于是重构的，因此没有beacon的特征，针对beacon特征的杀软是检测不出来的。
* golang本身具备一定的免杀性
* 针对各功能实现了免杀，cs部分不免杀的功能得到了更换

### 主体代码结构
#### communication
* http为发包的代码
* packet为通信所需的部分功能
#### config
* 公钥、C2服务器地址、https通信、超时的时间、代理等设置
* C2profile设置
#### crypt
* 通信需要的AES、RSA加密算法
* C2profile中加密算法的实现
#### packet
* commands为各个平台下部分功能的实现
* commands_type为beacon的命令
* evasion为规避杀软的代码
* execute_assembly为windows平台下内存执行不落地c#的代码
* heap为windows平台下堆内存加密代码
* inject为windows平台下进程注入的代码
* jobs为windows平台下注入cs原生反射型dll并管道回传的代码
* spoof为windows平台下欺骗相关的功能
* token为windows平台下令牌相关的功能
#### services
对packet里面的功能进行了跨平台封装，方便main.go调用
#### sysinfo
* meta为元信息的处理
* sysinfo为不同平台下有关进程与系统的判断及处理
#### main.go
主方法对各个命令进行了解析与执行，以及对结果和错误进行了返回

### 部分功能的实现细节
#### shell
shell之前直接调用了golang的os/exec库，现在更改为底层CreateProcess的实现，与run的区别仅在于shell调用了cmd。

#### run && execute
run和execute的区别在于，run可以返回执行的结果而execute无回显。底层的实现差别就在于run会通过管道回传执行的结果而execute不会。

shell、run和execute的实现在没有窃取令牌的时候调用了CreateProcess，窃取令牌后调用CreateProcessWithTokenW以令牌权限来执行命令。
#### powershell-import
powershell-import部分的实现与cs的思路一样，先把输入的powershell module保存，之后在执行powershell命令的时候本地开一个端口并把module放上去，powershell直接请求该端口进行不落地的powershell module加载，不落地加载powershell module可以对部分杀软进行绕过。

#### powershell
集成了powershell命令混淆免杀（AMSI绕过+ETW block+命令的混淆），VT全过，详情见我的[该项目](https://github.com/H4de5-7/powershell-obfuscation)。

#### 提权
集成了免杀bypassuac，即execute-assembly执行COM绕过的exe。集成了免杀系统服务提权，详情见 https://github.com/H4de5-7/elevate-bypass 。

#### execute-assembly
execute-assembly的实现与cs原生的实现不太一样，cs的beacon从服务端接收的内容的主体部分是c#的程序以及开.net环境的dll。cs的beacon首先拉起来一个进程（默认是rundll32），之后把用来开环境的dll注入到该进程中，然后将c#的程序注入到该进程并执行。考虑到步骤过于繁琐，并且容易拿不到执行的结果，我这里直接用[该项目](https://github.com/timwhitez/Doge-CLRLoad)实现了execute-assembly的功能，但未对全版本windows进行测试。

#### 进程注入
进程注入shinject、dllinject、psinject采用的是remote注入。

不过如果想执行自己的shellcode的话建议用shspawn，在当前实现中shspawn会注入geacon_pro本身，因此不会被杀软报远程线程注入。

#### 反射型dll注入
cs原生反射型dll注入的思路是先拉起来一个rundll32进程，之后把dll注进去执行，但是会被360核晶报远程线程注入。我尝试使用了native或者unhook等方法均失败，最后发现了将dll注入自己是不会被查杀的，因此考虑将cs的fork&run的方式改为注入自己的方式。
由于cs是fork&&run的形式,因此部分dll在结束的时候要执行ExitProcess。

![1666934161850](https://user-images.githubusercontent.com/48757788/198508271-5be424b8-f34c-404b-9646-0e1027713476.png)

但是我们注入自己的话就会把木马主线程退出，因此需要对下发的dll进行简单的修改，将dll中的ExitProcess字符串替换为ExitThread+\x00即可。

dll通过管道将结果异步地回传给服务端。目前的dll反射注入采用了注入自己的方法，后续会实现用户可通过配置文件进行注入方式的更改。

#### 令牌
令牌的部分目前实现了令牌的窃取、还原、制作、权限的获取。

#### 上线内网不出网主机
考虑到渗透中常常存在着内网主机上线的情况，即边缘主机出网，内网主机不出网的情况。目前实现的木马暂不支持代理转发的功能，但是可以通过设置config.go中的proxy参数，通过边缘主机的代理进行木马的上线。即如果在边缘主机的8080端口开了个http代理，那么在config.go中设置ProxyOn为true，Proxy为`http://ip:8080`即可令内网的木马上线我们的C2服务器。

#### 堆内存加密
堆内存加密的方法实现参考了[该文章](https://cloud.tencent.com/developer/article/1949555) 。在sleep之前先将除主线程之外的线程挂起，之后遍历堆对堆内存进行加密。sleep结束后解密并将线程恢复。不过该功能较为不稳定，有时在进行堆遍历的时候会突然卡住或者直接退出，并且考虑到后台可能会有keylogger或portscan这种的持久任务，将线程全部挂起有些不合适，如果有师傅有好的想法欢迎来讨论。同时我不太理解为什么go的time.Sleep函数在其他线程都挂起之后调用会一直沉睡，而调用windows.SleepEx就不会有问题，还望师傅们解答。

#### 字符集
由于golang默认对UTF-8进行处理，因此我们对协议协商的字符集进行了统一，windows、linux、mac平台下均为UTF-8，然后将部分返回格式为GBK的数据转为UTF之后再回传，避免了中文乱码问题。

#### 自删除
CobaltStrike貌似没有做自删除的功能，我们添加了不同平台下的自删除功能。windows平台下由于进程未退出的时候是无法自己删除自己的，常用的方法有bat与远程线程注入。 远程线程注入的缺点前面也提到了容易被杀软监控，因此我们这里简化了一下bat自删除，用CreateProcess新起了一个自删除进程并设置为空闲时间执行，自删除进程在geacon_pro进程执行完之后删除它。Linux平台下可以直接删除正在执行的进程的文件。

#### 欺骗
实现了父进程的欺骗、argue欺骗

#### 规避
实现了windows平台下的full unhook，这里原本参考了sliver的evasion实现，但是sliver里面没有用直接系统调用，可能会被杀软监控到，因此我们用timwhitez师傅的这个[项目](https://github.com/timwhitez/Doge-Gabh)实现了full unhook。

</details>

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.3.0] - 2023-02-05

**更新**  
- 新增unhook(ntdll.dll,kernel32.dll,kernelbase.dll)  
- 新增argue欺骗  
- 修复了drives的错误，如：keylogger中文会乱码、dllinject远程注入失败等  
- 将os.Exit(0)修改为return，避免转换成反射型dll注入后退出宿主进程  
- 优化代码结构与sysinfo的显示

#### [v1.2.0] - 2023-01-02

**更新**  
- 集成了svc-exe系统服务的免杀system提权  
- 新增了runu父进程欺骗、恢复了powershell-import  
- 修复了特定情况下screenshot显示、sedebug函数错误、部分指令判断错误的BUG

#### [v1.1.0] - 2022-12-18

**更新**  
- 集成了powershell命令混淆免杀(AMSI绕过+ETW block+命令混淆)，VT全过  
- 集成了免杀bypassuac  
- 新增了linux/macos下的timestomp，增加了公钥错误的回显  
- 修复了部分异步命令回显出错、screenshot中文乱码、windows平台下timestomp出错的BUG

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
