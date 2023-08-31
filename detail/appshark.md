## appshark <https://github.com/bytedance/appshark>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Kotlin-blue)
![Author](https://img.shields.io/badge/Author-bytedance-orange)
![GitHub stars](https://img.shields.io/github/stars/bytedance/appshark.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.1.2-red)
![Time](https://img.shields.io/badge/Join-20220914-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## Document Index
- [1.overview](doc/zh/overview.md)
- [2.startup](doc/zh/startup.md)
- [3.how to write rules](doc/zh/how_to_write_rules.md)
- [4.how to find compliance problems use appshark](doc/zh/how_to_find_compliance_problem_use_appshark.md)
- [5.a path traversal game](doc/zh/path_traversal_game.md)
- [6.argument](doc/zh/argument.md)
- [7.engine config](doc/zh/EngineConfig.md)
- [8.result](doc/zh/result.md)
- [9.faq](doc/zh/faq.md)


Appshark is a static taint analysis platform to scan vulnerabilities in an Android app.

## Prerequisites

Appshark requires a specific version of JDK
-- [JDK 11](https://www.oracle.com/java/technologies/javase/jdk11-archive-downloads.html). After testing, it does not
work on other LTS versions, JDK 8 and JDK 16, due to the dependency compatibility issue.

## Building/Compiling AppShark

We assume that you are working in the root directory of the project repo. You can build the whole project with
the [gradle](https://gradle.org/) tool.

```shell
$ ./gradlew build  -x test 
```

After executing the above command, you will see an artifact file `AppShark-0.1.1-all.jar` in the directory `build/libs`.

## Running AppShark

Like the previous step, we assume that you are still in the root folder of the project. You can run the tool with

 ```shell
 $ java -jar build/libs/AppShark-0.1.1-all.jar  config/config.json5
 ```

The `config.json5` has the following configuration contents.

```JSON
{
  "apkPath": "/Users/apks/app1.apk",
  "out": "out",
  "rules": "unZipSlip.json",
  "maxPointerAnalyzeTime": 600
} 
```

Each JSON field is explained below.

- apkPath: the path of the apk file to analyze
- out: the path of the output directory
- rules: the path(s) of the rule file(s), can be more than 1 rules
- maxPointerAnalyzeTime: the timeout duration in seconds set for the analysis started from an entry point
- debugRule: specify the rule name that enables logging for debugging

If you provide a configuration JSON file which sets the output path as `out` in the project root directory, you will
find the result file `out/results.json` after running the analysis.

## Interpreting the Results

Below is an example of the `results.json`.

```JSON
{
  "AppInfo": {
    "AppName": "test",
    "PackageName": "net.bytedance.security.app",
    "min_sdk": 17,
    "target_sdk": 28,
    "versionCode": 1000,
    "versionName": "1.0.0"
  },
  "SecurityInfo": {
    "FileRisk": {
      "unZipSlip": {
        "category": "FileRisk",
        "detail": "",
        "model": "2",
        "name": "unZipSlip",
        "possibility": "4",
        "vulners": [
          {
            "details": {
              "position": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>",
              "Sink": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>->$r31",
              "entryMethod": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void f()>",
              "Source": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>->$r3",
              "url": "/Volumes/dev/zijie/appshark-opensource/out/vuln/1-unZipSlip.html",
              "target": [
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>->$r3",
                "pf{obj{<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>:35=>java.lang.StringBuilder}(unknown)->@data}",
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>->$r11",
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>->$r31"
              ]
            },
            "hash": "ec57a2a3190677ffe78a0c8aaf58ba5aee4d2247",
            "possibility": "4"
          },
          {
            "details": {
              "position": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>",
              "Sink": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>->$r34",
              "entryMethod": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void f()>",
              "Source": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>->$r3",
              "url": "/Volumes/dev/zijie/appshark-opensource/out/vuln/2-unZipSlip.html",
              "target": [
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>->$r3",
                "pf{obj{<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>:33=>java.lang.StringBuilder}(unknown)->@data}",
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>->$r14",
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>->$r34"
              ]
            },
            "hash": "26c6d6ee704c59949cfef78350a1d9aef04c29ad",
            "possibility": "4"
          }
        ],
        "wiki": "",
        "deobfApk": "/Volumes/dev/zijie/appshark-opensource/app.apk"
      }
    }
  },
  "DeepLinkInfo": {
  },
  "HTTP_API": [
  ],
  "JsBridgeInfo": [
  ],
  "BasicInfo": {
    "ComponentsInfo": {
    },
    "JSNativeInterface": [
    ]
  },
  "UsePermissions": [
  ],
  "DefinePermissions": {
  },
  "Profile": "/Volumes/dev/zijie/appshark-opensource/out/vuln/3-profiler.json"
}

```

# License

AppShark is licensed under the [APACHE LICENSE, VERSION 2.0](http://www.apache.org/licenses/LICENSE-2.0)


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关

- 2022-11-03 发布文章[《AOSP Bug Hunting with appshark (1): Intent Redirection》](https://paper.seebug.org/2002/)

## 最近更新

#### [v0.1.2] - 2022-09-22

**更新**  
- 修复在 windows 平台运行的一些问题

#### [v0.1.1] - 2022-09-16

**更新**  
- 增加 APIMode 模式  
- 增加 camile.json 规则

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
