## 简介

![image-20221202142349665](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021423840.png)

**WordPress**是一个以PHP和MySQL为平台的自由开源的博客软件和内容管理系统。WordPress具有插件架构和模板系统。 截至2018年4月，排名前1000万的网站中超过30.6%使用WordPress 。WordPress 是最受欢迎的网站内容管理系统全球有大约40%的网站（7亿5000个）都是使用WordPress 架设网站的。WordPress 是目前因特网上最流行的博客系统 。WordPress在最著名的网络发布阶段中脱颖而出。如今，它被使用在超过7000万个站点上。



### 特性

WordPress具有一个带模板处理器（template processor）的页面模板系统（web template system）。

**主题编辑**

WordPress用户可以安装和切换主题。主题可让用户不改变博客内容和结构的情况下更改界面和WordPress站点的功能。主题可以在WordPress的“外观”管理工具中安装，或者通过FTP上传至主题文件夹。也可以通过编辑主题中的PHP和HTML代码自定义主题。

**插件编辑**

[WordPress](https://wordpress.org/) （页面存档备份，存于互联网档案馆）的一个特性是它丰富的插件架构，插件能使用户和开发者扩展WordPress程序的功能。当前WordPress插件数据库中有超过18000个插件，包括[SEO](https://zh.m.wikipedia.org/wiki/SEO)、[控件](https://zh.m.wikipedia.org/wiki/控件)等等。

**多作者共同写作和多博客共存编辑**

在WordPress 3.0之前，尽管多个在不同目录中的WordPress程序能被配置成使用不同的数据库，但此时程序仅支持一次部署建立一个博客。WordPress Multi-User（WordPress MU，或简称WPMU）从WordPress中分支，支持一次部署并建立多个博客，还能够被管理员统一管理。WordPress MU成功地使一个网站能够建立自己的博客社群，同时在一个控制面板中控制修改所有的博客。WordPress MU为每个博客建立了八个新数据表。

---



## 准备

- [x] **云服务器一台**
- [x] **域名一个**（如果是国内服务器需要备案）

### 本教程使用的环境

* **CentOS 7.9.2009 x86_64(Py3.7.9)**
* **宝塔面板腾讯云专享版 7.9.3（预装）**



**进入面板，安装LNMP，即Nginx、MySQL和PHP，这些环境是运行Typecho程序必不可少的。推荐使用PHP7以上版本，其他保持默认即可。**

看大家网站需要什么环境进行选择。如果是生产环境推荐大家使用编译安装，如果只是测试环境选择极速安装。两者的区别是编译安装慢但稳定，极速安装虽然快但是没编译安装稳定。耐心等待，可以在左上角查看进度。

![image-20221202142359200](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021423263.png)

* **nginx-1.20**
* **pureftpd-1.0.49**
* **mysql-5.7**
* **php-8.0**
* **phpmyadmin-5.1**

---



## 开始搭建

* **添加站点**

![image-20221202142407841](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021424966.png)

* **填写域名，多个域名分行填写，没有域名可以用ip地址**
* **FTP文件上传服务可不选，个人认为面板上传文件就很方便**
* **创建数据库**

![image-20221202142421606](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021424717.png)

* **保存好数据库密码以及用户名，后面会用到**

![image-20221202142429476](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021424530.png)



### 上传WordPress文件

* **进入WordPress官网下载** [Download | WordPress.org](https://wordpress.org/download/)

![image-20221202142439831](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021424901.png)

* **打开宝塔面板，进入网站根目录**

![image-20221202142456026](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021424100.png)

* **全选文件删除**（user.ini为放跨站配置可以不删)

![image-20221202142510289](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021425461.png)

* **上传WordPress.zip文件压缩包**

![image-20221202142524079](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021425275.png)

* **解压缩WordPress.zip到网站根目录**

![image-20221202142533922](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021425016.png)

* **删除WordPress.zip压缩包**（可选）

![image-20221202142546774](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021425881.png)

* **进入解压出的WordPress文件夹**
* **全选文件剪贴**

![image-20221202142555615](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021425857.png)

* **返回网站根目录，粘贴**

![image-20221202142603388](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021426490.png)

* **保证wordpress的程序在网站根目录中，如下**

![image-20221202142615296](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021426503.png)



### 解析域名

* **进入域名控制台，添加解析记录**
* **将你的域名解析到服务器的ip地址**

添加两条解析记录如下：

![image-20221202142626834](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021426900.png)



### 安装WordPress

* **浏览器地址栏输入你的域名**
* **进入安装程序，选择语言**

![image-20221202142635255](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021426413.png)

* **点击现在就开始**

![image-20221202142642478](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021426591.png)

* **输入数据库名和密码**（刚刚保存的）
* **提交**

![image-20221202142653079](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021426187.png)

* **运行安装程序**

![image-20221202142700673](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021427775.png)

* **设置站点标题、用户名、密码、邮箱**（用于每次登录网站后台）
* **安装WordPress**

![image-20221202142708780](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021427929.png)

* **登录网站**（使用设置的用户名和密码）

![image-20221202142719117](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021427204.png)

* **输入设置的用户名和密码，显示如下页面则安装成功**

![image-20221202142735954](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021427229.png)



### 设置伪静态

这一步尤其重要，正确设置伪静态和固定链接可以保证网站被正常访问，顺序一定不要搞错了，先在宝塔设置伪静态规则，再设置WordPress固定链接，否则可能导致除首页之外的任何页面都访问不了。

#### 设置伪静态规则

* **进入宝塔面板进行站点设置**

![image-20221202142748604](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021427732.png)

* **选择wordpress伪静态，保存**

![image-20221202142805766](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021428874.png)

#### 设置固定链接

* **登录网站后台** 设置→固定链接

![image-20221202142813022](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021428261.png)

* **使用自定义结构，用文章id作为地址**
* **删除链接中的/index.php**

![image-20221202142824656](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021428767.png)

* **按照自己想要的连接格式选中即可，保存更改**

![image-20221202142834862](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021428118.png)

---



### 主题 & 插件

WordPress 博客本身带主题/插件商店，因此可以直接在网站后台进行安装并启用，当然也有许多优秀的主题和插件无法在后台中直接安装，那么这些主题和插件需要自己到论坛、网上去找，下载后在网站后台上传，再到网站后台启用即可。

---



## 安装过程可能会遇到的问题

1. **开启放跨站攻击无法访问站点**（宝塔默认开启）

​		解决方法一：[宝塔默认启用"防止跨站"攻击后，网站打不开，善用open_basedir参数](http://sebcxy.com/article/95)

​		解决方法二：关闭放跨站攻击（不推荐）

2. **开启伪固定连接后文章页面无法访问**

​		解决方法：开启伪静态

---

参考文章：

[宝塔面板安装WordPress（超详细） - 知乎](https://zhuanlan.zhihu.com/p/145116769)

[使用宝塔面板搭建WordPress网站](http://cloud.yundashi168.com/archives/1039#i-8)

[宝塔面板搭建WordPress网站完整教程 - 简书](https://www.jianshu.com/p/293c94adc11d)
