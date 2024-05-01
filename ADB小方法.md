[【经验分享】如何获取任意小程序appId及页面路径](https://open.alipay.com/portal/forum/post/17101017)
[# ADB调试TP常用命令](https://blog.csdn.net/Clayton12321/article/details/87894749)
[# ADB调试TP常用命令2](https://www.cnblogs.com/lsgxeva/p/12669016.html)
[ADB简单指令教程](https://www.cnblogs.com/programandriod/p/13868887.html)

[常用url scheme收集](https://gist.github.com/zhuziyi1989/3f96a73c45a87778b560e44cb551ebd2?permalink_comment_id=3780939)
[支付宝官方url scheme讲解](https://opensupport.alipay.com/support/FAQ/c40822ae-a276-4f43-9c42-d2826339072f)
## URL 格式

```
alipays://platformapi/startapp?appId=[appId]&page=[page]&query=[query]
```

|   |   |   |
|---|---|---|
|参数|描述|示例|
|appId|要跳转的目标小程序 APPID。|20170713077xxxxx|
|page|要跳转到目标小程序的具体 page 页面，该值等于 app.json 里面的配置值；如果不带 page 字段，默认跳转到小程序首页。  <br>路径中可以在 ？后面附加跳转后的页面参数。页面参数必须进行 UrlEncode 编码，否则只能获取到第一个页面参数。|UrlEncode 编码前：pages/index/index?key1=1&key2=2  <br>UrlEncode 编码后：pages/index/index?key1%3D1%26key2%3D2|
|query|表示从外部 App 携带的参数透传到目标小程序，如果不需要携带参数给小程序，可以不带该参数。  <br>query：启动参数，内容按照格式为参数名=参数值&参数名=参数值  <br>注意： query 携带的启动参数必须进行 UrlEncode 编码否则只能获取到第一个参数。|UrlEncode 编码前：key1=value1&key2=value2  <br>UrlEncode 编码后：key1%3Dvalue1%26key2%3Dvalue2|

## scheme转换成https链接唤起小程序

需要把 scheme 当作参数进行 UrlEncode 编码后，拼接在 `https://ds.alipay.com/?scheme=` 后。
### 拼接过程

第一步、填写贵司正确的应用appId和page页面路径，完成如下：

```
alipays://platformapi/startapp?appId=202100216xxxxxxx&page=pages/index/index
```

  
携带启动参数场景，先单独对 query 携带的启动参数进行 UrlEncode 编码，完成如下：  
UrlEncode 编码前：

```
alipays://platformapi/startapp?appId=202100216xxxxxxx&page=pages/index/index&query=key1=value1&key2=value2
```

  
UrlEncode 编码后：

```
alipays://platformapi/startapp?appId=202100216xxxxxxx&page=pages/index/index&query=key1%3Dvalue1%26key2%3Dvalue2
```

  
第二步、对 第一步 拼接完成的链接进行整体 UrlEncode 编码并拼接在 https://ds.alipay.com/?scheme=后（携带启动参数场景），完成完整拼接如下：

```
https://ds.alipay.com/?scheme=alipays%3A%2F%2Fplatformapi%2Fstartapp%3FappId%3D202100216xxxxxxx%26page%3Dpages%2Findex%2Findex%26query%3Dkey1%253Dvalue1%2526key2%253Dvalue2
```

  
以下是 JS 方式进行拼接示例：

使用 encodeURIComponent 函数先对query携带的启动参数进行 UrlEncode 编码，再使用 encodeURIComponent 对整体 scheme 链接进行 UrlEncode 编码。

```
<script> 
  window.location.href=`https://ds.alipay.com/?scheme=`encodeURIComponent(`alipays://platformapi/startapp?appId=202100216xxxxxxx&page=pages/index/index&query=${encodeURIComponent('key1=value1&key2=value2')}`) 
  </script>
```

接下来看一下，scheme 调用小程序之后，应用和页面的处理逻辑。在叙述之前，先了解下前后台的定义。

主要为了应付垃圾小程序，每次要等巨久

