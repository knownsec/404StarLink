## GrabAccess <https://github.com/Push3AX/GrabAccess>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-C-blue)
![Author](https://img.shields.io/badge/Author-Push3AX-orange)
![GitHub stars](https://img.shields.io/github/stars/Push3AX/GrabAccess.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.1-red)
![Time](https://img.shields.io/badge/Join-20240805-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## GrabAccess

**Bookit / Windows登陆密码和Bitlocker绕过工具**

------

[**中文**](https://github.com/Push3AX/GrabAccess/blob/main/readme_cn.md) | [English](https://github.com/Push3AX/GrabAccess/blob/main/readme.md)

在物理接触的情况下，GrabAccess可以：

1. 绕过Windows登陆密码执行任意操作（以System权限执行命令、重置Windows账户密码等）
2. 植入木马并添加自启动（可以绕过Bitlocker，但要求受害者登录）
3. 通过修改主板UEFI固件实现无视重装系统、更换硬盘的持久化（Bootkit）



## 快速开始

GrabAccess最基础的功能是绕过Windows登录密码。

1. 准备一个U盘。（需为`FAT16`或`FAT32`格式）

2. 下载[GrabAccess_Release.zip](https://github.com/Push3AX/GrabAccess/releases/download/Version1.1/GrabAccess_Release_1.1.0.zip)，解压到U盘根目录。

   ![1](https://raw.githubusercontent.com/Push3AX/GrabAccess/main/images/1.png)

3. 将U盘插入目标计算机。重启，在启动时进入BIOS菜单。选择从U盘启动（如果开启了`Security Boot`，还需将其设置为`DISABLE`）.

   ![2](https://raw.githubusercontent.com/Push3AX/GrabAccess/main/images/2.png)

4. 在Windows启动时会弹出CMD窗口和账户管理窗口，可以System权限执行任意命令而无需登录。

   ![3](https://raw.githubusercontent.com/Push3AX/GrabAccess/main/images/3.png)

5. 按下`ALT+F4`关闭CMD窗口后，Windows回到登陆界面。



## 自动化植入（支持绕过 Bitlocker）

GrabAccess可以自动植入指定的程序，并为其添加启动项。

要使用该功能，需要预先将GrabAccess与要植入的程序打包：

1. 下载[GrabAccess_Release.zip](https://github.com/Push3AX/GrabAccess/releases/download/Version1.1/GrabAccess_Release_1.1.0.zip)，解压并放置在U盘根目录。

2. 将需要植入的程序命名为`payload.exe`，放置在U盘根目录。

3. 运行`build.bat`进行打包。

   ![4](https://raw.githubusercontent.com/Push3AX/GrabAccess/main/images/4.png)

4. 将U盘插入目标计算机、从U盘启动（与前文相同）

5. Windows启动后即可看到指定的程序。

![5](https://raw.githubusercontent.com/Push3AX/GrabAccess/main/images/5.png)

该植入过程可以绕过Bitlocker的系统盘加密。

从含有GrabAccess的U盘启动后，GrabAccess就会写入到内存中。此时可以拔出U盘，但需要停留在Bitlocker输入密码的界面，等待受害者返回输入密码。当Bitlocker解锁之后，指定的程序会被写入磁盘。但在这之前，由于GrabAccess仅停留在内存，如果重启或关机，GrabAccess将会失效。



## 修改主板UEFI固件实现Bootkit

GrabAccess可以被植入到计算机主板的UEFI固件。实现硬件级别的持久化（Bootkit）。

每次Windows系统启动时，GrabAccess会植入指定的程序，即使重装系统或更换硬盘之后也会重新植入。要移除它，只能刷写主板固件或更换主板。

**警告：以下操作可能损坏主板！必须对UEFI固件有一定了解才可继续。AT YOUR OWN RISK !!!!**

要实现这一功能，大致分为四步：

1. 将GrabAccess与要植入的程序打包
2. 提取主板UEFI固件
3. 向UEFI固件插入GrabAccessDXE
4. 将固件刷回主板

不同主板的第2和第4步有较大不同。部分主板可以通过软件方式刷新固件，但也有部分主板存在校验，只能使用编程器刷新。因差异众多，在此不深入讨论，读者可以自行在网上搜索某型号主板对应的方式。

将GrabAccess与要植入的程序打包的方式与前文相同，即：将需要植入的程序命名为payload.exe，放置在GrabAccess的根目录，运行build.bat进行打包。结束后得到`native.exe`，稍后将会用到。

在提取到主板UEFI固件后，使用[UEFITool](https://github.com/LongSoft/UEFITool)打开，按下`Ctrl+F`，选择`Text`，搜索`pcibus`，在下方双击搜索到的第一项。

![6](https://raw.githubusercontent.com/Push3AX/GrabAccess/main/images/6.png)

在`pcibus`这一项上右键，选择`Insert before`，然后选取[GrabAccess_Release.zip](https://github.com/Push3AX/GrabAccess/releases/download/Version1.1/GrabAccess_Release_1.1.0.zip)中`UEFI_FSS`文件夹的`GrabAccessDXE.ffs`。

![7](https://raw.githubusercontent.com/Push3AX/GrabAccess/main/images/7.png)

插入`GrabAccessDXE`后，在`GrabAccessDXE`上右键，选择`Insert before`，插入`UEFI_FSS`文件夹的`native.ffs`。此时应该如下所示：

![8](https://raw.githubusercontent.com/Push3AX/GrabAccess/main/images/8.png)

双击展开`native.ffs`（它没有名字，但GUID是`2136252F-5F7C-486D-B89F-545EC42AD45C`），在`Raw section`上右键，选择`Replace body`，然后选取前文中生成的`native.exe`进行替换。

![9](https://raw.githubusercontent.com/Push3AX/GrabAccess/main/images/9.png)

最后，点击File菜单的`Save image file`，保存固件到文件。

这份固件已经成功植入了Bootkit，将其刷回主板。如果一切顺利，在每一次Windows启动过程中，`native.exe`都会被写入并执行。

如果没有成功，可以尝试以下操作：

1. 关闭UEFI设置中的`Security Boot`和`CSM`，确定操作系统是通过UEFI模式加载的。
2. 向固件插入`UEFI_FSS`文件夹下的`pcddxe.ffs`（方法同前文。但注意，这个模块可能会与其它模块冲突造成不能开机，仅建议在使用编程器的情况下尝试！）



## 系统支持情况

GrabAccess仅支持UEFI引导下的Windows系统，目前仅支持x64系统。

已测试Windows 10 (1803, 22H2)和Windows 11(23H2)。包括使用了TPM、联网账户、Pin码的情况。但不支持绕过Security Boot。



# 原理解析

## Windows Platform Binary Table

和Kon-boot篡改Windows内核不同，GrabAccess的工作原理，源自于Windows的一项合法后门：WPBT（Windows Platform Binary Table）。

WPBT常用于计算机制造商植入驱动管理软件、防丢软件。类似Bootkit病毒，一旦主板中存在WPBT条目，无论是重装系统还是更换硬盘，只要使用Windows系统，开机后都会被安装指定程序。

WPBT的原始设计，应当是由生产商在主板的UEFI固件中插入一个特定的模块实现。但是，通过劫持UEFI的引导过程，攻击者可以插入WPBT条目，而无需修改主板固件。



## GrabAccess做了什么

GrabAccess包含两个部分。

其一是用于写入WPBT条目的UEFI应用程序，即源码中的Stage1-UEFI。它们用于在UEFI环境下向ACPI表写入WPBT条目。

其二是一个Windows Native Application，即源码中的Stage2-NativeNT，用于写出最终Payload和添加启动项。



## Native Application做了什么

WPBT所加载的应用程序，并非常规的Win32程序。而是一个Windows Native Application。它在Windows Native NT阶段执行，早于用户登录。但是Windows提供给Native APP的API，也少于Win32程序。	

源码中的Stage2-NativeNT负责将其末尾的最终Payload（即用户打包的指定程序）写出到`C:\\Windows\\System32\\GrabAccess.exe`，并为其添加启动项`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run\GrabAccess`。

如果其末尾没有Payload，则通过IFEO劫持Logonui.exe，在Windows登录时显示cmd.exe和netplwiz.exe



## Credits

1. [Windows Platform Binary Table (WPBT) ](https://download.microsoft.com/download/8/a/2/8a2fb72d-9b96-4e2d-a559-4a27cf905a80/windows-platform-binary-table.docx)
2. [WPBT-Builder ](https://github.com/tandasat/WPBT-Builder)
3. [Windows Native App by Fox](http://fox28813018.blogspot.com/2019/05/windows-platform-binary-table-wpbt-wpbt.html)


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
