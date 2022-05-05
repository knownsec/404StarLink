## DarkEye <https://github.com/zsdevX/DarkEye>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-zsdevX-orange)
![GitHub stars](https://img.shields.io/github/stars/zsdevX/DarkEye.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V4.3.0-red)
![Time](https://img.shields.io/badge/Join-20210120-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## 🚀快速使用

### 1、主机发现

支持多种`loader: tcp、ping、http、nb`

```bash
./dist/superscan_darwin_amd64 -action host -ip 192.168.1.1-254
```

loader: `http` (获取title、server、status、iconHash ...)

```bash
./dist/superscan_darwin_amd64 -action host -loader http -ip 192.168.1.1-254 
```

### 2、网段发现

#### 指定探测协议

支持两种`loader: tcp、ping`

```bash
 ./dist/superscan_darwin_amd64 -action net -loader ping -ip 192.168.1-254 
```

### 3、协议爆破

可查看帮助选取loader，默认为所有协议插件

```bash
./dist/superscan_darwin_amd64 -action risk -loader ssh -p 22  -ip 192.168.1.253 		
```

修改爆破字典

```bash
./dist/superscan_darwin_amd64 -action risk -ip 192.168.1.253 -p 22 -user varbing -pass pass.txt
```

### 4、IP域名碰撞

```bash
./dist/superscan_darwin_amd64 -action ip-host -ip 192.168.1.1-2 -p 80 -host host.txt
```

## ⚡️技巧

1. 查看帮助：`./dist/superscan_darwin_amd64 -h`。

2. 并发说明：当IP数量多时，使用`-t 256`增加IP并发；当端口数量多时，可以使用`-tt 100`增加端口并发。

2. 通过调整`-timeout(ms)`参数适配延迟场景，内网调小些，外网调大些，默认2000ms

4. `-ip`参数灵活，支持：掩码：`a.b.c.d/24`、范围：`a.b.c.1-254`、子网范围 :`a.b.1-254`、IP:`a.b.c.d`

5. `-bar` 显示进度

   ```asp
   mssql    2/1168 [--------------------------------------------------]   0 %
   mysql  201/1168 [========>-----------------------------------------]  17 %
   ssh  201/1168 [========>-------------------------------------------]  17 %
   redis  202/1168 [========>-----------------------------------------]  17 %
   ftp  201/1168 [========>-------------------------------------------]  17 %
   memcached  202/1168 [=======>--------------------------------------]  17 %
   mongodb  100/1168 [===>--------------------------------------------]   9 %
   postgresql 1168/1168 [=============================================] 100 %
   ```

## 🛠 编译安装

```bash
git clone https://github.com/b1gcat/DarkEye.git
./build all

Tips:编译好后文件都自动发布到dist目录下
```


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
