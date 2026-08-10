[ssh 密码登录禁用](https://www.cnblogs.com/ramlife/p/17077252.html)
```yaml
# 将/etc/ssh/sshd_config中的相关行修改如下即可
PubkeyAuthentication yes
PasswordAuthentication no
```

### ssh 相关参数
| 参数名称 | 效果 |
| --- | --- | --- |
| -i | 可使用指定密钥登录 |


### 编译安装
[Linux上如何手动编译升级/安装OpenSSH版本](https://juejin.cn/post/7062370067903676453)

**!!!若为远程电脑建议先备份再操作，防止无法连接!!!**

简单来说总计四部
 - 安装essential tools等必备编译软件
 - 手动编译依赖库openssl与zlib
 - 编译安装openssh
 - 复制or ln到bin与sbin库

```bash
wget https://www.openssl.org/source/openssl-1.1.1m.tar.gz 
tar -xf openssl-1.1.1m.tar.gz 
cd openssl-1.1.1m
# 配置 
./config --prefix=/usr/local/openssl shared 
# 编译 # 安装
make & make install
cd ..


# 下载源码 
wget http://www.zlib.net/zlib-1.2.11.tar.gz 
# 解压 
tar -xf zlib-1.2.11.tar.gz 
# 进入源码目录 
cd zlib-1.2.11
# 预编译 
./configure --prefix=/usr/local/zlib 
# 编译 # 安装 
make & make install
cd ..
# Debian/Ubuntu debian限定操作
sudo apt -y install libz-dev


# 防止版本冲突
sudo apt purge --remove "openssh*"
# 下载源码 
wget https://mirror.leaseweb.com/pub/OpenBSD/OpenSSH/portable/openssh-8.8p1.tar.gz 
# 解压源码 
tar -xf openssh-8.8p1.tar.gz 
# 进入源码目录 
cd openssh-8.8p1
# 编译配置 
./configure --prefix=/usr/local/openssh --sysconfdir=/etc/ssh --with-ssl-dir=/usr/local/openssl --with-zlib-dir=/usr/local/zlib --without-openssl-header-check 
# 编译 # 安装 
make & make install
cd ..


# openssl软链接
ln -s /usr/local/openssl/lib64/libssl.so.3 /usr/lib/ 
ln -s /usr/local/openssl/lib64/libcrypto.so.3 /usr/lib/
# 防止权限错误
echo "sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin" >> /etc/passwd
# 添加到bin&sbin中 PS：亦可以使用ln
cp /usr/local/openssh/sbin/sshd /usr/sbin/sshd 
cp /usr/local/openssh/bin/ssh /usr/bin/ssh 
cp /usr/local/openssh/bin/ssh-keygen /usr/bin/ssh-keygen
```

接下来是ssh单独的配置流程
创建修改`/usr/lib/systemd/system/sshd.service`文件
```config
[Unit]
Description=OpenSSH serve
Documentation=man:sshd(8) man:sshd_config(5)
#After=network.target sshd-keygen.service
#Wants=sshd-keygen.service
After=network.target

[Service]
#Type=notify
#EnvironmentFile=/etc/sysconfig/sshd
#ExecStart=/usr/local/openssh/sbin/sshd -D $OPTIONS
ExecStart=/usr/local/openssh/sbin/sshd
#ExecReload=/bin/kill -HUP $MAINPID
#KillMode=process
#Restart=on-failure
#RestartSec=42s

[Install]
WantedBy=multi-user.target
```

### copy 编译好的ssh
建议仅cp不删或仅创建链接
```bash
cd ./output/target/
    sudo cp etc/ssh/   /home/filesystem/rootfs/etc/ -rf  # /home/filesystem/rootfs 是你保存自己制作的文件系统的路径，如果你只需要在现有板子的系统上升级，就复制到板子上的 /etc 文件夹即可，下面操作同样
    sudo cp etc/init.d/S50sshd   /home/filesystem/rootfs/etc/init.d/  -rf
    sudo cp usr/sbin/sshd   /home/filesystem/rootfs/usr/sbin/ -rf
    sudo cp usr/bin/ssh*   /home/filesystem/rootfs/usr/bin/  -rf.　　 
    //一些文件系统可能还会缺失一些 lib 库文件，
    //这时候可以把编译出来的缺失的对应的库文件复制进去，
    //编译出来的库文件所在目录是 ./output/target/usr/lib ,      
    //亦或者把整个目录替复制过去 cp ./output/target/usr/lib /home/filesystem/rootfs/usr/lib
```

### sshd相关配置

![[../img/Pasted image 20250903220756.png]]