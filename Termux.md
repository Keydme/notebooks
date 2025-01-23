[[Termux 初始化]]
如果遇到突然无法下载的问题，可以通过这个换一下源就好了
termux-change-repo

(手机上的Linux??)
[obsidian 手机git](https://zhuanlan.zhihu.com/p/619764281)

[清华源镜像官网](https://mirrors.ustc.edu.cn/help/index.html)

[Termux 高级配置](https://blog.csdn.net/qq_39312146/article/details/127913614)

[国光的高档教程](https://www.sqlsec.com/2018/05/termux.html#Termux-%E7%AE%80%E4%BB%8B)

[Termux Themes for many type](https://blog.csdn.net/m0_57236802/article/details/135183963)

[Termux ssh to link win](https://www.jianshu.com/p/5963a747e280/)

[Ohmyzsh gallery](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)

[termux api](https://zhuanlan.zhihu.com/p/322205509)
目前为止最好用的指令！！！！
可是通知常驻锁屏界面！！
待办事项有福啦！！！

### `termux-notification`

用法：`termux-notification [options]`  
显示系统通知。内容文本使用 `-c / -content` 指定或从标准输入中读取。  
阅读--help-actions以获取有关操作参数的帮助。

|可选项|功能|
|---|---|
|--action action|按下通知时执行的动作|
|--alert-once|当通知被编辑时不发出警告|
|--button1 text|通知上第一个按钮显示的文字|
|--button1-action action|通知上第一个按钮执行的动作|
|--button2 text|通知上第二个按钮显示的文字|
|--button2-action action|通知上第二个按钮执行的动作|
|--button3 text|通知上第三个按钮显示的文字|
|--button3-action action|通知上第三个按钮执行的动作|
|-c/--content content|通知中显示的内容。优先于标准输入。|
|--group group|通知分组（相同分组的通知会被一同显示）|
|-h/--help|显示此帮助信息|
|--help-actions|显示关于按钮行为的帮助|
|--icon icon-name|设置显示在状态栏的图标。到[https://material.io/resources/icons/](https://link.zhihu.com/?target=https%3A//material.io/resources/icons/) 查看可用图标（默认图标：event_note）|
|-i/--id id|通知ID（会覆盖之前任何拥有相同ID的通知）|
|--image-path path|将被显示在通知上的一张图片的绝对路径|
|--led-color rrggbb|以RRGGBB表示的通知闪烁灯颜色（默认：无）|
|--led-off milliseconds|number of milliseconds for the LED to be off while it's flashing （默认：800）|
|--led-on milliseconds|number of milliseconds for the LED to be on while it's flashing （默认：800）|
|--on-delete action|当通知被清除时执行的动作|
|--ongoing|将通知固定到任务栏|
|--priority prio|通知优先级（high/low/max/min/default）|
|--sound|随通知播放声音|
|-t/--title title|要显示的通知标题|
|--vibrate pattern|vibrate pattern, comma separated as in 500,1000,200|
|--type type|要使用的通知风格（default/media）|


备份压缩所需目录
tar -zcf /sdcard/1/termux-backup.tar.gz home usr