[Vue.js官网](https://cn.vuejs.org/)
### 1. 安装node.js 
[nodejs安装指南](https://blog.csdn.net/m0_37714470/article/details/117956075)
Node.js 是一个基于Chrome JavaScript 运行时建立的一个平台。

Node.js是一个事件驱动I/O服务端JavaScript环境，基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。（其实就是一个后台语言，用js开发，最终编译成C/C++语言，适合不熟悉后台的前台攻城狮）

对于前端开发工程师来说，nodejs或多或少都使用用过，比如用nodejs下的npm包管理工具去下载模块，很愉快的构建前端项目，也很容易的打包项目。其实nodejs原生就是为linux开发的，我们可以通过多种方式在linux上安装nodejs，比如通过源码方式、通过编译包方式等等。

这里介绍如何通过nodejs官网编译包的形式在linux服务器上安装nodejs。

  

#### 1、检查是否已安装

对于操作系统而言，不管什么软件或者系统，都是目录结构和文件，特别在linux下目录的概念更加明显，所以可以说安装软件就是复制文件和目录。

尽管大部分服务器不会默认给你安装nodejs，但是也有些镜像比较良心内置了nodejs，所以在在开始安装前我们可检查下是否安装了nodejs（当然顺便也检查下npm），我们远程登陆linux后，在输入以下命令分别检查nodejs和npm是否安装了：

  

|   |   |
|---|---|
|1<br><br>2<br><br>3|`whereis    nodejs`<br><br>`whereis   npm`|

如果系统提示没有找到相关路径，那么这表明没有安装，我们接着往下看

#### 2、下载nodejs编译包

我们在window上是直接下载exe，双击安装就可以了，而在linux上不太一样。

我们先打开nodejs下载页面：[http://nodejs.cn/download/](https://links.jianshu.com/go?to=http%3A%2F%2Fnodejs.cn%2Fdownload%2F)，选择合适的linux版本编译包

![](https://img2020.cnblogs.com/blog/2425050/202111/2425050-20211119172342263-267274879.png)

点击下载就可以了，这里提供两种方式，第一种是下载到window本机，然后通过pscp.exe上传到服务器，第二种是直接在linux服务器上使用wget下载，推荐使用第二种

如前面拿到下载地址为：[https://npm.taobao.org/mirrors/node/v10.13.0/node-v10.13.0-linux-x64.tar.xz](https://links.jianshu.com/go?to=https%3A%2F%2Fnpm.taobao.org%2Fmirrors%2Fnode%2Fv10.13.0%2Fnode-v10.13.0-linux-x64.tar.xz)

我们远程linux，输入（putty工具右键直接粘贴复制的内容）

  

|   |   |
|---|---|
|1|`wget   -c   https:``//npm.taobao.org/mirrors/node/v10.13.0/node-v10.13.0-linux-x64.tar.xz`|

　　即可下载，如

![](https://img2020.cnblogs.com/blog/2425050/202111/2425050-20211119172500559-1267032772.png)

查看一下文件

|   |   |
|---|---|
|1||

　　![](https://img2020.cnblogs.com/blog/2425050/202111/2425050-20211119172541118-23909708.png)

发现目标文件以及下载完成了，接着我们就要解压文件了

（_PS：mysql....rpm是后续安装mysql数据库用的，这里先忽略_）

#### 3、解压编译包

前面也说到，软件就是文件和目录的一个集合，所以我们下载的node-v10.13.0-linux-x64.tar.xz解压后就可以正常执行了，当然了，目录也不要随便放，不好维护。

首先我们解压文件到当前目录

  

|   |   |
|---|---|
|1|`tar    -xvf    node-v10.13.0-linux-x64.tar.xz`|

　　![](https://img2020.cnblogs.com/blog/2425050/202111/2425050-20211119172627871-711254145.png)

（PS：说一个小tip，在关于路径和文件名时，主要输入了前面几个字符后，按一下tap键，系统会自动补全，这在window的cmd和一些代码编辑器上也是通用的）

很愉快就把文件解压到了当前目录（/root/），可是我们的软件需要放到合适的地方才好，就像在window下安装软件的时候我们一般都不装在C盘一个意思，所以我们现在把这个文件夹复制或者剪切到另一个目录下。

在linux下有一个目录是专门拿来放软件的，那就是**/usr/**，注意不是/user/，如果我们去查看它的文件结构我们会注意下面又有几个比较特殊的文件夹，分别是/bin、/local、/sbin等

![](https://img2020.cnblogs.com/blog/2425050/202111/2425050-20211119172716070-727783796.png)

这几个特殊目录下都是放一下可执行文件的，如

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5|`/usr/bin    系统预设的可执行文件，如开关机在这里，优先级最高`<br><br>`/usr/local/bin   用户本身相关的可执行文件，如自己安装的软件推荐放在这里，会提升到全局`<br><br>`/usr/sbin    基本同上`|

可以把我们刚刚的文件放到/usr/local/bin下，这样就可以直接全局使用，而且不用设置软连接，不过我这里由于习惯问题，我会把文件放到/usr/sbin文件夹下，具体流程是一样的。

我们还是**回到**刚刚下载解压的文件那里，为了方便，我们先把文件重命名成nodejs

  

|   |   |
|---|---|
|1<br><br>2<br><br>3|`cd   ~`<br><br>`mv   node-v10.13.0-linux-x64   nodejs`|

　　![](https://img2020.cnblogs.com/blog/2425050/202111/2425050-20211119172831080-330595570.png)

linux下的重命名命令是（mv   源文件路径   新文件路径），和移动文件move的命令一样

当然机智的你肯定是用tap键自动补全命令的，不要一个字母一个字母这样敲

重命名后我们查看一下nodejs的bin文件夹有什么可执行文件

![](https://img2020.cnblogs.com/blog/2425050/202111/2425050-20211119172905337-1023291029.png)

可以看到有npm、node和npx三个，这三个都是可执行文件

那么重头戏来了，我们需要**把/root/nodejs文件夹移动到/usr/sbin/目录下**

|   |   |
|---|---|
|1|`mv    /root/nodejs/     /usr/sbin/`|

　　![](https://img2020.cnblogs.com/blog/2425050/202111/2425050-20211119173018706-528643473.png)

推荐使用绝对路径，而不是相对路径。执行完成后root路径下的nodejs文件夹会被移动到/usr/sbin/下。

#### 4、配置软链接

 为了使nodejs能够全局使用，我们需要配置一下软链接（类似于快捷方式，如果安装的路径在/usr/local/bin/下不需要这一步操作），当然也是软连接到用户目录下/usr/local/bin/

软链接的命令很简单： _ln    -s   源文件   目标路径_

|   |   |
|---|---|
|1<br><br>2<br><br>3|`ln -s  /usr/sbin/nodejs/bin/node    /usr/local/bin/`<br><br>`ln -s  /usr/sbin/nodejs/bin/npm    /usr/local/bin/`|

　　上面两句命令就是把node和npm可执行文件链接到/usr/local/bin/目录下，相当在全局环境中加了两个快捷方式（也可以理解成系统变量）

#### 5、检查安装结果

配置了这么久，我们看一下效果怎么样。因为前面我们配的是全局路径，所以应该在任意一个路径执行node或者npm都应该是可行的，我们可以试一下下面两句命令

|   |   |
|---|---|
|1<br><br>2<br><br>3|`node  -v`<br><br>`npm   -version`|

![](https://img2020.cnblogs.com/blog/2425050/202111/2425050-20211119173213969-7416096.png)

当然也可以利用whereis   node  查看具体路径（查询出来的是快捷方式的路径）

到这里nodejs的安装就完成了

#### 6、配置淘宝镜像

然鹅~~，对于想要配置淘宝镜像的小伙伴，使用方式可window下的一样，我们需要下载cnpm，命令如下：

> npm    install    -g    cnpm    --registry=https://registry.npm.taobao.org  

安装成功后，cnpm可执行文件会下载到nodejs的安装目录下（也就是/usr/sbin/nodejs/bin/）。接着我们把cnpm配置到全局下，也就是创建软链接到/usr/local/bin/下（如果本来就在该目录下不要做软连接）

>  ln   -s    /usr/sbin/nodejs/bin/cnpm      /usr/local/bin/  

这时候我们就可以使用cnpm来下载模块了，速度那是杠杠的

 ![](https://img2020.cnblogs.com/blog/2425050/202111/2425050-20211119173335449-1554558169.png)

原文地址：https://www.jianshu.com/p/21e42cd362e7
### Js表达式
每个绑定仅支持**单一表达式**，也就是一段能够被求值的 JavaScript 代码。一个简单的判断方法是是否可以合法地写在 `return` 后面。

可以在绑定的表达式中使用一个组件暴露的方法：
```template
<time :title="toTitleDate(date)" :datetime="date">
  {{ formatDate(date) }}
</time>
```