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
