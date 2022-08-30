## Cloud-Bucket-Leak-Detection-Tools <https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-UzJu-orange)
![GitHub stars](https://img.shields.io/github/stars/UzJu/Cloud-Bucket-Leak-Detection-Tools.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.4.0-red)
![Time](https://img.shields.io/badge/Join-20220829-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


```bash
git clone https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools.git
cd Cloud-Bucket-Leak-Detection-Tools/
# 安装依赖 建议使用Python3.8以上的版本 我的版本: Python 3.9.13 (main, May 24 2022, 21:28:31)
# 已经测试版本如下
# 1、python3.8.9
# 2、python3.9.13
# 3、python3.7
# 4、python3.6.15
# 5、python3.9.6
pip3 install -r requirements.txt
python3 main.py -h
```

![image-20220716140707903](https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools/raw/main/images/image-20220716140707903.png)

使用之前需要在`config/conf.py`文件配置自己对应的云厂商AK

![image-20220716140934866](https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools/raw/main/images/image-20220716140934866.png)

## 1、阿里云存储桶

### 1.1、单个存储桶检测

```bash
python3 main.py -aliyun [存储桶URL]
```

![image-20220716141132931](https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools/raw/main/images/image-20220716141132931.png)

### 1.2、自动存储桶劫持

当如果检测存储桶不存在时会自动劫持该存储桶

![image-20220703202339058](https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools/raw/main/images/image-20220703202339058.png)

### 1.3、批量存储桶地址检测

```bash
# fofa语法
domain="aliyuncs.com"
server="AliyunOSS"domain="aliyuncs.com"
```

```bash
# 使用-faliyun
python3 main.py -faliyun url.txt
```

![image-20220716141356518](https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools/raw/main/images/image-20220716141356518.png)

## 2、腾讯云存储桶

```bash
python3 main.py -tcloud [存储桶地址]
```

![image-20220716141554856](https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools/raw/main/images/image-20220716141554856.png)

## 3、华为云存储桶

```bash
python3 main.py -hcloud [存储桶地址]
```

![image-20220716141948046](https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools/raw/main/images/image-20220716141948046.png)

## 4、AWS存储桶

```bash
python3 main.py -aws [存储桶地址]
```

![image-20220716142431142](https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools/raw/main/images/image-20220716142431142.png)

## 5、扫描结果保存

扫描结果会存放在`results`目录下

![image-20220716142617997](https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools/raw/main/images/image-20220716142617997.png)

![image-20220716142641883](https://github.com/UzJu/Cloud-Bucket-Leak-Detection-Tools/raw/main/images/image-20220716142641883.png)


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
