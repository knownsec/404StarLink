## js-cookie-monitor-debugger-hook <https://github.com/JSREI/js-cookie-monitor-debugger-hook>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-JavaScript-blue)
![Author](https://img.shields.io/badge/Author-JSREI-orange)
![GitHub stars](https://img.shields.io/github/stars/JSREI/js-cookie-monitor-debugger-hook.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.11.0-red)
![Time](https://img.shields.io/badge/Join-20230830-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->

## 监控、定位JavaScript操作cookie

## 一、脚本说明

### 为什么会有这个东西？

数据无价的时代，爬虫与反爬的对抗已经进入白热化状态，其中Cookie反爬是`最常见之一`的反爬类型， 网站方通过混淆得亲妈都不认识的JS代码设置Cookie（通常是浏览器指纹、请求时必须带上的Cookie之类的），
面对请求时必须要带上但是又不知道在哪里生成的Cookie， 你在几万行混淆的亲妈都不认识的JS屎海中苦苦挣扎希望能找到生成Cookie的地方（要是逆向思路不科学兴许还会呛上几口...），
甚至几度想找个借口骗自己放弃，或者要不干脆用Selenium之类的浏览器模拟方式算了？ 怂个球，此脚本就是来助你一臂之力的！ （你我都知道，这段只是撑场面的废话，你可以略过，如果你没有不幸读完的话...）

### 脚本功能

本脚本的功能大致分为两个部分：

- monitor： 监控所有JS操作cookie变化的动作并打印在控制台上
- debugger: 在cookie符合给定条件并且发生变化时打debugger断点

### Hook生效的条件

- 需要本脚本被成功注入到页面头部最先执行，脚本都未注入成功自然无法Hook
- 需要是JavaScript操作document.cookie赋值来操作Cookie才能够Hook到 （目前还没碰到不是这么赋值的...）

### 使用须知

本脚本是通过将自己的JS代码注入到页面，Hook住`document.cookie`来完成各种功能， 因此在使用本脚本之前要先确定要搞的Cookie确实是通过JS生成的
（后面介绍了一种非常简单的确定Cookie是JS生成还是服务器返回的方式）。

## 二、有何优势？

## 2.1 不影响浏览器自带的Cookie管理

目前很多Hook脚本Hook姿势并不对，本脚本采用的是一次性、反复Hook，对浏览器自带的Cookie管理无影响：

![./images/img.png](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/img.png)

## 2.2 功能更强：监控Cookie变化

除了cookie断点功能之外，增加了Cookie修改监控功能，能够在更宏观的角度分析页面上的Cookie：

![./images/img_1.png](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/img_1.png)

（算了，放弃打码了...）

颜色是用于区分操作类型：

- 绿色是添加Cookie
- 红色是删除Cookie
- 黄色是修改已经存在的Cookie的值

每个操作都会跟着一个code location，单击可以定位到做了此操作的JS代码的位置。

## 2.3 功能更强：打断点时细分Cookie变化类型

从v0.6开始引入了功能更强大并且配置更灵活的断点规则，引入事件机制， 将Cookie修改细分为增加、删除、更新三个事件，支持更细粒度的打断点， 关于Cookie事件，详情请参阅本文第五部分。

关于为什么要这样设计？ 一种比较常见的情况，目标网站有反爬的Cookie是JS设置的， 但是JS代码的逻辑是先疯狂的删除，然后删除好多次之后才添加真正的值， 这种方式设置Cookie正好能反制一般的Cookie Hook调试。

这里是其中一个例子，比如F5的Cookie保护，有一个Cookie `TS51c47c46075`，它就是先被删除好多次，然后再被添加一次：
![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/20f986d7.png)
这种情况下可以针对**添加**名为`TS51c47c46075`的Cookie事件打一个断点， 就可以避免那些红色的删除事件混淆视听。

## 三、 安装

### 3.1 安装油猴插件

理论上只要本脚本的JS代码能够注入到页面上即可，这里采用的是油猴插件来将JS代码注入到页面上。

油猴插件可从Chrome商店安装：

[https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)

如果无法翻墙，可以在百度搜索“Tampermonkey”字样寻找第三方网站下载，但请注意不要安装了虚假的恶意插件，推荐从官方商店安装。

其它工具亦可，只要能够将本脚本的JS代码注入到页面最头部执行即可。

### 3.2 安装本脚本

安装油猴脚本可以从官方商店，也可以拷贝代码自己在本地创建。

#### 3.2.1 从油猴商店安装本脚本

推荐此方式，从油猴商店安装的油猴脚本有后续版本更新时能够自动更新，本脚本已经在油猴商店上架：

[https://greasyfork.org/zh-CN/scripts/419781-js-cookie-monitor-debugger-hook](https://greasyfork.org/zh-CN/scripts/419781-js-cookie-monitor-debugger-hook)

#### 3.2.2 手动创建插件

如果您觉得自动更新太烦，或者有其它的顾虑，可以在这里复制本脚本的代码：

[https://github.com/CC11001100/js-cookie-monitor-debugger-hook/blob/main/js-cookie-monitor-debugger-hook.js](https://github.com/CC11001100/js-cookie-monitor-debugger-hook/blob/main/js-cookie-monitor-debugger-hook.js)

review确认没问题之后在油猴的管理面板添加即可。

## 四、监控Cookie的变化（monitor）

### 4.1 基本用法

注意，监控是为了在宏观上有一个全局的认识，并不是为了定位细节 （通常情况下正确的使用工具才能提高效率哇，当然一个人的认知是有限的，欢迎大家反馈更有意思的玩法）， 比如打开一个页面时：

![./images/img_1.png](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/img_1.png)

根据这张图，我们就能够对这个网站上哪些cookie是JS操作的，什么时间如何操作的有个大致的了解。

### 4.2 基本用法进阶

再比如借助monitor观察cookie的变化规律，比如这个页面，根据时间能够看出这个cookie每隔半分钟会被改变一次：

![./images/img_2.png](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/img_2.png)

### 4.3 过滤打印信息，只查看某个Cookie的变化

（2021-1-7 18:27:49更新v0.4添加此功能）： 如果控制台打印的信息过多， 可以借助Chrome浏览器自带的过滤来筛选，打印的日志的格式已经统一，只需要`cookieName = Cookie名字`即可， 比如：

![./images/img_9.png](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/img_9.png)

请注意，搜索时要保证你的搜索信息是URL解码了的，否则可能会不匹配， 因为控制台的打印信息都是先URL解码再打印的。

### 4.4 过滤打印信息，快速确定Cookie是否是JS本地生成的

如果你不确定要搞的Cookie是本地生成的还是某个请求服务器`set-cookie`返回的， 则可以把本脚本打开，然后刷新目标网站的页面，然后在控制台搜索Cookie名字即可，
方法与上一节类似，当Cookie的名字比较短没有标识性的时候可以加`cookieName`辅助定位，比如：

```text
cookieName = v
```

### 4.5 减少冗余信息（不推荐）

有时候目标网站可能会反复设置一个cookie，还都是同样的值，这个变量用于忽略此类事件：

![./images/img_8.png](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/img_8.png)

一般保持默认即可。

## 五、 定位Cookie的变化（debugger）

```@since v0.6 ```
此部分的文档适用于v0.6+版本，如果您本地的版本小于0.6，请升级版本后再来阅读文档。

从v0.6开始，在Cookie的值发生改变时打断点变得很复杂，也变得很简单， 复杂是因为引入了事件机制，简单是因为简化了断点规则配置更灵活。

断点规则可以分为`标准规则`和`简化规则`，标准规则是程序底层方便实现处理的， 简化规则是为了用户更方便地配置，通常情况下您只需要了解简化规则就可以了， 当简化规则配置无法满足需求时再来查阅标准规则如何配置。

#### 5.1 debuggerRules

所有的规则都是配置在`debuggerRules`数组中的，在脚本的头部有一个变量：
![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/45ecea34.png)
如果找不到的话，可以按Ctrl+F按变量的名字搜索：

```js
debuggerRules
```

这个变量是一个数组类型，里面存放着一些规则条件，来决定什么情况下会进入断点。

注意，这是一个数组，数组中的规则是或的关系，触发Cookie修改事件时， 会顺序匹配每条规则， 只要有一条规则匹配成功就会进入一次断点。

### 5.2 常用配置方式（简化的配置规则）

#### 5.2.1 Cookie名字过滤

当名为`foo`的Cookie发生变化时进入断点：

```js
const debuggerRules = ["foo"];
```

上面这种方式指定一个字符串，会按照Cookie名字等于给定的字符串去匹配。

注意，此处的完全匹配如果有被URL编码的部分也需要先URL解码再粘贴到这里， 其它涉及到字符串的地方都一样后面不再赘述。

如果Cookie的名字中包含一直变化的部分，比如时间戳、UUID之类的， 通过名字已经无法定位，则通过正则匹配：

```js
const debuggerRules = [/foo.+/];
```

绝大多数情况只需要这两种配置就够了。

下面来实践一下，当打开这个页面

[https://www.ishumei.com/trial/captcha.html](https://www.ishumei.com/trial/captcha.html)

能看到脚本检测到了一些Cookie操作：

![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/36eb394d.png)

其中有个`smidV2`很可疑，于是我们为它添加一个断点：

![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/5415caa1.png)

修改完`debuggerRules`数组要注意按Ctrl+S保存脚本，然后因为油猴是在页面加载的时候注入JS代码的， 所以要刷新页面重新注入，当刷新页面的时候就自动进入了断点：

![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/47c3b465.png)

上图的红色框A中是专门传进来的一些变量，通过将鼠标移动到这些变量上查看值， 我们能够大概知道当前断点的一些情况：

![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/0cf06995.png)

然后就是红色框B，我们打Cookie断点就是为了追踪调用栈定位生成Cookie的地方， 红色方框内是本脚本的调用栈，有很明显的`userscript.html`标识， 忽略此部分的调用栈即可。

然后追溯调用栈，能够看到设置Cookie的地方：

![](images/README_images/33dc63f1.png)

当然看这个栈对我们没用，我们要做的就是逐步往前定位， 直到定位到真正生成Cookie的地方，但是呢，本脚本只能帮你打个断点， 后面星辰大海的征程就要靠你自己啦！

#### 5.2.2 Cookie名字和事件结合

在名为`foo`的Cookie被`添加`时进入断点：

```js
const debuggerRules = [{"add": "foo"}];
```

在名为`foo`的Cookie被`删除`时进入断点：

```js
const debuggerRules = [{"delete": "foo"}];
```

在名为`foo`的Cookie已经存在但是值被`更新`时进入断点：

```js
const debuggerRules = [{"update": "foo"}];
```

条件可以同时指定多个，在`添加和更新`时进入断点，相当于是把删除排除在外：

```js
const debuggerRules = [{"add|update": "foo"}];
```

涉及到Cookie名字匹配的地方都可以使用字符串或者正则：

```js
const debuggerRules = [{"add": /foo_\d+/}];
```

### 5.3 标准的配置规则

上面的简化规则会被转化为标准规则，您也可以直接在`debuggerRules`数组中配置标准规则， 一条标准的规则的格式：

```text
{
    "events": "{add|delete|update}",
    "name": {"cookie-name" | /cookie-name-regex/},
    "value": {"cookie-value" | /cookie-value-regex/}
}
```

#### events:

字符串类型，表示此条规则匹配的事件类型，可以是单个事件，比如`add`， 也可以是多个事件，多个事件之间使用`|`来分隔，比如`add|update`， 如果觉得挤的话还可以在`|`两侧加空格，比如`add | update`
当配置了事件类型时只会匹配给定的事件类型，当不配置此选项时，默认匹配所有事件类型。

#### name:

可以是字符串，也可以是正则，当Cookie的名字匹配给定的字符串或者正则时为true， 此条不可忽略必须配置。

#### value:

可以是字符串，也可以是正则，当Cookie的值匹配给定的字符串或者正则时此规则为true， 可以不配置，不配置则会忽略此选项。

### 5.4 事件类型详解

前面介绍断点规则的配置，多次提到了事件类型， 我们只知道每个事件对应的名字的字符串是啥了， 但是还不知道每种事件意味着底层发生了啥， 本部分就是解释每种事件的实现机制。

Cookie发生了变化细分为增加Cookie、删除Cookie、更新已有的Cookie的值，其中每个事件对应着一个事件名字：

- 增加Cookie（add）
- 删除Cookie（delete）
- 更新Cookie（update）

#### 增加Cookie事件

Cookie之前在本地不存在，这是第一次添加。 有可能是第一次访问这个网站 ，也有可能是清除了Cookie重新访问，或者是每次访问网站都会生成新的Cookie，
甚至可能是网站自己的代码把Cookie删了重新添加，这都会触发增加Cookie事件。

比如执行下面的代码，这里为了保证Cookie之前不存在，在cookie的名字中加了时间戳：

```js
document.cookie = "foo_" + new Date().getTime() + "=bar; expires=Fri, 31 Dec 9999 23:59:59 GMT; path=/";
```

当我们在控制台运行这行代码的时候，就会触发Cookie添加事件：

![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/10ea2db6.png)

#### 更新Cookie事件

当一个Cookie在本地已经存在，然后又尝试为它设置值，就会触发更新Cookie事件。

比如下面的代码：

```js
document.cookie = "foo_10086=blabla; expires=Fri, 31 Dec 9999 23:59:59 GMT; path=/";
document.cookie = "foo_10086=wuawua; expires=Fri, 31 Dec 9999 23:59:59 GMT; path=/";
```

第一条设置Cookie的语句会触发Cookie新增事件， 第二条设置Cookie的语句因为要设置的Cookie已经存在了， 所以触发了Cookie更新事件。

![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/fa06f80c.png)

#### 删除Cookie事件

如果前端开发者在设置Cookie的时候，给了一个早于当前时间的expires， 则意味着要删除这个Cookie，比如一种常见的删除Cookie的方式：

```js
const expires = new Date(new Date().getTime() - 1000 * 30).toGMTString();
document.cookie = "foo=; expires=" + expires + "; path=/"
```

当我们在控制台运行这段代码时，就会触发Cookie删除事件：

![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/35720fae.png)

由上面也可以看出来，触发Cookie删除事件纯粹是检测expires， 并不会真的去检查这个Cookie之前是否存在。

### 5.5 控制事件类型断点是否开启的标志位

前面介绍了在配置Cookie断点规则的时候有个事件类型， 事实上每个事件类型都对应着一个此事件类型的断点是否开启的标志位， 这个标志位的优先级是最高的，比如没有开启删除Cookie断点的情况下，触发了Cookie删除事件，
会先检查Cookie删除断点是否开启标志位，如果是关闭的， 则直接忽略本次事件不再尝试匹配断点规则 （开发者工具控制台上是仍然会打印本次删除事件的日志的）。

所以现在的情况就变得非常复杂了，让我们再捋一下这一个小小的Cookie断点要走的流程：

1. 触发Cookie增加、删除、修改事件，然后检查对应的事件类型断点是否开启
2. 如果没有开启，则忽略，如果已经开启，则顺序检查是否匹配给定的规则
3. 每匹配成功一条规则，则进入断点一次.

默认情况下只开启了Cookie增加事件和Cookie修改事件的断点：

![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/2a5b0f6c.png)

因为一般情况下，增加Cookie和更新Cookie可以混为一谈，它们都是为Cookie赋了一个值， 而大部分情况下我们不会关注Cookie被删除的事件，所以这里就这么设置了，如果无法满足你的需求，
可以自行修改`enableEventDebugger`对应的值。

## 六、 问题反馈

在使用的过程过程中遇到任何问题，可以在GitHub的`Issues`中反馈， 也可以在油猴脚本的评论区反馈，还可以给我发邮件，我看到之后会尽快处理。

## 七、FAQ

### 7.1 如何调整控制台打印的字体大小？

从v0.6版本开始增加了一个变量用于调整本脚本在控制台打印的日志的字体大小，单位为px：

![](https://github.com/JSREI/js-cookie-monitor-debugger-hook/raw/main/images/README_images/8b47aea4.png)

随着版本迭代，可能不在这个位置了，如果一下找不到，就在代码搜索：

```js
consoleLogFontSize
```

然后修改这个变量的值即可。

或者另一种方案，可以在开发者工具控制台按住Ctrl+鼠标滚轮缩放调整整体大小， 这是Chrome浏览器自带的功能。

### 7.2 为什么Cookie明明是JS设置的，但是没有Hook到？你个大骗子！  :（

在本文的最开始就交代了，本脚本要能够成功的注入到页面的开头部分并且执行才能够Hook成功， 对于类似于加速乐第一层那种整个页面只返回一个script，里面是这种逻辑：

```html

<script>
    document.cookie = 这里是一些奇奇怪怪的JS用于计算出Cookie;
    location.href = "跳转走了";
</script>
```

设置了Cookie并且立刻就重定向到了新的页面，对于这种操作，有可能会Hook不到，这是油猴脚本的问题，如果坚持要Hook， 可以采用挂代理将本脚本注入到这个URL的响应的头部。

# 八、实战示例

此页面下是一些使用此脚本逆向的实战例子汇总：  
[点我进入导航页](https://github.com/JSREI/js-cookie-monitor-debugger-hook/blob/main/docs)

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
