# Matplotlib_learning
## Some notes about learing matplotlib(14 Days)

![myprofile](https://user-images.githubusercontent.com/99868099/158113303-bd3e129e-9910-4502-81e9-97becd2e2a67.jpg)
=======
## 1.brief introduction
1. figure components   
Figure-Axes(sub figures)-Axis(axis/grid)-Tick(measure)
2. two interfaces
  * object-oriented style<br>
  create figure and axes then draw(use ax to call function)
  ```python
  x = np.linspace(0, 2, 100) # range
  fig, ax = plt.subplots()  # figure\ax
  ax.plot(x, x, label='linear')  
  ax.plot(x, x**2, label='quadratic')  
  ax.plot(x, x**3, label='cubic')  
  ax.set_xlabel('x label') 
  ax.set_ylabel('y label') 
  ax.set_title("Simple Plot")  
  ax.legend() 
  plt.show()
  ```
  * pyplot<br>
  use pyplot to call function
  ```python
  x = np.linspace(0, 2, 100)
  plt.plot(x, x, label='linear') 
  plt.plot(x, x**2, label='quadratic')  
  plt.plot(x, x**3, label='cubic')
  plt.xlabel('x label')
  plt.ylabel('y label')
  plt.title("Simple Plot")
  plt.legend()
  plt.show()
  ```
3. template<br>
can stick to the template and add your contents
```python
# step1 variable
x = np.linspace(0, 2, 100)
y = x**2

# step2 set styles of lines
mpl.rc('lines', linewidth=4, linestyle='-.')

# step3 set layout(eg. 3*3)
fig, ax = plt.subplots()  

# step4 figure
ax.plot(x, y, label='linear')  

# step5 improvement
ax.set_xlabel('x label') 
ax.set_ylabel('y label') 
ax.set_title("Simple Plot")  
ax.legend()
```
---
**思考题**<br>
1. 请思考两种绘图模式的优缺点和各自适合的使用场景<br>
- oo模式可利用subplots方法进行进行子图的分布设置，当要画多张子图放在同一张figure中时，即可在此设置；缺点则是画单张图时代码与pyplot比较为繁琐；
- pyplot比较简单，适合画单张图，不适合画多张子图。
2. 在第五节绘图模板中我们是以OO模式作为例子展示的，请思考并写一个pyplot绘图模式的简单模板
```python
# step1 准备数据
x = np.linspace(0, 2, 100)
y = x**2

# step2 设置绘图样式，这一模块的扩展参考第五章进一步学习，这一步不是必须的，样式也可以在绘制图像是进行设置
mpl.rc('lines', linewidth=4, linestyle='-.')

# step3 绘制图像， 这一模块的扩展参考第二章进一步学习
plt.plot(x, y, label='linear')  

# step4 添加标签，文字和图例，这一模块的扩展参考第四章进一步学习
plt.xlabel('x label') 
plt.ylabel('y label') 
plt.title("Simple Plot")  
plt.legend()
plt.show()
```

***

## 2.primitives and object container
1. Abstract
* three layers of api
  * FigureCabvas(drawing zone)
  * Render(drawing pencil)
  * Artist(setting styles)
* categories of artist
  * prinitive
    * Line
    * Text
    * Rectangle
    * Image
    * etc.
  * container
    * Figure
    * Axes
    * Axis
2. primitives
* 2D line
  * set by plot func
  ```python
  x = range(0,5)
  y = [2,5,7,8,10]
  plt.plot(x,y, linewidth=10);
  ```
  * set on line obj
  ```python
  x = range(0,5)
  y = [2,5,7,8,10]
  line, = plt.plot(x, y, '-') # 列表解包的操作，列表中有一个Line2D对象的元素，获取这个对象
  line.set_antialiased(False); # 关闭抗锯齿
  ```
  * set by setp func
  ```python
  x = range(0,5)
  y = [2,5,7,8,10]
  lines = plt.plot(x, y)
  plt.setp(lines, color='r', linewidth=10); # 利用setp函数对获取的lines属性列表进行操作
  ```
* draw lines
  * straight line
    * plot
    ```python
    x = range(0,5)
    y1 = [2,5,7,8,10]
    y2= [3,6,8,9,11]
    fig,ax= plt.subplots() # 创建图层及坐标系
    ax.plot(x,y1)
    ax.plot(x,y2)
    ```
    * line object
    ```python
    x = range(0,5)
    y1 = [2,5,7,8,10]
    y2 = [3,6,8,9,11]
    fig,ax= plt.subplots()
    lines = [Line2D(x, y1), Line2D(x, y2,color='orange')]  # 显式创建Line2D对象，对象中传递相关参数
    for line in lines: # 使用for循环对对象进行操作
        ax.add_line(line) # 使用add_line方法将创建的Line2D添加到子图中
    ax.set_xlim(0,4)
    ax.set_ylim(2, 11);
    ```
  * errorbar
* patches
  * rectangle
    * hist
    ```python
    x=np.random.randint(0,100,100) #生成[0-100)之间的100个数据,即 数据集 
    bins=np.arange(0,101,10) #设置连续的边界值，即直方图的分布区间[0,10),[10,20)... 
    plt.hist(x,bins,color='fuchsia',alpha=0.5)#alpha设置透明度，0为完全透明 
    plt.xlabel('scores') 
    plt.ylabel('count') 
    plt.xlim(0,100);
    ```
    ```python
    # rectangle class
    fig = plt.figure()
    ax1 = fig.add_subplot(111)

    for i in df_cnt.index:
      rect =     plt.Rectangle((df_cnt.loc[i,'mini'],0),df_cnt.loc[i,'width'],df_cnt.loc[i,'fenzu'])
      ax1.add_patch(rect)
    ax1.set_xlim(0, 100)
    ax1.set_ylim(0, 16);
    ```
    * bar
    ```python
    # bar绘制柱状图
    y = range(1,17)
    plt.bar(np.arange(16), y, alpha=0.5, width=0.5, color='yellow', edgecolor='red',  label='The First Bar', lw=3);
    ```
    ```python
    # Rectangle矩形类绘制柱状图
    fig = plt.figure()
    ax1 = fig.add_subplot(111)
    for i in range(1,17):
        rect =  plt.Rectangle((i+0.25,0),0.5,i) # Rectangle(lower left point, width, height)
        ax1.add_patch(rect)
    ax1.set_xlim(0, 16)
    ax1.set_ylim(0, 16);
    ```
  * polygoan 
  ```python
  # 用fill来绘制图形
  x = np.linspace(0, 5 * np.pi, 1000) 
  y1 = np.sin(x)
  y2 = np.sin(2 * x) 
  plt.fill(x, y1, color = "g", alpha = 0.3);
  ```
  * wedge(pie chart)
  ```python
  # use pie
  labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'
  sizes = [15, 30, 45, 10] # data
  explode = (0, 0.1, 0, 0) # offset of radius
  fig1, ax1 = plt.subplots()
  # autopct:the form of percentage display;startangle: the start angle of pie chart(counterclockwise)
  ax1.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%', shadow=True, startangle=90)
  ax1.axis('equal');
  ```
  ```python
  # use wedge
  # wedge(center,r,theta1,theta2,width=None,**kwargs)
  fig = plt.figure(figsize=(5,5))
  ax1 = fig.add_subplot(111)
  theta1 = 0
  sizes = [15,30,45,10]
  patches = []
  patches += [
      Wedge((0.5, 0.5), .4, 0, 54),           
      Wedge((0.5, 0.5), .4, 54, 162),  
      Wedge((0.5, 0.5), .4, 162, 324),           
      Wedge((0.5, 0.5), .4, 324, 360), 
  ]
  colors = 100 * np.random.rand(len(patches))
  p = PatchCollection(patches,alpha=0.8)
  p.set_array(colors)
  ax1.add_collection(p);
  ```
* collections(scatter plot)
```python
# user scatter
x = [0,2,4,6,8,10] # the position of x axis
y = [10]*len(x) # all at the pos of 10 on y axis
s = [20*2**n for n in range(len(x))] # set the size of dots
plt.scatter(x,y,s=s)
```
* images
```python
methods = [None, 'none', 'nearest', 'bilinear', 'bicubic', 'spline16',
           'spline36', 'hanning', 'hamming', 'hermite', 'kaiser', 'quadric',
           'catrom', 'gaussian', 'bessel', 'mitchell', 'sinc', 'lanczos']


grid = np.random.rand(4, 4)

fig, axs = plt.subplots(nrows=3, ncols=6, figsize=(9, 6),
                        subplot_kw={'xticks': [], 'yticks': []})

for ax, interp_method in zip(axs.flat, methods):
    ax.imshow(grid, interpolation=interp_method, cmap='viridis')
    ax.set_title(str(interp_method))

plt.tight_layout();
```
3. Object container
include primitives and properties
* figure
```python
# primitives of subplot and axes added in list of axes
fig = plt.figure()
ax1 = fig.add_subplot(211)
ax2 = fig.add_axes([0.1,0.1,0.7,0.3]) # coordinate of left point, width, height
print(ax1)
print(fig.axes)
```
```python
# use 'for' circle
fig = plt.figure()
ax1 = fig.add_subplot(211)
for ax in fig.axes:
    ax.grid(True)
```
* axes
```python
fig = plt.figure()
ax = fig.add_subplot(111)
rect = ax.patch  # 利用axes的patch属性实例化Rectangle对象
rect.set_facecolor('green')
```
* axis
style of axis(label,scale,title,grid)
```python
# use axis to get text and position of scale
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"

fig, ax = plt.subplots()
x = range(0,5)
y = [2,5,7,8,10]
plt.plot(x, y, '-')

axis = ax.xaxis # axis为X轴对象
axis.get_ticklocs()     # 获取刻度线位置
axis.get_ticklabels()   # 获取刻度label列表(一个Text实例的列表）。 
axis.get_ticklines()    # 获取刻度线列表(一个Line2D实例的列表）。 
axis.get_data_interval()# 获取轴刻度间隔
axis.get_view_interval()# 获取轴视角（位置）的间隔
```
set the properties of axis and scale
```python
fig = plt.figure() # 创建一个新图表
rect = fig.patch   # 矩形实例并将其设为黄色
rect.set_facecolor('lightgoldenrodyellow')

ax1 = fig.add_axes([0.1, 0.3, 0.4, 0.4]) # 创一个axes对象，从(0.1,0.3)的位置开始，宽和高都为0.4，
rect = ax1.patch   # ax1的矩形设为灰色,实例化对象rect
rect.set_facecolor('lightslategray')


for label in ax1.xaxis.get_ticklabels(): 
    # 调用x轴刻度标签实例，是一个text实例
    label.set_color('red') # 颜色
    label.set_rotation(45) # 旋转角度
    label.set_fontsize(16) # 字体大小

for line in ax1.yaxis.get_ticklines():
    # 调用y轴刻度线条实例, 是一个Line2D实例
    line.set_color('green')    # 颜色
    line.set_markersize(25)    # marker大小
    line.set_markeredgewidth(2)# marker粗细
```
* tick
tick1 -> (down of x-axis/left of y-axis); tick2 -> (up of x-axis/right of y-axis)
```python
fig, ax = plt.subplots()
ax.plot(100*np.random.rand(20))

# 设置ticker的显示格式
formatter = matplotlib.ticker.FormatStrFormatter('$%1.2f')
ax.yaxis.set_major_formatter(formatter)

# 设置ticker的参数，右侧为主轴，颜色为绿色
ax.yaxis.set_tick_params(which='major', labelcolor='green',
                         labelleft=False, labelright=True);
```

***
**思考题**<br>
1. primitives 和 container的区别和联系是什么，分别用于控制可视化图表中的哪些要素<br>
primitive是图的元素，而container可以利用自身属性创建元素的对象，并通过对象来进行样式的调整。

2. 使用提供的drug数据集，对第一列yyyy和第二列state分组求和，画出下面折线图。PA加粗标黄，其他为灰色。

3. 分别用一组长方形柱和填充面积的方式模仿画出下图，函数 y = -1 * (x - 2) * (x - 8) +10 在区间[2,9]的积分面积
