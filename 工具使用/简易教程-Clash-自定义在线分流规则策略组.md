## 简介

Clash for Windows（CFW）应该是目前Windows和macOS上最好用的基于规则的跨平台代理工具软件，允许用户可视化操作和支持主流SS/V2ray/Trojan多协议。Clash.Net在此基础上对UI进行了美化，也推荐使用。

已经上手Clash的用户大都是在用ACL4SSR或其他大佬的维护的分流策略，他们的规则策略其实已经能满足绝大部分用户的使用场景，但是还有一小撮用户（比如我）由于工作或者个人使用习惯的差异，有些分流没有包含这些差异在内，这时统一使用Final（漏网之鱼）来回切换就比较麻烦，因此这种情况下，制作属于自己的分流规则策略组还是很有必要的。

将折腾过后得出的方法分享给大家，少走点弯路。本教程理论上适用于所有Clash内核的代理工具，如Clash X Pro，Clash for Android（CFA）以及路由器版的OpenClash。



👇🏼 **教程整体逻辑** 👇🏼

→ **`制作线上分流规则和策略组文件`**
→ **`转码托管机场订阅和分流策略组文件地址`**
→ **`将转码后的分流策略组文件地址正确放入订阅转换API链接中`**
→ **`导入最终配置文件链接到CFW`**



## 制作线上分流规则和策略组

这一步是为了创建符合你使用习惯的分流规则 **`.list`** 和策略组 **`.ini`** 文件。原则上只要有一个可以线上读写维护的库就可以，这里推荐Github库和VPS，本文仅以Github版教程抛砖引玉，VPS版就是现在本地写好再传到服务器就好了。

一般情况下，并不是所有分流规则完全都要自己写，大部分可以使用大佬维护的分流规则，然后写自己需要的分流规则，最后整理出自用分流策略组文件。



### 分流规则库推荐

