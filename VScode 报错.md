# YES 1
如果你在VScode中遇到不停输入密码或者报错Permission denied, please try again.时，请尝试此方法。

原因：该报错是由于没有服务器端的.vscode-server未及时更新导致。
解决方法：

登录ssh，执行命令
```bash
ls -a  # 查看是否存在.vscode-server文件夹
rm -rf .vscode-server  # 存在则删除该文件夹
ls -a  # 查看是否已经删除
```

登录vscode，执行命令
点击右下角进行远程连接
选择connect to host
选择Add New SSH Host
输入用户名，ip地址和端口号

ssh \<user>@\<ip>:\<port>

ssh root@47.115.223.46
点击左下角出现的Connect
正常登录，不过会稍微慢一点，因为需要下载.vscode-server/

# QES 1
结果是本地的~/.ssh/config文件在我改git 的时候搞没了难绷🤣


参考：
https://blog.csdn.net/m0_61552056/article/details/134216102