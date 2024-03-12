##### 开始
需求：
- 服务器一台（本地or云）
- 公网IP
- 域名（可选）
- ssl证书（可选）

方案： flask+gunicorn+nginx。
- 服务通过gunicorn 发出，
- nginx代理到公网的80端口，
- flask做的项目。

鄙人的目的呢是很单纯的，只是想搞个企业微信来推消息，不用天天删除邮件，目前用邮件发消息简单归简单，但每天都要去删邮件，着实有些麻烦了。
于是趁着白嫖服务器的时间，顺带着去弄了下网站的搭建，真的好TM麻烦啊，到处报错，不对，，，QWQ
像我这种对Linux半生不熟，其实可以说一窍不通，指令都基本不会，在这7-8个小时里就不停的重复查。。
好在是终于给网站穿出来了，就这IP还是能用的。
server酱有一个项目叫wecom酱，是他自己的开源计划，
我一开始都没找到。。。好久才发现原来这是他自己写的。。。
下面就开始吧
##### frp
开始我只知道frp是用来内网穿透的，说实话，我以为内网穿透可以直接拿来弄公网IP，就是开放到浏览器上，但我没弄明白，而且！没弄明白第二天直接放弃了
主要是我以为用户必须安装frpc于是放弃了
frp安装:
```bash
wget https://github.com/fatedier/frp/releases/download/v0.52.3/frp_0.52.3_linux_amd64.tar.gz
tar -xvf frp_0.38.0_linux_amd64.tar.gz
# 删除客户端配置 (可选)
rm -f frpc*
```
服务端配置
```bash
vim frps.ini	# linux上编辑服务端的配置文件
#默认端口7000，就是客户端和服务端通信的端口，不是你转发的那个端口，如果要改端口，客户端和服务端两边的配置文件都要改
bind_port = 7000 

# 控制台配置，frp的web管理控制台的用户名和密码，7500是默认端口(所以前面把7500端口提前放开了)，可以通过服务端ip+7500端口登录
dashboard_port = 7500 
dashboard_user = admin 
dashboard_pwd = admin

#token = 123456789 #用于验证，为了安全，和客户端对应，服务端配置了token客户端也要配置一样的，这个配置根据需要配置，这里就不配了。
server_addr = 云服务器公网IP #编辑客户端配置文件  只需要配置公网的IP就可以，别的不要改动
```
启动frp服务端
```bash
./frps -c ./frps.ini &	#后台启动
nohup ./frps -c ./frps.ini &  #后台启动

```
在客户设备上启动客户端后可用
```bash
frpc.exe -c frpc.ini  # windown上启动客户端
```
我其实只弄了安装然后就没继续了，毕竟感觉是指定连接，没希望就没做下去了

##### gunicorn
说实话弄这个的时候我已经脑子发热去买域名了。。
这一天我还买了好多东西，呜呜呜。
这直接用pip就行
```bash
pip3 insatll gunicorn
```
以下指令在项目的入口文件的文件夹处使用
```bash
gunicorn -b 127.0.0.1:7000 init:app
```
init为我项目的入口文件，app为入口实例。
没有指定进程数和线程数，之前尝试指定了以后，项目跑起来做表单验证的时候，会报csrf的错误，所以反而默认还能正常运行，这是坑一。（是不是坑我也不知道，就先放着不删了）

