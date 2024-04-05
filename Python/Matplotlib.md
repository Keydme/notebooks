#python #可视化
[可以随机做几个的好看玩意](https://matplotlib.org/stable/gallery/index.html)


[热力图的绘制](https://blog.csdn.net/KIKI_ZSH/article/details/123505175)
主要通过 **matplotlib.pyplot.imshow()** 色系展示
或 **matplotlib.pyplot.matshow()** 绘制指定图
感觉这两种的调用都长得一样
其中的cmap是个好东西

流图函数使用教程
[Python的streamplot使用及说明](https://www.jb51.net/python/299352zdw.htm)
[绘制流图](https://geek-docs.com/matplotlib/matplotlib-pyplot/matplotlib-pyplot-streamplot-in-python.html)
PS:上面这个图中有很多好用的东西

[文本的添加与注释](https://blog.csdn.net/weixin_48964486/article/details/124073704)
水印+注释

[python画个好看的双复摆](https://zhuanlan.zhihu.com/p/340482320)
主要使用atplotlib.animation.FuncAnimation保存动画


[极好的pyplot的简单教程](https://blog.csdn.net/Crayonxin2000/article/details/119910846?spm=1001.2014.3001.5502)

# pyplot基础
matplotlib有些默认配置不能显示中文，而且格式不符合论文规范，需要设置一下
```python
# 设置字体为宋体
plt.rcParams['font.family'] = ['serif'] # 设置字体为有衬线字体（宋体是有衬线字体之一）
plt.rcParams['font.serif'] = ['SimSun'] # 设置有衬线字体为宋体
## 下面的是设置字体为黑体
# plt.rcParams['font.family'] = ['sans-serif'] # 设置字体为无衬线字体（黑体是无衬线字体之一）
# plt.rcParams['font.sans-serif'] = ['SimHei'] # 设置无衬线字体为黑体

# 设置公式格式
plt.rcParams['mathtext.fontset'] = 'stix'

# 正常显示负号
plt.rcParams['axes.unicode_minus'] = False
plt.rcParams['font.size']=18 #设 置字体字号
plt.rcParams['xtick.labelsize']=16 # 设置横坐标轴字体字号
plt.rcParams['ytick.labelsize']=16 # 设置纵坐标轴字体字号

# 设置刻度朝里，我喜欢朝里，默认的朝外感觉有点丑
plt.tick_params(which="major",direction='in',length=5,bottom=True,left=True)
```
## plt绘图类型
1. 折线  `plt.plot(X,Y)`
2. 散点  `plt.scatter(X,Y)`
3. 柱状  `plt.bar(X,Y)`
4. (频数)直方图  `plt.hist(array)`
5. 饼图  `plt.pie(data,labels=,autopct='%1.1f%%')`
6. 箱线图 `plt.boxplot(X,Y)`
![[../img/Pasted image 20240324175613.png]]
7. 流图 `plt.streamplot(X,Y,U,V,linewidth=2)`
8. 等高图 `plt.contour(X,Y,Z,level)`
9. 3D面图 `ax.plot_surface(X,Y,Z)`
	(`fig,ax=plt.subplots(subplot_kw={"projection":"3d"})`)
10. 待续
## 基本操作
1. 添加信息
```python
plt.xlabel() # 设置 x 轴标签 
plt.ylabel() # 设置 y 轴标签 
plt.title() # 设置标题
```
2. 显示刻度
`plt.xticks()`
3. 显示图例
`plt.legend()`
4. 显示图像
`plt.show`
5. 样式设计
```python
# 设置线条宽度 
plt.rcParams['lines.linewidth']=1 
# 设置线条颜色 
plt.rcParams['lines.color']='green' 
# 设置线条样式 
plt.rcParams['lines.linestytle']='-'
```

## 简单的高级用法

名词解析：
- 画板-Figure
- 画纸-Axes
- 坐标轴-Axis
- 样式-Artist
- ...

### Figure

### Axes
![[../img/Pasted image 20240324155729.png]]