> 👉🏼 注册一个[Github](https://github.com/)账号，有邮箱就能注册。（已有跳过这步）

> 获取正确Github链接地址：点开所需文件，在右上方点 **`Raw`**，然后完整拷贝浏览器 **`raw.githubusercontent`** 开头的链接地址。

**ACL4SSR的库**:https://github.com/ACL4SSR/ACL4SSR/tree/master/Clash

**blackmatrix7的库**:https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash

**神机规则库**:https://github.com/DivineEngine/Profiles/tree/master/Clash/RuleSet

- 分流规则参考使用 **`.list`** 后缀文件。
- 如果参考的分流规则是 **`.yaml`** 后缀文件，建议先只选取部分需要的规则，然后复制转移或 **`fork`** 该规则到个人Github库中，把 **`-`** 字段用全部替换的方式删掉，再重命名为 **`.list`** 后缀文件。



### 制作自用分流规则

> **命名**：文件命名随意，但是一定是英文+以 **`.list`** 结尾。

> 英文的 **`;`** 和 **`#`** 都是常用的注释符号，表示该行代码不会生效，常用于代码前的分类和备注。



👉 **常用规则写法参考**:

```
# 表示包含xxx.com域名后缀下的所有网站链接
DOMAIN-SUFFIX,xxx.com

# 表示包含这个xxxx域名关键词的所有网站链接
DOMAIN-KEYWORD,xxxx
```

👉 **以PayPal分流规则为例**：

```
# PayPal
DOMAIN-SUFFIX,paypal.com
DOMAIN-SUFFIX,paypal.me
DOMAIN-SUFFIX,paypalobjects.com
DOMAIN-KEYWORD,paypal
```

👇 **更多写法可以参考Clash文档** 👇

https://docs.cfw.lbyczf.com/contents/ui/profiles/rules.html



### 制作分流策略组

> **命名**：文件命名随意，但是一定是英文+以 **`.ini`** 结尾。

> **`.ini`** 配置文件中：
> **`ruleset`** 指的是配配置中包含的分流规则，
> **`custom_proxy_group`** 指的是最终在Clash中呈现的分流策略组及其排序。

> **`ruleset`** 排序原则：
> 重要直连分流规则 > 去广告规则 > 小分流 > 国内外大分流 > 补充规则。

策略组的排序非常重要，因为分流策略组的匹配是按照至上而下收录，匹配到了就停止不再往下，比如YouTube规则要放在国外媒体前面，而完整的国外媒体规则包含了YouTube, Netflix, Pornhub等等，所以分流规则较大要放在YouTube小分流规则后面。



👉 **分流策略组模板参考**：

**ACL4SSR的配置文件**：https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Full.ini

👉 **分流策略组文件说明**：

1. 一般情况下，只需要对 **`ruleset`** 和 **`custom_proxy_group`** 进行修改即可，其他地方不懂就不改。
2. **`ruleset`** 和 **`custom_proxy_group`** 中分流规则和策略组自定义命名要完全对应，但是可以几个**同命名而不同地址**的 **`.list`** 分流规则对应一个策略组。

> 📌 举个例子：我创建3条 **`ruleset`** 分流规则并链接到Github的地址，且全部都命名 **`全球直连`** ，那在 **`custom_proxy_group`** 中命名为 **`全球直连`** 策略组会全部应用上面三条分流规则。

👉 **Ruleset说明**：
逗号前的红框位置为该分流规则的命名，逗号后为该分流规则`.list`后缀的地址链接，如果规则同名最终会共同叠加生效。

![image-20221202150029335](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021500375.png)

👉 **Custom_proxy_group说明**：
这个分组为在CFW图形界面最终呈现的策略组排序。**`Select`** 后面有多少 **`[]XXXX`** 代表该策略组有多少种规则可以选，可以自定义，一般用 **`上飘点`** 分隔，最后一项后不需要加 **`上飘点`**。

![image-20221202150036248](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021500300.png)

```
# 以下代码是CFW默认自带的，不用特意再写，结合上图，按需设置策略组的选项
→ DIRECT: 直连 
→ REJECT: 该规则下不走网络活动，常用于广告拦截
→ .*: 表示加入你订阅中所有节点 
→ url-test: 表示有该代码下的节点会自动测速 

# 自动归类节点 - 以图片中香港节点策略组为例
→ (港|HK|Hong Kong)
代表具有"港"，"HK"，"HongKong"关键词的节点会归类到香港节点这个策略组中，
测速以 http://www.gstatic.com/generate_204`300,,50为准。
```

### 提交上传配置文件

> ⚠️**温馨提示**⚠️
>
> 在GitHub上面几步改好的 **`.list`** 和 **`.ini`** 文件，要点 **`Commit Change`** 提交，再去拷贝 **`Raw`** 文件链接。

![image-20221202150043992](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021500081.png)

---



## 转码托管 - 机场订阅和策略组

这里只要用到两种链接，一种是你的机场订阅链接，另一种则是你先前编辑好 **`.ini`** 分流策略组配置的链接。



### 转码托管机场链接

这一步是利用开源订阅转换API转码你的机场订阅链接，如果有网易云解锁节点链接也可以加入一并转换。

一般情况下，这些订阅转换API转码不会保存你的节点信息。通俗来说，只是把你的字符转换成另外一种计算机语言，并套进对应的代理工具软件配置参数的链接中，不放心且有能力的也可以自己搭建API。



🔗**订阅转换托管API推荐**：

[ACL4SSR 在线订阅转换](https://acl4ssr-sub.github.io/)

[边缘@订阅转换API](https://bianyuan.xyz/)



👉 **转换托管步骤**

1. 输入的订阅/节点链接，选择生成类型，这里我们默认选 **`Clash`**（也有叫Clash新参数的）

![image-20221202150055111](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021500270.png)

2. 点生成订阅链接，获得转码后的链接地址，下面是按照图内的地址转码后得到的结果：

```
# 温馨提示：往右拖动还有内容
# 该配置文件地址还没有嵌入策略组地址信息
# 这里以我截图乱填的一个个订阅地址为例
https://pub-api-1.bianyuan.xyz/sub?target=clash&url=https%3A%2F%2Fcate.com&insert=false

# 预留一下策略组配置文件地址位置，在上面链接的基础上合并下面这串代码
&insert=false&config=peizhiwenjian&emoji=true&list=false&udp=false&tfo=false&scv=false&fdn=false&sort=false

# 如果订阅支持udp, tfo就把这两项后面的false改成true，默认为false，加完后完整链接为：
https://pub-api-1.bianyuan.xyz/sub?target=clash&url=https%3A%2F%2Fcate.com&insert=false&config=peizhiwenjian&emoji=true&list=false&udp=false&tfo=false&scv=false&fdn=false&sort=false
```

### 转码分流策略组

先前我们已经编辑好我们自定义的 **.ini** 后缀的分流策略组配置文件，在Github上，我们要拷贝这个文件的 **`Raw`** 地址，这个地址才是文件的源地址。

![image-20221202150102998](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021501190.png)

上图页面并不是**.ini**文件的地址，实际上此文件是存储在`Raw`地址的：

![image-20221202150110699](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021501870.png)

👉 **转换策略组步骤**

1. 在https://www.urlencoder.org/ 上转码，按照下图步骤。

![image-20221202150123165](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021501299.png)

2. 把转码后链接地址粘贴在下方链接中 **`peizhiwenjian`** 处即可成功获得最终的配置文件。

```
# 温馨提示：往右拖动还有内容
# &insert 前为先前通过`api.dler.io`转换后的订阅地址
# peizhiwenjian 替换成你转码后配置文件地址，一定是.ini结尾的

https://pub-api-1.bianyuan.xyz/sub?target=clash&url=https%3A%2F%2Fcate.com&insert=false&config=peizhiwenjian&emoji=true&list=false&udp=false&tfo=false&scv=false&fdn=false&sort=false
```

---



## 导入配置文件地址到Clash

按照图示导入最终的配置文件到 **`CFW`** 或 **`Clash.Net`**，完结撒花！

- API有可能会被墙，建议在编辑自用分流规则时加入你使用的订阅转换API域名。
- 每次Github的配置文件修改后，由于缓存的原因，CFW建议过一两分钟再点更新配置文件。
- 使用托管API得到的链接，更新时会偶尔套用失效，应该是服务器问题，等待一两分钟再次更新就好了。

![image-20221202150135842](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021501953.png)

