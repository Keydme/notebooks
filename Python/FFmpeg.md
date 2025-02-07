# 安装下载
[官网](https://ffmpeg.org/download.html)
# 命令行各个参数用途
利用cmd仅保存输出的消息无输入的命令行指令

1> 2> cmd重定向
ffmpeg 的日志输出全部都是用标准错误输出，即stderr。  
所以实际只有“2>”起到效果。  
不保存使用的命令行信息。  
控制台将不再出现相关信息。

```bash
//示例1
ffmpeg -i input output 2> XXX.txt
//示例2
ffmpeg -i input output 1> XXX.txt 2>&1
```

### -report
转储完整的命令行和控制台输出到当前目录一个文件名 ​​为program - YYYYMMDD - HHMMSS .log的文件。  
此文件对于错误报告非常有用。这也意味着-loglevel verbose。  
保存全部的信息。


### 多文件合并转换示例
```bash
ffmpeg -safe 0 -f concat -y -i index.txt -c copy {output_file}.mp4 2> msg.txt
```