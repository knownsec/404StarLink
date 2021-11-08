## Pocassist <https://github.com/jweny/pocassist>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-jweny-orange)
![GitHub stars](https://img.shields.io/github/stars/jweny/pocassist.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.0.5-red)
![Time](https://img.shields.io/badge/Join-20210702-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


pocassist是一个 Golang 编写的全新开源漏洞测试框架。

- 简单易用
  - 只需要在前端编辑，即可生成poc对批量目标进行测试
  - 单二进制文件，无依赖，也无需安装
- 性能优秀
  - 支持高并发，多重并发控制，通过使用 `ants`实例化协程池，复用 goroutine
  - 多重内存复用，尽可能小的内存占用
- 规则体系
  - 完全兼容xray，但又不仅仅是xray。除了支持定义目录级漏洞poc，还支持服务器级漏洞、参数级漏洞、url级漏洞以及对页面内容检测，如果以上还不满足你的需求，还支持加载自定义脚本。

使用之前务必先阅读使用文档！

🏠[使用文档](https://pocassist.jweny.top/)	⬇️[下载最新版本](https://github.com/jweny/pocassist/releases)

## 快速开始

### 像数 1, 2, 3 一样容易

```bash
# 启动服务
./pocassist

# 浏览器访问 
http://127.0.0.1:1231
```

建议使用[pocassistdb](https://github.com/jweny/pocassistdb)作为漏洞库。⬇️[下载漏洞库最新版本](https://github.com/jweny/pocassistdb/releases/)，并在`config.yaml `的`sqlite`项配置路径。

有想一块维护poc的师傅也可直接向该项目提PR。

## Demo

登录页

![登录页](https://github.com/jweny/pocassist/raw/master/docs/pic/%E7%99%BB%E5%BD%95%E9%A1%B5.jpg)

规则首页

![规则首页](https://github.com/jweny/pocassist/raw/master/docs/pic/%E8%A7%84%E5%88%99%E9%A6%96%E9%A1%B5.jpg)

规则详情

![规则详情](https://github.com/jweny/pocassist/raw/master/docs/pic/%E8%A7%84%E5%88%99%E8%AF%A6%E6%83%85.jpg)

支持一键导入xray规则

![upload-yaml](https://github.com/jweny/pocassist/raw/master/docs/pic/yaml.gif)

单条规则靶机测试

![单条规则靶机测试](https://github.com/jweny/pocassist/raw/master/docs/pic/%E5%8D%95%E6%9D%A1%E8%A7%84%E5%88%99%E9%9D%B6%E6%9C%BA%E6%B5%8B%E8%AF%95.png)

漏洞描述首页

![漏洞描述首页](https://github.com/jweny/pocassist/raw/master/docs/pic/%E6%BC%8F%E6%B4%9E%E6%8F%8F%E8%BF%B0%E9%A6%96%E9%A1%B5.jpg)

漏洞描述详情

![漏洞描述详情](https://github.com/jweny/pocassist/raw/master/docs/pic/%E6%BC%8F%E6%B4%9E%E6%8F%8F%E8%BF%B0%E8%AF%A6%E6%83%85.png)

新建批量扫描任务

![新建扫描任务](https://github.com/jweny/pocassist/raw/master/docs/pic/%E6%96%B0%E5%BB%BA%E6%89%AB%E6%8F%8F%E4%BB%BB%E5%8A%A1.png)

任务状态

![任务首页](https://github.com/jweny/pocassist/raw/master/docs/pic/%E4%BB%BB%E5%8A%A1%E9%A6%96%E9%A1%B5.png)

扫描结果

![扫描结果](https://github.com/jweny/pocassist/raw/master/docs/pic/%E6%89%AB%E6%8F%8F%E7%BB%93%E6%9E%9C.jpg)

结果首页

![结果首页](https://github.com/jweny/pocassist/raw/master/docs/pic/%E7%BB%93%E6%9E%9C%E9%A6%96%E9%A1%B5.jpg)

组件首页

![组件首页](https://github.com/jweny/pocassist/raw/master/docs/pic/%E7%BB%84%E4%BB%B6%E9%A6%96%E9%A1%B5.jpg)

## 常见问题

1. 自定义配置。pocassist首次运行时将在当前目录生成`config.yaml`，引擎启动后实时监控配置文件变化，配置文件修改后无需重启，即热加载
2. 用户名密码错误：检查数据库配置，以及数据库auth表。建议使用[pocassistdb](https://github.com/jweny/pocassistdb)作为漏洞库
5. 支持前后端分离部署。前端源码、nginx配置示例可参考[pocassistweb](https://github.com/jweny/pocassistweb)
4. 其他使用问题请先阅读[使用文档](https://pocassist.jweny.top/)

## 免责声明

未经授权，使用pocassist攻击目标是非法的。pocassist仅用于安全测试目的。为避免被恶意使用，本项目所有收录的poc均为漏洞的理论判断，不存在漏洞利用过程，不会对目标发起真实攻击和漏洞利用。

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
