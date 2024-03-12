![[Pasted image 20240131213021.png]]
[tor官网](https://torproject.org/)
若是国内服务器要先打开[[Linux 科学上网]]

[Tor启动检测](https://github.com/ohyicong/Tor/tree/master)
[chrome开启tor](https://stackoverflow.com/questions/55689701/how-to-use-tor-with-chrome-browser-through-selenium)
```python
from selenium import webdriver
import os

# To use Tor's SOCKS proxy server with chrome, include the socks protocol in the scheme with the --proxy-server option
# PROXY = "socks5://127.0.0.1:9150" # IP:PORT or HOST:PORT

torexe = os.popen(r'C:\Users\Debanjan.B\Desktop\Tor Browser\Browser\TorBrowser\Tor\tor.exe')
PROXY = "socks5://localhost:9050" # IP:PORT or HOST:PORT
options = webdriver.ChromeOptions()
options.add_argument('--proxy-server=%s' % PROXY)
driver = webdriver.Chrome(chrome_options=options, executable_path=r'C:\Utility\BrowserDrivers\chromedriver.exe')
driver.get("http://check.torproject.org")
```
很奇怪的是我的服务器他打不开？？
说实话因为我是先开代理，后面selenium返回了空。（难道是没密码？？）
相当不理解没报错才是最麻烦的

libevent的安装(服务器上好像安装了一大堆乱七八糟的东西？？)
https://www.cnblogs.com/TechNomad/p/17874913.html
python配置tor（垃圾东西，连好看点的格式都没有）只能说还算能用？
https://www.wangan.com/p/7fy78y865176210f


[StepByStepTorturial](https://gist.github.com/DusanMadar/8d11026b7ce0bce6a67f7dd87b999f6b)
上面的因该是好东西但还没看过
另一个ｔｏｒpython教程
https://infosecwriteups.com/configuring-tor-with-python-1a90fc1c246f