## xtate <https://github.com/sharkocha/xtate>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-C-blue)
![Author](https://img.shields.io/badge/Author-sharkocha-orange)
![GitHub stars](https://img.shields.io/github/stars/sharkocha/xtate.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V2.5.0-red)
![Time](https://img.shields.io/badge/Join-20241029-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->
 
<h1 id="top" ></h1>
<h1 id="whatsthis">🤔 What's this?</h1>

Welcome to Xtate -- A modular all-stack network scanner for next-generation internet surveys!

<h1 id="features">✨ Features</h1>

- Designed for Internet-scale scanning and surveys both in academic and practice:
    - High-speed asynchronous transmission mechanism for packets.
    - Stateless scanning model for application layer(aka. ZBanner).
    - HLTCP(Hybrid-state lightweight TCP stack) in user-space for stateful scanning.
    - etc.
- Modularized interfaces: Custom modules in 4 types can be written to achieve your scanning task.
    - Scan Module
    - Probe Module
    - Generate Module
    - Output Module
- Corresponding modules have been implemented for commonly used functions:
    - Port scanning and host discovery in many ways.
    - Grab service banners within one connection in a complete stateless manner.
    - Obtain TLS info and TLS-based service banner with HLTCP.
    - Service discovery and identification like LZR.
    - Probe Topology like yarrp.
    - etc.
- Full support for IPv6 and can work in LAN.
- ~~Written in advanced and popular C language.~~


<h1 id="tableofcontent">📇 Table of Content</h1>

1. 🎤[Introduction](https://github.com/sharkocha/xtate/blob/xtate/README.md#introduction)
1. 🎨[Design](https://github.com/sharkocha/xtate/blob/xtate/README.md#design)
1. 🤺[Basic Usage](https://github.com/sharkocha/xtate/blob/xtate/README.md#basicusage)
1. 📦[Modules](https://github.com/sharkocha/xtate/blob/xtate/README.md#modules)
    1. [Some Typical Scan Modules](https://github.com/sharkocha/xtate/blob/xtate/README.md#some-typical-scan-modules)
    1. [Some Generalizable Probe Modules](https://github.com/sharkocha/xtate/blob/xtate/README.md#some-generalizable-probe-modules)
    1. [Output Modules](https://github.com/sharkocha/xtate/blob/xtate/README.md#output-modules)
    1. [Generate Modules](https://github.com/sharkocha/xtate/blob/xtate/README.md#generate-modules)
1. 💁[Helps in Detail](https://github.com/sharkocha/xtate/blob/xtate/README.md#-helps-in-detail)
1. 🥽[Scan Rate](https://github.com/sharkocha/xtate/blob/xtate/README.md#scanrate)
1. ❗[️Set Your Firewall](https://github.com/sharkocha/xtate/blob/xtate/README.md#setyourfirewall)
1. 🔨[Build](https://github.com/sharkocha/xtate/blob/xtate/README.md#build)
    1. [Dependencies](https://github.com/sharkocha/xtate/blob/xtate/README.md#dependencies)
    1. [Compile on Linux](https://github.com/sharkocha/xtate/blob/xtate/README.md#compile-on-linux)
    1. [Compile on Windows](https://github.com/sharkocha/xtate/blob/xtate/README.md#compile-on-windows)
1. ✍[Author](https://github.com/sharkocha/xtate/blob/xtate/README.md#author)
1. 📄[Papers](https://github.com/sharkocha/xtate/blob/xtate/README.md#papers)
1. 🪪[License](https://github.com/sharkocha/xtate/blob/xtate/README.md#license)

<h1 id="introduction">🎤 Introduction</h1>

Xtate provides basic ability of super fast asychronous packet sending/receiving and highly extensible architecture.
It allows adding self-define ScanModules or ProbeModules to do different scan task with specific strategy.
All modules could work in a packet send rate which takes up more than 90% of a gigabit of bandwidth in pcap mode and 90% of a 10 gigabit of bandwidth in PFRING mode.

Xtate focuses on large-scale active measurement of obtaining information about protocol themselves and corresponding underlying characteristics in real time.
In other words, Xtate is not good at being a crawler or concentrating on content level detection like other specialized scanners. 
(Although Xtate has that abilities...)

Xtate was originally designed to do all scans for UDP and TCP in complete stateless manner, even obtaining responses over TCP with our **ZBanner** tech.
But some new added features and modules make it be more than stateless.

For example, Xtate could do stateful TCP connection and even get HTTPS reponses after finishing TLS handshake with an improved user space stack what we called **HLTCP(hybrid-state lightweight TCP stack)** which optimized for large-scale scanning.
However, being fast and concise is always our target.

In addition, Xtate supports IPv6 addresses and can be built on Windows and Linux with optional dependencies.

<a href="#top">🔝back to top</a>

<h1 id="design">🎨 Design</h1>

Unlike existing high-speed asynchronous scanners, Xtate enables richer scanning strategies by dividing the scanning process at a fine-grained level into individual functional modules.
This is how Xtate working internally (or you can check it by `xtate --intro`):

```
+--------------------------------------------------------------------------------------------+
|                                                                                            |
|      New Targets Generation     Tx Threads           Packet  Transmit         Tx Threads   |
|     +----------------------+  ------------->  +---------------------------+  ----------->  |
|     | 1.GenerateModule     |  ------------->  | 1.ProbeModule Hello Making|  ----------->  |
|     | 2.Scan Rate Control  |  ------------->  | 2.ScanModule Transmiting  |  ----------->  |
|     +----------------------+                  +---------------------------+                |
|                                                                                            |
|                                                                            ^               |
|                                                                            |               |
|     Packets need to be send   +-----------------------+  Send in priority  |               |
|  +--------------------------->| Pakcets Sending Queue +--------------------+               |
|  |                            +-----------------------+                                    |
|  |                                                                                         |
|  |                                                                                         |
|  |         ScanModule Handling                        ScanModule Validation                |
|  |  +-----------------------------+ Handle Threads +-----------------------+               |
|  |  | 1.ProbeModule Handling      | <------------- | 1.Packet Record       |   Rx  Thread  |
|  |  | 2.OutputModule save results | <------------- | 2.Deduplication       | <-----------  |
|  +--| 3.More packets to send      | <------------- | 3.ProbeModule Validate|               |
|     +-----------------------------+                +-----------------------+               |
|                                                                                            |
+--------------------------------------------------------------------------------------------+
```

The most important of these are the Scan module and the Probe module.
The Scan module is responsible for tasks in the network, transport and sometimes data-link layers during the scanning process (e.g., underlying packet construction, verification, etc.), while the Probe module is responsible for tasks above the transport layer (e.g., payload generation, content detection, etc.).
A Scan module can be used alone (e.g. `icmp-echo` ScanModule), or paired with different Probe modules (e.g., `zbanner` ScanModulea and `http` ProbeModule). By clever design, Probe modules can even be nested with other Probe modules (e.g., `tcp-state` ScanModule, `tls-state` ProbeModule and `http` ProbeModule).
Both Scan modules and Probe modules have own sub-parameters.

This is what ScanModules, ProbeModules and "all-stack" mean (or you can check it by `xtate --intro`):

```
+----------------------------------------------------------------------+
|    Free supporting for new scan strategies and protocols through     |
|    flexible ScanModules and ProbeModules creating and combination    |
|                                                                      |
|     +--------------------+           +-------------------------+     |
|     |  Application Layer +---------->|                         |     |
|     +--------------------+           |     ProbeModules        |     |
|                                      |                         |     |
|     +--------------------+           |       e.g. HTTP         |     |
|     | Presentation Layer +---------->|            DNS          |     |
|     +--------------------+           |            Netbios      |     |
|                                      |            TLS          |     |
|     +--------------------+           |                         |     |
|     |   Session Layer    +---------->|                         |     |
|     +--------------------+           +-------------------------+     |
|                                                                      |
|     +--------------------+           +-------------------------+     |
|     |   Transport Layer  +---------->|                         |     |
|     +--------------------+           |      ScanModules        |     |
|                                      |                         |     |
|     +--------------------+           |       e.g. TCP          |     |
|     |   Network Layer    +---------->|            UDP          |     |
|     +--------------------+           |            ICMP         |     |
|                                      |            NDP          |     |
|     +--------------------+           |            ARP          |     |
|     |   Data-link Layer  +---------->|                         |     |
|     +--------------------+           +-------------------------+     |
|                                                                      |
|     +--------------------+                                           |
|     |   Physical Layer   +---------->     Stop kidding!!!            |
|     +--------------------+                                           |
|                                                                      |
+----------------------------------------------------------------------+
```

Xtate allows and encourages users to write their own modules to accomplish specific scanning tasks.

<a href="#top">🔝back to top</a>

<h1 id="basicusage">🤺 Basic Usage</h1>

Use `xtate --usage` to see the basic usages of xtate.
But actually you can do much more than these if you know xtate deeply by reading helps.

```
usage format:
  xtate [options] [-ip IPs -p PORTs [-scan SCANMODULE [-probe PROBEMODULE]]]

basic use examples of xtate:

  xtate -p 80,8000-8100 -ip 10.0.0.0/8 --rate 10000
      use default TcpSyn ScanModule to scan web ports on 10.x.x.x at 10kpps.
      
  xtate -p u:80 -ip 10.0.0.0/8 -scan udp -probe echo -show info
      use UdpProbe ScanModule to scan UDP 80 port with echo ProbeModule and also
      show info results.
      
  xtate -ip 10.0.0.0/8 -scan icmp-echo -scan-arg "-ttl"
      use IcmpEcho ScanModule to do ping scan and record TTL.
      
  xtate -p 80 -ip 10.0.0.0/8 -scan zbanner -probe http -scan-arg "-banner"
      use ZBanner ScanModule to grab http banners with http ProbeModule and Scan
      Module-specific param.
      
  xtate -p s:38412 -ip 10.0.0.0/8 -scan sctp-init -show fail
      use SctpInit ScanModule to scan SCTP 38412(36412) port and show fail resul
      ts.
      
  xtate -ip 192.168.0.1/24 -scan arp-req -lan
      do ARP scan with LAN mode in local network.
      
  xtate -ip fe80::1/120 -scan ndp-ns -src-ip fe80::2 -fake-router-mac
      do NDP NS scan with a link-local source IP in local network.
```

<a href="#top">🔝back to top</a>

<h1 id="modules">📦 Modules</h1>

## Some Typical Scan Modules

Some scan modules would carry probe modules in same type for different performing.

I only mention some typicals of them here which do not contain much basic ones like `tcp-syn`, `icmp-echo`, etc. Details are in the help document.

- `zbanner`: Send probe payload after construct complete TCP connection and grab the response banner.
All of these happen in **completely stateless manner** so that ZBanner could work in high-speed pachet send rate.
It accept tcp type probe module.
ZBanner tech was born from our research papar.

- `tcp-state`: Do scanning with an hybrid-state lightweight TCP stack what we called HLTCP.
Actually it's stateful scan module and accept state type of probe module.
HLTCP was born from our research paper.
It has basic tcp funtions in large-scale scanning scenario and could touch upper layer service over TLS by pairing with `tls-state` probe module.

- `udp`: Send probe payload in type of udp and try to grab valid response.


## Some Generalizable Probe Modules

However, writing modules in C is not an easy task although it helps writter understand more about principle.
So I try to provide some highly generalizable Scan and Probe modules.
These allows you to just use simple commands, regular expressions, or lua scripts to accomplish most of scanning tasks for POC.

I only present some typicals of them here.
Details are in the help document.

- `hello`: Hello probe use static content set by user and reports banner. We can set a regex to match the response as successed. It is tcp type probe and we have udp and state type version, too.

- `recog`: Recog probe is like Hello probe but use a fingerprint file in Recog xml format to match the response by a bunch of regex. It is useful for version detection. It is tcp type probe and we have udp and state type version, too.

- `http`: For the most import application protocol, we provide Http probe for self-defined http header. We also can set a regex to match the response. It is tcp type probe and we have state type version, too.

- `lua-tcp`: Let a specified lua script with proper implementation as a tcp type probe. It will save a lot of time for use for writing simple probes.

- `lua-udp`: The udp type version of `lua-tcp`.

## Output Modules

I support users to write their own scan or probe modules to present unique scan strategy.
And xtate support to result in a formatted item with standard and self-defined key-value field.
This makes output modules to save results in various ways.

Xtate could save results in text, csv, ndjson, MongoDB, etc.
You can write your own output module for better saving.

## Generate Modules

GenerateModule or Generator is an abstraction for scan targets generation. It makes target generation extensible and flexible.
I expect that users can design their own target generation algorithms, or method like gererating from database or files, even design it with OutputModule together.

<a href="#top">🔝back to top</a>

<h1 id="helpsindetail">💁 Helps in Detail</h1>

Xtate has many parameters for global configuration and sub-parameters for specific modules.
All detailed help information of parameters ared embeded into the program, and I recommend using the compiled binary to view them.
PS: Some of the help info are too long, you can use `less`(`more`) command or output it to files(or `vim`).

See all global parameters and help of xtate.

```
xtate --help
```

See all ScanModules with names and introductions.

```
xtate --list-scan
```

See specified ScanModules with sub-parameters and help info.

```
xtate --help-scan <module-name>
```

See all ProbeModules with names and introductions.

```
xtate --list-probe
```

See specified ProbeModules with sub-parameters and help info.

```
xtate --help-probe <module-name>
```

See all OutputModules with names and introductions.

```
xtate --list-out
```

See specified OutputModules with sub-parameters and help info.

```
xtate --help-out <module-name>
```

See all GenerateModules with names and introductions.

```
xtate --list-gen
```

See specified GenerateModules with sub-parameters and help info.

```
xtate --help-gen <module-name>
```

<a href="#top">🔝back to top</a>

<h1 id="scanrate">🥽 Scan Rate</h1>

Xtate could do scan with a high-speed send rate like ZMap and Masscan but with more functions.
All those tools work on similar sending way like raw socket, libpcap(winpcap) or zero-copy(PFRING/netmap).

Xtate inherent and improve the packet sending way of Masscan which contains multi-thread libpcap/winpcap and PFRING.
And it randomizes the target IP addresses so that it shouldn't overwhelm any distant network.
Xtate could event randomize the source IPv4/IPv6 addresses if needed(Yes, I fixed).

By default, the rate is set to 100 packets/second. To increase the rate to a million use something like --rate 1000000.
When scanning the IPv4 Internet, you'll be scanning lots of subnets, so even though there's a high rate of packets going out, each target subnet will receive a small rate of incoming packets.

However, with IPv6 scanning, you'll tend to focus on a single target subnet with billions of addresses.
Thus, your default behavior will overwhelm the target network.
Networks often crash under the load that xtate can generate.

In addition, Xtate support LAN mode to do NDP or ARP scan.
Set a proper scan rate when operate on your own network.

<h1 id="setyourfirewall">❗ Set Your Firewall</h1>

Xtate needs to avoid responds of system stack when using udp, zbanner or HLTCP scan.
When Linux local system receives a SYN-ACK from the probed target, it responds with a RST packet that kills the connection before Xtate handle.
Same for udp, local system may respond an icmp(port unreachable) while we receive our packets.

The easiest way to prevent this is to assign Xtate a separate IP address.
Or I write some shell scripts to set iptable rules in `firewall` directory both for tcp/udp in IPv4/IPv6.

Note, when we do tcp-syn scan, it's better to let system stack to respond RST automaticly.
But you can also set subparameter `--send-rst` to tcp-syn scan module to let Xtate send rst by itself while we work on Windows or use seperate source IP address on Linux.

<a href="#top">🔝back to top</a>

<h1 id="build">🔨 Build</h1>

Xtate could be built both on Linux and Windows with CMake(>=v3.20) because of cross-platform source code.
And some dependencies are optional, we can give up some modules if the specific dependency libraries cannot be prepared.

## Dependencies

Dependent libraries for building:

- OpenSSL>=1.1.1 (optional or use `-DWITH_OPENSSL=<ON/OFF>` to switch explicitly)
- PCRE2 8bits (optional or use `-DWITH_PCRE2=<ON/OFF>` to switch explicitly)
- LibXml2 (optional or use `-DWITH_LIBXML2=<ON/OFF>` to switch explicitly)
- libbson>=1.7 (optional or use `-DWITH_BSON=<ON/OFF>` to switch explicitly)
- libmongoc>=1.7 (optional or use `-DWITH_MONGOC=<ON/OFF>` to switch explicitly)

Optional dependencies for building won't be compiled with if Cmake didn't find the packages on your system or you can switch off it by CMake parameters.

Dependent libraries for running:

- libpcap(Linux)
- winpcap/npcap(Windows)
- PFRING driver(optional on Linux)
- lua5.3/5.4(optional for lua probe support)

All of them can be installed on Windows in some way you like but always easier on Linux like Ubuntu(e.g. 22/24):

```
sudo apt install \
libpcap-dev \
libssl-dev \
libpcre2-dev \
libxml2-dev \
liblua5.X-0 \
libbson-dev \
libmongoc-dev
```

Use `xtate --version` to check details of version, binary info after building.

## Compile on Linux

Recommended compile suites:

- GCC
- Clang

After dependencies installed we can build xtate by CMake with parameters or with given script quickly:

```
./build.sh [debug]
```

## Compile on Windows

Recommended compile suites:

- MSVC
- MinGW-w64

Generate a Visual Studio solution (e.g. VS2022) and build with MSVC:

```
cd build
cmake .. \
    [-G "Visual Studio 17 2022"] \
    [-DCMAKE_TOOLCHAIN_FILE=<maybe path of your vcpkg toolchain>]
cmake --build . \
    --config <Release/Debug/MinSizeRel/RelWithDebInfo> \
    --parallel 4
```

Generate a unix-style Makefile and build with MinGW-w64 :

```
cd build
cmake .. \
    -G "Unix Makefiles" \
    -DCMAKE_BUILD_TYPE=<Release/Debug>
make -j4
```

<a href="#top">🔝back to top</a>

<h1 id="author">✍ Author</h1>

Xtate was created by Sharkocha:

- email: chenchiyu14@nudt.edu.cn

Original code was written during my master's studies at:

- College of Electronic Engineering, [National University of Defense Technology](https://english.nudt.edu.cn/).
- Anhui Province Key Laboratory of Cyberspace Security Situation Awareness and Evaluation.

The initial version of Xtate was born from [Masscan](https://github.com/robertdavidgraham/masscan/tree/master).
Thanks to Robert Grahm for providing valued programing throughts and code infrastructures.
Also thanks to other excellent open-source projects I refered to and noted in the code.
I've learned more than just finishing my worthless graduate thesis.

<h1 id="papers">📄 Papers</h1>

Some of the Scan and Probe modules with original technology are derived from our papers.
You can see some details of Xtate in theory from them.
I hope that Xtate will be used more in academic researches.
And It would be my honored if you cite our papers about Xtate despite my poor academic writing for a boring degree.

- ZBanner: Fast Stateless Scanning Capable of Obtaining Responses over TCP

```
@misc{chen2024zbanner,
      title={ZBanner: Fast Stateless Scanning Capable of Obtaining Responses over TCP}, 
      author={Chiyu Chen and Yuliang Lu and Guozheng Yang and Yi Xie and Shasha Guo},
      year={2024},
      eprint={2405.07409},
      archivePrefix={arXiv},
      primaryClass={cs.NI}
}
```

- Efficient Application-Layer Scanning with Hybrid-State Lightweight TCP Stack for TLS-based Service Monitoring

```
publishing...
```

**Well...bad papers and thesis, but wonderful scanner**😜

<a href="#top">🔝back to top</a>

<h1 id="license">🪪 License</h1>

Copyright (c) 2024 sharkocha

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published by
the Free Software Foundation, version 3 of the License.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v2.5.0] - 2024-12-04

**更新**  
- 新增支持将元信息输出到指定文件  
- 更新帮助文本  
- 修复一些全局时间操作

#### [v2.4.6] - 2024-11-15

**更新**  
- 修复在特殊环境或低版本编译器上编译和链接错误

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
