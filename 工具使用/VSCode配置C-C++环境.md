> 转载自：[【教程】VScode中配置C语言/C++运行环境_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Cu411y7vT/?spm_id_from=333.880.my_history.page.click&vd_source=1abbb8d283902a924ee10e192a4f108b)

### 下载编辑器VScode

- 官网：https://code.visualstudio.com/

  ![下载指引](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021529307.png)

   

- 安装VScode（建议附加任务全部勾选）

  <img src="https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021529086.gif" alt="vscode安装" style="zoom:67%;" />

 

 

### 下载编译器MinGW并解压

- 官网页面：https://www.mingw-w64.org/

- 下载页面：https://sourceforge.net/projects/mingw-w64/files/ -内置了iconv工具

- 非官方下载页面：[MinGW Distro - nuwen.net](https://nuwen.net/mingw.html) -此版本未内置iconv工具

  > 你可以进入官网自行寻找
  >
  > 你也可以直接点击为你找好的下载页面

- 下载页面中选择 `x86_64-win32-seh` 下载

  <img src="https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021529461.png" alt="mingw下载" style="zoom:50%;" />

  > 如果你因为网络环境限制无法下载
  >
  > 不限速下载，请笑纳^-^：https://wwn.lanzouh.com/iLOip031ku6b 密码:1234

- 在C盘中解压文件

  <img src="https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021530923.gif" alt="img" style="zoom:67%;" />

  > 理论上你可以在任何地方解压，但注意路径不能包含中文，至于特殊字符请自行测试

 

 

### 将MinGW添加至环境变量

- 进入mingw64下的bin文件夹，复制当前路径，Win + i唤起系统设置，输入高级系统设置并进入，点击环境变量，选择path，编辑，新建，粘贴路径，按下三个确定

  <img src="https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021530015.gif" alt="img" style="zoom: 67%;" /> 





### 配置VScode插件

- 打开VScode安装插件 `Chinese` 和 `C/C++` ，等待安装完毕后重启VScode

  <img src="https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021530660.gif" alt="img" style="zoom: 67%;" />

   

- 切换C/C++插件至 `1.8.4` 版本（非必要，不过对于小白来说更方便，此版本运行即自动配置）

  <img src="https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021531705.png" alt="img" style="zoom: 67%;" />

  > 因最新版本不会自动生成launch.json文件，给后续优化带来不便，故退回旧版本。

 



### 运行代码

- 新建文件夹，修改为英文名称并进入，右键 `通过Code打开` 若在安装时未勾选相关选项，可能没有这个选项，请自行在VScode内操作打开文件夹

- 新建一个文件，英文命名且扩展名为 `.c` 

- 编写相关代码

  ```c
  #include <stdio.h>
  #include <stdlib.h>
  int main()
  {
      printf("Hello World!\n");
      printf("你好世界！\n");
      system("pause");    // 防止运行后自动退出，需头文件stdlib.h
      return 0;
  }
  ```

  

- VScode菜单栏，点击运行，启动调试，稍等程序运行，输出结果在下方终端，上方调试面板，点击最右边的 <strong style="color:#ffc000;">`橙色方框` </strong>停止程序运行

<img src="https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021531504.gif" alt="img" style="zoom:50%;" />

 

 

### 调整和优化

> 请根据自己的需要进行优化
>
> 代码运行后 `.vscode` 文件夹会自动生成在你的源文件目录下
>
> `.vscode` 文件夹下的 `task.json` 和 `launch.json` 用来控制程序的运行和调试

- **将程序运行在外部控制台**【墙裂推荐】

  - 打开`.vscode` 文件夹下的 `launch.json` 文件，找到 `"externalConsole": false,` 将 `false` 改为 `true` 并保存

    ![img](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021531043.png)

     

- **解决中文乱码问题**【墙裂推荐】| [VSCode中解决终端的中文乱码问题 - 我等着你 - 博客园](https://www.cnblogs.com/stu-jyj3621/p/12815080.html)

  中文乱码是由于VSC的默认编码格式是UTF-8，那么编译后程序的字符串的保存方式仍然为UTF-8，而CMD的编码方式为GBK。GBK的编码中文和符号是双字节，字符和整型是单字节。utf-8的中文和符号是三字节，字符和整型是单字节，二者的中文字符并不兼容。为解决这个问题，我们需要将二者的编码方式设为相同编码。方法多种多样，最方便、副作用最小的是下面将要介绍的方法：

  

  先了解一下gcc编译选项：

  `-finput-charset`:输入字符集设置(需要和源文件编码一致)，告诉编译器以什么样的编码形式读入源文件中的字符串。

  `-fexec-charset`:执行字符集设置(需要设置为当前运行环境支持的编码),告诉[编译器](https://so.csdn.net/so/search?q=编译器&spm=1001.2101.3001.7020)在内存中以什么样的编码形式保存字符串。

  `-fwide-exec-charset`:宽字符执行编码(在windows下应设置为utf-16LE)，告诉编译器在内存中以什么样的编码形式保存宽字符串。

  修改程序编码方式为GBK：

  - 打开`.vscode` 文件夹下的 `task.json` 文件，找到 `"${fileDirname}\\${fileBasenameNoExtension}.exe"` 在后面加上英文 `逗号` 然后回车到下一行，粘贴下面文本 `"-fexec-charset=GBK"` 并保存

    ![img](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021531599.png)

    编译时用`"-fexec-charset=GBK"`这个参数（目前的配置是有的），生成的程序的字符串就是GBK编码的，源文件编码格式不会受到影响，仍是UTF-8。
    
    
    
    **注意**：加入此参数需要依赖你下载的mingw内置iconv工具！！！
    
    iconv是一个计算机程序以及一套应用程序编程接口的名称。 作为应用程序的iconv采用命令行界面，允许将某种特定编码的文件转换为另一种编码。
    
    若缺少iconv工具使用了此参数，会出现如下**报错**：
    
    ```
    no iconv implementation, cannot convert from utf-8 to gbk
    ```
    
    

- **收纳生成的 `exe` 可执行文件**【可选】

  - 打开`.vscode` 文件夹下的 `task.json` 文件，找到 `"${fileDirname}\\${fileBasenameNoExtension}.exe"` 

  - 修改成 `"${fileDirname}\\coin\\${fileBasenameNoExtension}.exe"` 并保存，同理，`launch.json` 下也有相同的字段，需要你修改

  - 在源文件同目录下新建 `coin` 文件夹，程序运行后，可执行文件将会生成在里面（其中 `coin` 可修改成你喜欢的英文名字）

    > 这样 `.c` 文件一多起来的时候，就不会出现 `.exe` 和 `.c` 相互穿插在目录中^-^

    ![img](https://cdn.jsdelivr.net/gh/sxfinn/CDN/img/202212021531435.png)



​		以上优化C++的项目同理，不再演示。



### 提示

- 若源代码文件夹含有中文路径，将会无法编译程序。
- 若你的Windows用户名使用了中文，可能无法运行。