说实话最后就这么简单的两步，我TM查报错查了快6个小时，真TM离谱，全都错在我写脚本的草率上，
我项目的最后一句是
```python
app.run('0.0.0.0',port=5000)
```
事实上只要用
```python
if __name__ == '__main__':
	app.run('0.0.0.0',port=5000)
```
就可以完成，可惜，写烂脚本的我永远的失去了那六个小时。
但就是那一句让gunicorn疯狂爆错，如下
```bash
Traceback (most recent call last):
  File "/usr/local/lib/python3.6/site-packages/gunicorn/arbiter.py", line 609, in spawn_worker
    worker.init_process()
  File "/usr/local/lib/python3.6/site-packages/gunicorn/workers/base.py", line 134, in init_process
    self.load_wsgi()
  File "/usr/local/lib/python3.6/site-packages/gunicorn/workers/base.py", line 146, in load_wsgi
    self.wsgi = self.app.wsgi()
  File "/usr/local/lib/python3.6/site-packages/gunicorn/app/base.py", line 67, in wsgi
    self.callable = self.load()
  File "/usr/local/lib/python3.6/site-packages/gunicorn/app/wsgiapp.py", line 58, in load
    return self.load_wsgiapp()
  File "/usr/local/lib/python3.6/site-packages/gunicorn/app/wsgiapp.py", line 48, in load_wsgiapp
    return util.import_app(self.app_uri)
  File "/usr/local/lib/python3.6/site-packages/gunicorn/util.py", line 371, in import_app
    mod = importlib.import_module(module)
  File "/usr/lib64/python3.6/importlib/__init__.py", line 126, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 994, in _gcd_import
  File "<frozen importlib._bootstrap>", line 971, in _find_and_load
  File "<frozen importlib._bootstrap>", line 955, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 665, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 678, in exec_module
  File "<frozen importlib._bootstrap>", line 219, in _call_with_frames_removed
  File "/root/share/init.py", line 78, in <module>
    app.run('0.0.0.0',port=5001)
  File "/usr/local/lib64/python3.6/site-packages/flask/app.py", line 920, in run
    run_simple(t.cast(str, host), port, self, **options)
  File "/usr/local/lib/python3.6/site-packages/werkzeug/serving.py", line 1017, in run_simple
    inner()
  File "/usr/local/lib/python3.6/site-packages/werkzeug/serving.py", line 966, in inner
    fd=fd,
  File "/usr/local/lib/python3.6/site-packages/werkzeug/serving.py", line 790, in make_server
    host, port, app, request_handler, passthrough_errors, ssl_context, fd=fd
  File "/usr/local/lib/python3.6/site-packages/werkzeug/serving.py", line 693, in __init__
    super().__init__(server_address, handler)  # type: ignore
  File "/usr/lib64/python3.6/socketserver.py", line 456, in __init__
    self.server_bind()
  File "/usr/lib64/python3.6/http/server.py", line 136, in server_bind
    socketserver.TCPServer.server_bind(self)
  File "/usr/lib64/python3.6/socketserver.py", line 470, in server_bind
    self.socket.bind(self.server_address)
OSError: [Errno 98] Address already in use
```
其实哪里出问题都在上面了，但我就是不知道，欸嘿，呜呜呜
6个小时啊╥﹏╥...
而且这报错老长一段，一时不知道从何处找起，呜呜呜。
这之后就轻松了
##### nginx
用yum即可，可怜的我还自己用wget了一遍，make了一遍，然后发现自己不知道怎么用uninstall被迫用rm -rf nginx删库
```bash
yum install nginx
```
然后无脑y就行（正常来说，不过最好看看）
之后是配置问题，
```bash
vi /etc/nginx/nginx.conf
# 进行如下配置
server {
    # 监听80端口
    listen 80;
    # 本机
    server_name localhost; 
    # 默认请求的url
    location / {
        #请求转发到gunicorn服务器
        proxy_pass http://127.0.0.1:5000;  # 这里的ip+端口就是我们启动flak的ip和端口
        #设置请求头，并将头信息传递给服务器端 
        proxy_set_header Host $host; 
    }
}
```
然后用
```bash
systemctl start nginx
```
就大功告成，
可以直接在浏览器中访问你的服务器发出来的网站信息真的是艰难困苦啊
/(ㄒoㄒ)/~~
基本流程就是这样的啦

nginx 教程
https://blog.csdn.net/2301_77444674/article/details/131438516


参考：
https://www.cnblogs.com/songzhixue/p/11353943.html
https://zhuanlan.zhihu.com/p/577187092
https://pdf-lib.org/Home/Details/5262
https://www.xjx100.cn/news/648722.html?action=onClick