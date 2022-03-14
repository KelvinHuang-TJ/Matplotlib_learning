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
