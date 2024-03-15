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


git 启动(连接远程仓库)（目前建议ssh建立）
```bash
git init
git remote add origin https://github.com/Keydme/notebooks.git
git pull https://github.com/Keydme/notebooks.git main --allow-unrelated-histories
# 上一个指令中的附加指令一般需删去（--allow.....）
# 基本上就连接好一个仓库了
git commit -m "first_push"
git push -u origin master
```
(ssh版)
只需将git remote add ...
改成ssh地址就行，然后须在github官网上上传公钥方可建立连接
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
emmm
2编主要是远程用的是main，但是没master，所以就无效了
```
T w T 好难git

[通过 SSH 连接到 GitHub(完美指南)](https://docs.github.com/zh/enterprise-server@3.8/authentication/connecting-to-github-with-ssh)

tnnd

md qisi laozi l
[git 优秀的合并教程](https://blog.csdn.net/trustnature/article/details/124030984)
[git pull & git push的详细使用](https://blog.csdn.net/matafeiyanll/article/details/129832152)
male ge bazi 
在某些场合，Git会自动在本地分支与远程分支之间，建立一种追踪关系(tracking)。比如，在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动”追踪”origin/master分支。
Git也允许手动建立追踪关系。
`$ git branch --set-upstream master origin/next`
当然这里是next分支

变基用于新建个库，并于原远程库可以形成关系？
`$ git pull --rebase`
使本地库可push？

.gitignore文件以下简单用法
```bash
# dir 不需要提交的目录
/node_modules
​
# file 不需要提交的文件
config.ini
​
# log 不需要提交的任意包含后缀名为log的文件
*.log
​
# Package Files 不需要提交的任意包含后缀名为jar的文件
*.jar
```
用git add -f可强制添加被忽略的文件
```text
在 .gitignore 文件中，每一行的忽略规则的语法如下：
1、空格不匹配任意文件，可作为分隔符，可用反斜杠转义
2、以“＃”开头的行都会被 Git 忽略。即#开头的文件标识注释，可以使用反斜杠进行转义。
3、可以使用标准的glob模式匹配。所谓的glob模式是指shell所使用的简化了的正则表达式。
4、以斜杠"/"开头表示目录；"/"结束的模式只匹配文件夹以及在该文件夹路径下的内容，但是不匹配该文件；"/"开始的模式匹配项目跟目录；如果一个模式不包含斜杠，则它匹配相对于当前 .gitignore 文件路径的内容，如果该模式不在 .gitignore 文件中，则相对于项目根目录。
5、以星号"*"通配多个字符，即匹配多个任意字符；使用两个星号"**" 表示匹配任意中间目录，比如a/**/z可以匹配 a/z, a/b/z 或 a/b/c/z等。
6、以问号"?"通配单个字符，即匹配一个任意字符；
7、以方括号"[]"包含单个字符的匹配列表，即匹配任何一个列在方括号中的字符。比如[abc]表示要么匹配一个a，要么匹配一个b，要么匹配一个c；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配。比如[0-9]表示匹配所有0到9的数字，[a-z]表示匹配任意的小写字母）。
8、以叹号"!"表示不忽略(跟踪)匹配到的文件或目录，即要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。需要特别注意的是：如果文件的父目录已经被前面的规则排除掉了，那么对这个文件用"!"规则是不起作用的。也就是说"!"开头的模式表示否定，该文件将会再次被包含，如果排除了该文件的父级目录，则使用"!"也不会再次被包含。可以使用反斜杠进行转义。
```
**需要谨记**：git对于.ignore配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；

**十分重要**：如果你不慎在创建.gitignore文件之前就push了项目，那么即使你在.gitignore文件中写入新的过滤规则，这些规则也不会起作用，Git仍然会对所有文件进行版本管理。简单来说出现这种问题的原因就是Git已经开始管理这些文件了，所以你无法再通过过滤规则过滤它们。所以大家一定要养成在项目开始就创建.gitignore文件的习惯，否则一单push，处理起来会非常麻烦。
？以上真假？？
