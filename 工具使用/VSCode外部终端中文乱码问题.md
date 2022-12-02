## VSCode中解决终端的中文乱码问题

在处理这个问题之前，你首先得知道为什么会出现这个这个问题。

你在使用VScode编辑代码时，代码页面中文正常，而终端输出那里中文却为乱码。

出现这个现象的原因是因为编码方式的不同。（VScode的默认编码方式为UTF-8，输出到终端的字符都是UTF-8的，而中国地区下cmd的编码方式GBK）

如果VScode终端那里调用的是cmd，两者编码方式的不同的就导致了中文乱码的问题。

所以我们解决乱码的方式，就是将两者的编码方式统一就行，要么将两者都统一为UTF-8，要么就统一为GBK。（个人建议统一为GBK）

<img src="https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021532483.png" alt="image-20221101153757881" style="zoom: 50%;" />



### 方法一

VSCode终端其实调用的是cmd.exe，所以当这里出现中文乱码的时候要解决的是cmd的编码设置问题。

1. 可以通过 chcp 命令查看 cmd 的编码设置，GBK2312 的代码页编号是 *936*，然后改成utf-8的编码即可；
2. utf-8 对应的代码页编号是 65001 ，所以执行 **chcp 65001** 就可以把cmd的编码设置成uft-8了；
3. 这样就解决了乱码问题，然后可以再次运行代码查看输出 ；



![img](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021532846.png)

![img](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021532256.png)



当然每次使用都输入一遍 chcp 65001 太烦了 ，可以直接在setting.json 中加上 

```json
"code-runner.executorMap":{
        "cpp":"chcp 65001 "
    },
```



### 方法二

![img](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021533735.png)

若是按F5启动调试出现乱码，则可以按

- **具体操作步骤  文件——>首选项——>设置——>搜索设置——>encoding——>Files：Encoding ——> gbk** 修改实现

VScode默认是UTF-8编码格式，我们要做的是更改VScode的默认编码格式为GBK。

下面是有关gbk和UTF-8编码方式的简单介绍：

- GBK全称《汉字内码扩展规范》（GBK即“国标”、“扩展”汉语拼音的第一个字母，英文名称：Chinese Internal Code Specification） ，中华人民共和国全国信息技术标准化技术委员会1995年12月1日制订，国家技术监督局标准化司、电子工业部科技与质量监督司1995年12月15日联合以技监标函1995 229号文件的形式，将它确定为技术规范指导性文件。这一版的GBK规范为1.0版。
- UTF-8（8-bit Unicode Transformation Format）是一种针对Unicode的可变长度字符编码，又称万国码，由Ken Thompson于1992年创建。现在已经标准化为RFC 3629。UTF-8用1到6个字节编码Unicode字符。用在网页上可以统一页面显示中文简体繁体及其它语言（如英文，日文，韩文）。

![img](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021532718.png)

 ![img](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021533208.png)



### 方法三

在node.js的调试过称中，经常需要在终端中使用console.log()输入一些变量，然而windows的cmd默认是GBK编码，在调试的过程中会出现乱码。

幸好VScode提供的对内置控制台的运行参数设定，我们可以通过 `terminal.integrated.shellArgs.windows `选项对内置控制台的运行进行参数设定。

通过打开“文件”--“首选项”--“用户设置”，然后在setting.json中设置：

```json
{
    "editor.fontSize": 18,
    "terminal.integrated.shellArgs.windows": ["/K chcp 65001 >nul"],
    "terminal.integrated.fontFamily": "Lucida Console",
}
```

![img](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021533504.png)

`/K chcp 65001 >nul `的含义是在运行cmd的时候将编码设置为 **65001；**

`>nul `是避免在控制台输出修改编码的信息，否则会输出 **`active code page: 65001`；**

同时，把字体修改为 **`Lucida Console`**。

 

转载自：https://www.cnblogs.com/stu-jyj3621



