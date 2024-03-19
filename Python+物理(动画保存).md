##### scipy中的odient函数求解微分方程简单讲解
odeint(func, y0, t, args=(), Dfun=None, col_deriv=0, full_output=0,ml=None, mu=None, rtol=None, atol=None, tcrit=None, h0=0.0,hmax=0.0, hmin=0.0, ixpr=0, mxstep=0, mxhnil=0, mxordn=12,  mxords=5, printmessg=0, tfirst=False)
###### 参数解析

- func 函数名，极为重要  
    举个例子：如果你要解的微分方程为:dy/dt=t,那么可以设

```python
def func(y,t):
    return t
```

再一个例子:dy/dt=y

```python
def func(y,t):
    return y
```

theta''(t) + b\*theta'(t) + c\*sin(theta(t)) = 0  
那么可以令：theta'(t) = omega(t)
omega'(t) = -b\*omega(t) - c\*sin(theta(t))

```python
def pend(y, t, b, c):
    theta, omega = y
    dydt = [omega, -b * omega - c * np.sin(theta)]
    return dydt
```

从第三个例子可以看出,可以是一个数组

- y0  
    y0,很好理解，自然就是微分方程的初始值
- args很简单看第三个微分方程$theta''(t) + b*theta'(t) + c*sin(theta(t)) = 0$的例子:
    \_b,c_是常量，而这个args就是用来带入这个常量的
- t  
    自然就是定义域的的数值,比如当t在（0，100）时,就可以

```text
t = np.linspace(1,100,1000)
```

###### 举例

- dy/dt=y，这个方程在y0=1时的解是y=exp(t)

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

#定义函数
def func(y, t):
    return np.array(y)


t = np.linspace(0, 10, 100)
result = odeint(func, y0=1, t=t)
y_real = np.exp(t)
plt.plot(t, result[:, 0], label='odient', marker='*')
plt.plot(t, y_real, label='real')
plt.legend()
plt.show()
```
- theta''(t) + b\*theta'(t) + c\*sin(theta(t)) = 0
    那么可以令：theta'(t) = omega(t)omega'(t) = -b\*omega(t) - c\*sin(theta(t))

```python
def pend(y, t, b, c):
    theta, omega = y
    dydt = [omega, -b * omega - c * np.sin(theta)]
    return dydt

b = 0.25
c = 5.0
y0 = [np.pi - 0.1, 0.0]
t = np.linspace(0, 10, 101)
sol = odeint(pend, y0=y0, t=t, args=(b, c))
plt.plot(t, sol[:, 0], 'b', label='theta(t)')
plt.plot(t, sol[:, 1], 'g', label='omega(t)')
plt.legend(loc='best')
plt.xlabel('t')
plt.grid()
plt.show()
```
##### 函数FuncAnimation
函数FuncAnimation(fig,func,frames,init_func,interval,blit)是绘制动图的主要函数，其参数如下：
    a.fig 绘制动图的画布名称`
    b.func自定义动画函数，即下边程序定义的函数update
    c.frames动画长度，一次循环包含的帧数，在函数运行时，其值会传递给函数update(n)的形参“n”
    d.init_func自定义开始帧，即传入刚定义的函数init,初始化函数
    e.interval更新频率，以ms计
    f.blit选择更新所有点，还是仅更新产生变化的点。应选择True，但mac用户请选择False，否则无法显
    
- plt画布调整函数
```python
# 调整画布里图像的位置
plt.subplots_adjust(top=0.88,
				bottom=0.11,
				left=0.11,
				right=0.9,
				hspace=0.2,
				wspace=0.2)
# 使图像在画布上尽可能大，贴着画布边缘
plt.tight_layout()
# 设置画布尺寸
plt.figure(figsize=(11, 5.6))
```
###### 示例
```python
# 动态画出sin函数曲线
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation

# 生成子图，相当于fig = plt.figure(),ax = fig.add_subplot(),其中ax的函数参数表示把当前画布进行分割，
fig, ax = plt.subplots()
xdata, ydata = [], []
ln, = ax.plot([], [], 'r-', animated=False)

def init():
    ax.set_xlim(0, 2 * np.pi)
    ax.set_ylim(-1, 1)
    # 返回曲线
    return ln,

def update(frame):
    # 将每次传过来的n追加到xdata中
    xdata.append(frame)
    ydata.append(np.sin(frame))
    # 重新设置曲线的值
    ln.set_data(xdata, ydata)
    return ln,

ani = FuncAnimation(fig=fig, func=update, frames=np.linspace(0, 2 * np.pi, 128),
                    init_func=init, blit=True)

plt.show()

ani.save('sin_test1.gif', writer='imagemagick', fps=100)
```