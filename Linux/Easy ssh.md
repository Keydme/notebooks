[ssh 密码登录禁用](https://www.cnblogs.com/ramlife/p/17077252.html)
```yaml
# 将/etc/ssh/sshd_config中的相关行修改如下即可
PubkeyAuthentication yes
PasswordAuthentication no
```
