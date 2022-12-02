## 下载

进入官网-[Download | Node.js](https://nodejs.org/en/download/)

LTS为对于大多数用户推荐的版本，一般来说没有特殊需求我们就直接下载这个即可；

![image-20220706154050887](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021524816.png)

## 安装

1. 勾选协议，点击next

![image-20220706155843251](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021524837.png)

2. 选择安装路径，点击next

![image-20220706155933298](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021524838.png)

3. 选择安装选项，我这里选择添加到环境变量，点击next

![image-20220706160026121](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021524350.png)

4. 选择是否需要组件，不需勾选，直接next

![image-20220706160107632](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021524276.png)

5. 安装，install等待一会儿即可

![image-20220706160214323](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021524871.png)

安装完成

![image-20220706160239109](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021524303.png)

## 验证是否正常安装

注意安装Node.js会包含环境变量及npm的安装，安装后，检测Node.js是否安装成功，在命令行中输入 node -v :

![image-20220706160357367](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021525952.png)

检测npm是否安装成功，在命令行中输入npm -v :

![image-20220706160457194](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021525253.png)

发现这里有一个警告，这是版本未更新导致的问题，解决方法如下：

### 解决方法

---

（未出现问题可直接跳过这一步）

**npm WARN config global `--global`, `--local` are deprecated. Use `--location=global` instead报错解决方法。**

**将npm升级到最新版本即可**

**升级方法**

1. 在windows中以**管理员身份**打开cmd，然后执行命令

```bash
npm install -g npm-windows-upgrade
```

2. 更改脚本策略
   下载Windows Power Shell
   然后以**管理员身份**运行，执行命令

```powershell
set-ExecutionPolicy RemoteSigned
```

![image-20220706155639229](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021525972.png)

输入`Y`

成功更改脚本策略

3. 在Windows Power Shell上运行命令

```powershell
npm-windows-upgrade
```

4. 选择要更新的版本

选择最新的，按回车即可。



检验npm是否安装成功，命令行输入 npm -v

![image-20220706161330802](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021525156.png)



问题解决！

到这里，nodejs和npm的安装就全部完成了。

其实此问题是由版本号导致

第二种方法应该也行，是官方提供的方法，同样是用npm-windows-upgrade更新npm，链接在下面：

[felixrieseberg/npm-windows-upgrade: Upgrade npm on Windows](https://github.com/felixrieseberg/npm-windows-upgrade)



问题解决链接参照：

[npm WARN config global `--global`, `--local` are deprecated. Use `--location=global` instead. 怎么解决-前端-CSDN问答](https://ask.csdn.net/questions/7733789)

https://github.com/npm/cli/issues/4980

https://blog.csdn.net/weixin_42288182/article/details/106896534
