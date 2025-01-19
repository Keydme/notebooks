[[Termux]]

```bash
pkg install vim git openssh curl wget nmap netcat-openbsd python zsh sqlite sqlcipher vim-python
```

> kali安装小bug
> 需要新建chroot并把kali移进去



###### **备份**

[官方备份](https://wiki.termux.com/wiki/Backing_up_Termux)

> **It is highly recommended to understand what the listed commands do before copy-pasting them.**

```bash
termux-setup-storage
```

```bash
tar -zcf /sdcard/termux-backup.tar.gz -C /data/data/com.termux/files ./home ./usr
```

```bash
tar -zxf /sdcard/termux-backup.tar.gz -C /data/data/com.termux/files --recursive-unlink --preserve-permissions
```