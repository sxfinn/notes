##  CloudFlare 回源 OSS/COS

Cloudflare常应用在网站建设中，不仅省心还省钱。HTTPS 证书实在是太贵了, 一个通配符域名证书一年要至少花上一两千. 那么如何满足广大人民群众建站需求呢? Cloudflare 就是一个很好的选择. Cloudflare 是一家 CDN 提供商, 可以为网站提供反向代理. 它的做法是, 将域名解析到 Cloudflare 的服务器 (或者说代理) 上, 然后浏览器使用 Cloudflare 的证书与代理建立 SSL 连接; 接着代理会与目标服务器使用自签名的证书建立 SSL 连接, 接下来的数据都由代理转发. Cloudflare 会信任这个自签名证书, 所以整个过程都是没问题的.

![image-20220827180550205](https://pic.xinsong.xyz/img/202208271805226.png)

Cloudflare确实良心，我们也可以将其应用在图床上，就可以隐藏我们真是的源站地址。本文将以腾讯云COS为例，使用Cloudflare为COS开启CDN服务，让我们的站点更安全，阿里OSS同样适用，只有略微差别。



### 腾讯云COS配置

---

* **开通COS进入存储桶列表，创建存储桶**

![image-20220827163055013](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021517273.png)

* **众所周知，宽带联盟覆盖区域不包括中国大陆，因此你需要重新开通一个海外地区的存储桶**
* **存储桶名字随便取**
* **权限我这里选择公有读私有写。担心安全问题的朋友可以设置为私有读写，不过需要设置 Bucket 授权策略来允许 Cloudflare 的节点 IP 访问**

![image-20220827163242460](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021517976.png)

* **高级配置默认即可**

![image-20220827163344491](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021517893.png)

* **创建成功**

![image-20220827163409157](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021517430.png)

* **进入此存储桶配置管理，域名传输管理—>自定义源站域名**

* **添加自定义源站域名**

![image-20220827163647283](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021517074.png)

* **保存，复制下方CNAME值，即我们原始的源站访问域名**

![image-20220827163742638](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021518966.png)



### Cloudflare配置

---

* **注册账号，登录Cloudflare**
* **添加站点**（我们在腾讯云添加的自定义源站域名的主域名）

![image-20220827163911951](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021518609.png)

* **选择免费套餐**

![image-20220827165919652](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021518448.png)

* **这里稍等一下，CF添加站点后会自动检查有哪些解析记录，点击继续**

![image-20220827170319347](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021518684.png)



### 更换DNS服务器到Cloudflare

---

我们如果想要使用Cloudflare的CDN和解析服务需要将DNS服务器更改为CF的。



* **如下图，CF会提供给我们两个框框中的域名服务器，提示我们将DNS服务器更改为CF的**

![image-20220827170409136](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021518139.png)

* **进入你购买域名的厂商，登录您的域注册厂商的管理员帐户，打开对应域名管理，修改DNS服务器**

* 

![image-20220827170614700](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021518671.png)

* **修改DNS服务器为Cloudflare的，将CF分配给我们的域名填入下方框框保存即可**

![image-20220827170654518](https://pic.xinsong.xyz/img/202208271706562.png)



* **稍等一会儿后配置才会生效，每个域名注册商都有些许不同，但步骤都差不多**
* **更换DNS后，返回Cloudflare，点击完成**

![image-20220827172221129](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021518960.png)

* **然后会出现一些简单配置项，如图配置或者跳过即可**

![image-20220827172447453](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021518425.png)



### 添加CNAME解析记录

---

* **为刚刚的自定义源站域名添加CNAME记录指向原始的源站访问域名，并开启CF代理**（打开小云朵表示开启CDN加速）
* **保存**

![image-20220827164134992](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021519141.png)

* **Cloudflare添加域名后，会自动生成通用证书，快速开启全站HTTPS，服务端不用做任何修改，还可以选择开启多种模式**
* **进入SSL/TLS，有四种模式供我们选择，一般来说选择第二个和第三个就可以**

![image-20220827175128929](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021519572.png)

* **回到腾讯云的自定义源站域名配置**

![image-20220827171008129](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021519080.png)

**注意**：这里会有个小警告，但是不用去管，因为我们开启CF代理我们的站点后，CNAME记录的检测可能会出现些问题。



Cloudflare可以和国内CDN结合，达到国内IP走国内CDN，国外IP走Cloudflare，达到全球加速的效果。



**方案**：一个域名既作为COS源站的CDN加速域名，又作为Cloudflare代理COS源站的自定义域名。

