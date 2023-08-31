## LBot <https://github.com/knownsec/LBot>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-LoRexxar@knownsec404-orange)
![GitHub stars](https://img.shields.io/github/stars/knownsec/LBot.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.0.1-red)
![Time](https://img.shields.io/badge/Join-20200921-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


LBot的基础模型是脱胎于LSpider诞生的多线程任务调度模型。

主要是用于方便的写一个xss的bot程序。

使用者可以简单的修改其逻辑以及配置环境，即可获得一个简单的xss的bot程序。由于原型来自于爬虫程序，所以只要前端有一定的频率限制，后端很难出现问题，比较稳定。

# install

## 下载Lbot

```
git clone https://github.com/knownsec/LBot.git
```

## 修改配置文件

```
cp LBot/settings.py.bak LBot/settings.py
```

并配置其中相关的mysql配置

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'disable',
        'USER': 'root',
        'PASSWORD': '',
        'HOST': '127.0.0.1',
        'PORT': '3306',
        'OPTIONS': {
            'init_command': 'SET default_storage_engine=INNODB;SET NAMES utf8mb4',
            'charset': 'utf8mb4',
        },
        'TEST': {
            'CHARSET': 'utf8',
            'COLLATION': 'utf8_general_ci',
        },
    }
}
```
## 配置环境

```
python3 -m pip install django
```

如果mysqlclient无法安装，还需要提前安装

```
sudo apt-get install libmysqlclient-dev
```

## 同步数据库配置

```
python3 manage.py makemigrations
python3 manage.py migrate
```

## 配置chrome headless

```
sudo wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/

wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -

sudo apt-get update

sudo apt-get install google-chrome-stable
```

看一下chrome的版本

```bash
lorexxar@instance-1:~/lorexxar/lspider/LSpider$ google-chrome --version
Google Chrome 81.0.4044.138 
```

去官网下载对应版本的webdriver放在bin目录下

```
https://chromedriver.chromium.org/downloads
```

修改名字
```bash
mv bin/chromedriver bin/chromedriver_linux64

```

## 针对守护的xss题目魔改bot程序

主流的xss bot守护方式一共有两种，一种是依靠cookie或者ip限制bot访问，另一种是通过登录账号模拟管理员的bot。

```
# Bot admin pass
CTF_BACK_USER = 'admin'
CTF_BACK_PASS = 'adminsecretpass'
CTF_BACK_COOKIE = "s3cr3t_k3y_f0r_4dmin"
```

如果是依赖cookie的需要设置HOME_PAGE
```
# homepage

HOME_PAGE = "http://127.0.0.1/index.php"
```

核心bot部分主要在`Botend\views.py` function `LBotCore`

```
    reportt = ReportTask.objects.filter(aread=0).first()
    
    if not reportt:
        continue
    
    # 任务锁
    reportt.aread = 1
    reportt.save()
    
    # cookie 方式
    report_url = reportt.url
    cookies = "admin="+CTF_BACK_COOKIE
    
    self.req = LReq(is_chrome=True)
    
    # 访问目标
    self.req.get(report_url, 'RespByChrome', 0, cookies)

```


# usage

```
python3 manage.py LBotCoreBackend
```


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
