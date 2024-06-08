[Xpath解析](https://blog.csdn.net/weixin_73320743/article/details/133136583)
![[../img/Pasted image 20240608184626.png]]

基本定位语法

|表达式|说明|举例|
|--|--|--|
|/ |从根节点开始选取|/html/div/span|
|// |从任意节点开始选取|//input|
|. |选取当前节点||
|.. |选取当前节点的父节点|//input/.. 会选取 input 的父节点|
|@ |选取属性或者根据属性选取|//input[@data] 选取具备 data 属性的 input 元素 //@data 选取所有 data 属性|
|* |通配符，表示任意节点或任意属性||

e.g.
//父元素名[@属性名1='属性值1']/子元素名[@属性名2='属性值2']
可使用 and or not 进行运算选择
//tagname[contains(text(),'value')]：匹配包含指定值的文本内容的元素。

|函数|说明|举例|
|--|--|--|
|contains|选取属性或者文本包含某些字符|//div[contains(@id, 'data')] 选取 id 属性包含 data 的 div 元素|
|starts-with|	选取属性或者文本以某些字符开头|	//div[starts-with(@id, 'data')] 选取 id 属性以 data 开头的 div 元素|
| ends-with | 选取属性或者文本以某些字符结尾 | //div[ends-with(@id, 'require')] 选取 id 属性以 require 结尾的 div 元素|
