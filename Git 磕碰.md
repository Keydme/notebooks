#git #github #ssh 
[Pro Git 原书中版](https://git-scm.com/book/zh/v2)

连接检测
```bash
ssh -T git@github.com
```
~/.ssh/config文件内容
```bash
Host github.com
User xxxxqq.com #自己邮箱
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
Port 443
```
![[Pasted image 20240121201916.png]]
git 配置查看
```bash
git config --global -l
```

出现fatal: unable to access 'https://github.com/Keydme/checkin.git/': Failed to connect to github.com port 443 after 21113 ms: Couldn't connect to server
后尝试的解决办法
```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
# 在使用clash后如此设置
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```


git 启动(连接远程仓库)
```bash
git init
git remote add origin https://github.com/Keydme/notebooks.git
git pull https://github.com/Keydme/notebooks.git main --allow-unrelated-histories
# 上一个指令中的附加指令一般需删去（--allow.....）
# 基本上就连接好一个仓库了
git commit -m "first_push"
git push -u origin master
```
```bash
1. `git init` -- create a new repo in "my-site"
2. `git remote add origin https://github.com/.....` -- make this repo a "clone" of my origin
3. `git fetch --all` -- make sure I'm aware of the most recent commits
4. `git branch -u origin/master master` -- tell my local master to track origin master
```

```
Your branch is up to date with 'origin/master'.
只在让我们不要使用master
因为github默认新建repo是main branch
本地使用master提交需要上头的审核
```
T w T 好难git

[通过 SSH 连接到 GitHub(完美指南)](https://docs.github.com/zh/enterprise-server@3.8/authentication/connecting-to-github-with-ssh)

tnnd

md qisi laozi l
[git 优秀的合并教程](https://blog.csdn.net/trustnature/article/details/124030984)
male ge bazi 