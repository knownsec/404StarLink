## ct <https://github.com/knownsec/ct>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Rust-blue)
![Author](https://img.shields.io/badge/Author-rungobier@Knownsec404-orange)
![GitHub stars](https://img.shields.io/github/stars/knownsec/ct.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.9-red)
![Time](https://img.shields.io/badge/Join-20211213-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

ct 是一款使用 rust 语言进行开发，并且基于 ZoomEye 域名查询以及利用域名字典进行子域名爆破的工具，同时在最终爆破完成后， 自动生成 Windows/*nix 下的可执行脚本。 脚本内容为自动将相应的的.gv 文件转化成为相应的
.png 文件，graphviz 下载安装请参见 [graphviz](https://graphviz.org/download/)
支持在Windows/Linux/Mac上使用。

## 编译环境构建

*nix 编译环境执行如下指令即可安装：

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
Windows 编译环境安装请下载[rustup-init.exe](https://static.rust-lang.org/rustup/dist/i686-pc-windows-gnu/rustup-init.exe)并执行。


## 使用

从[releases](https://github.com/knownsec/ct/releases "releases")下载二进制文件。

```
ct 1.0.9
Autor: rungobier@knownsec 404 team <rungobier@gmail.com>
Collect information tools about the target domain.

USAGE:
    ct_win64.exe [FLAGS] [OPTIONS] [domain]

FLAGS:
    -E                Extended analysis domain
    -T                Network upload speed test.
    -Z                Do not use zoomeye data
    -C, --cidr        Convert the IP related to the target domain name to cidr for extended search. Default is false.
    -h, --help        Prints help information
    -i, --info        Get ZoomEye account base info
    -q, --query-ip    Use zoomeye to query ip information
    -V, --version     Prints version information

OPTIONS:
        --init <apikey>                Initialize the ZoomEye api key
    -s, --dns-dict <dns-file>          DNS Server list in a textual file.
                                       file example...
                                       8.8.8.8
                                       1.1.1.1
                                       ...
    -d, --domain-dict <domain-file>    Domain dict list in a file.
                                       file example....
                                       www
                                       mail
                                       dev
                                       ...
    -F <filter-domains>                Extended filter domain list.
                                       Example of extended filtering domain name list:
                                       knownsec.com,jiasule.com,365cyd.com...
        --query-num <query-num>        Maximum number of zoomeye query. Default query number 100
    -t, --threads <thread-num>         Maximum number of threads. Default number $CPU_NUM
    -w, --work-dir <work-dir>          Directory to save the results of tasks. Default
                                       [/tmp|$DESKTOP]/YYYYmmddHHMM_$DOMAIN

ARGS:
    <domain>    Target domain name

```

### 常用命令

```
ZoomEye apikey 初始化
ct --init 62EC1239-xxxx-xxxxx-xxxx-e45291301ee

开启扩展搜索
ct -E 

过滤域名，域名之间以,分隔
ct -F

查看ZoomEye账号信息
ct -i

上行网络测速 (使用了speedtest库)
ct -T

利用zoomeye的域名查询进行的懒人模式 默认每账号每天2万条查询结果
ct baidu.com

使用域名字典爆破
ct -d domain_dict.txt baidu.com

使用指定dns域名解析服务器及字典进行爆破(不使用ZoomEye数据加-Z，默认不加为合并) 字典路径需要带完整路径
ct -Z -d domain_dict.txt -s dns.txt baidu.com
```

## 域名以及IP关系图形生成

*nix

```bash
cd /tmp/202111301212_baidu.com
chmod +x convert2png.sh
./convert2png.sh
ls *.png
```

Windows

```bat
cd C:\Users\rungobier\Desktop\202111301212_baidu.com
convert2png.bat
dir *.png
```

最终生成的效果图如下：

![域名维度](https://github.com/knownsec/ct/raw/main/images/domain_graph.gv.svg)

## 编译

```bash
git clone https://github.com/knownsec/ct
cd ct
cargo build --release
./target/release/ct 
```

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

#### [v1.0.9] - 2022-07-18

**更新**  
- 加入域名自动扩展搜索参数 -E- 加入无效域名过滤参数 -F， 同时自带过滤清单- 修改部分bug

**Example**  
- `ct -E -F 365cyd.cn,jiashule.com,365cyd.com,knownsec.com baidu.com`

#### [v1.0.5] - 2022-01-13

**新增**  
- 加入查询IP开关参数

**优化**  
- 调整网速测试的代码

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
