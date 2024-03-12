#科学上网 #Linux #clash 
# clash
（选自）
[这里](https://glados.rocks/console/terminal)
## glados教程
第一步: 开一个新的 Terminal 运行Clash, 启动代理

```bash
curl https://glados.rocks/tools/clash-linux.zip -o clash.zip #下载Clash  
unzip clash.zip  user@localhost:~$ cd clash  curl https://update.glados-config.com/clash/undefined/xxxx/8888/glados-terminal.yaml > glados.yaml #下载您的终端配置文件
chmod +x ./clash-linux-amd64-v1.10.0  
./clash-linux-amd64-v1.10.0 -f glados.yaml -d .
```

clash 打印如下日志说明clash启动成功

INFO[0000] HTTP proxy listening  at: [::]:7890  
INFO[0000] SOCKS proxy listening at: [::]:7891  
INFO[0000] RESTful API listening at: 127.0.0.1:9090  （图形控制界面）

日志提示已经开放了HTTP代理服务端口为7890, SOCK55服务端口为7891.

后面设置其他程序(浏览器/GIT等)通过7890/7891来代理访问网络就可以了。

第二步: 使用代理

1. 例如 Git:

新开一个Terminal:

user@localhost:~$ git clone https://github.com/twbs/bootstrap.git --config "http.proxy=127.0.0.1:7890"    

clash 打印如下日志说明clash完成了工作

INFO[0007] [TCP] 127.0.0.1:54875 --> github.com:443 match DomainKeyword(github) using Proxy

2. 例如 NPM:

user@localhost:~$  npm config set proxy http://127.0.0.1:7890   
user@localhost:~$  npm install pm2 -g   
user@localhost:~$  npm config delete proxy  #取消代理设置  

3. 通过设置Shell的环境变量, 例如 APT/CURL:

user@localhost:~$ export http_proxy="127.0.0.1:7890"   
user@localhost:~$ apt update   
user@localhost:~$ apt install wget   
user@localhost:~$ export http_proxy="" #取消代理设置  

user@localhost:~$ export http_proxy="127.0.0.1:7890"   
user@localhost:~$ curl https://ifconfig.me   
user@localhost:~$ export http_proxy="" #取消代理设置  

4. SSH 通过代理连接服务器, 例如:

ubuntu 下编辑 ~/.ssh/config 文件:

Host 1.1.1.1  
User root  
ProxyCommand /usr/bin/nc -X5 -x 127.0.0.1:7891  %h %p  

连接服务器

ssh root@1.1.1.1

5. 桌面型Linux(如Ubuntu 22.04)请打开设置-网络-设置网络代理为SOCK5, 地址为 127.0.0.1, 端口为7891.

注意: ping 并不是 TCP 应用，因此无法使用Clash的HTTP/SOCK5代理.

第三步: 管理Clash(可选)

可以使用 [Web UI 管理 Clash](http://127.0.0.1:9090/ui), Port 填写9090

项目地址: [https://github.com/Dreamacro/clash](https://github.com/Dreamacro/clash)

~~更多平台下载地址: [https://github.com/Dreamacro/clash/releases](https://github.com/Dreamacro/clash/releases)~~（已失效）


## AKIYA、
https://little-star.love/posts/f2114751/
附带一定的自动化教程
自己看吧

