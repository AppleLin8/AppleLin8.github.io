---
title: python main
layout: post
categories: python
date:   2020-12-2 12:06:28 +0800
tags: python
excerpt: python __main__
---
--------------------
文章出自个人博客<https://applelin8.github.io/2020/12/2/python-main>，转载请申明

------------------
# content <span id="home">
* [__main__](#1)
* [read](#2)
* [numpy](#3)

----------------------------

# main <span id="1">

Calculate the area of a circle

```python
#const.py
PI = 3.14

def main():
    print("PI:", PI)

if __name__ == "__main__":
    main()
  
```



```python
#area.py
from const import PI

def calc_circle_area(radius):
    return PI * (radius ** 2)
    
def main():
    print("circle area: ", calc_circle_area(2))
    
main()
```

# read <span id="2">

```python
# File: read.py

import sys
import re

def read_cmd(file, type):
    with open(file) as file:
        i=0
        for line in file:
            if line.find(type) != -1 and line.find(',') != -1:
                i+=1
                #print(line,end='')
                print(re.split(r'=| |,', line.strip())[0])
        print('cmd count is %d'%(i))


if __name__ == '__main__':
    file=sys.argv[1]
    type=sys.argv[2]
    
    print(file, type)
    read_cmd(file, type)
```

# numpy <span id="3">

安装
```bash
python -m pip install numpy scipy matplotlib -i https://pypi.tuna.tsinghua.edu.cn/simple

python -m pip install pandas seaborn -i https://pypi.tuna.tsinghua.edu.cn/simple

```

画直方图

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from matplotlib.font_manager import FontProperties   #显示中文，并指定字体
myfont=FontProperties(fname=r'C:/Windows/Fonts/simhei.ttf',size=14)
sns.set(font=myfont.get_name())
plt.rcParams['axes.unicode_minus']=False      #显示负号

def draw_123():
    plt.rcParams['figure.figsize'] = (13, 5)    #设定图片大小
    f = plt.figure()                            #确定画布

    x = list(range(1,10))
    a = np.asarray(x)
    print("a is : ",a);

    f.add_subplot(1,2,1)
    sns.distplot(a, kde=False)                 #绘制频数直方图
    #sns.distplot(a, kde=True,hist=True)                 #绘制频数直方图
    plt.ylabel("频数", fontsize=16)
    plt.xticks(fontsize=16)                    #设置x轴刻度值的字体大小
    plt.yticks(fontsize=16)                   #设置y轴刻度值的字体大小
    plt.title("(draw 1..10)", fontsize=20)             #设置子图标题
    
    f.add_subplot(1,2,2)
    sns.distplot(a)                           #绘制密度直方图
    plt.ylabel("密度", fontsize=16)
    plt.xticks(fontsize=16)                  #设置x轴刻度值的字体大小
    plt.yticks(fontsize=16)                  #设置y轴刻度值的字体大小
    
    plt.subplots_adjust(wspace=0.3)         #调整两幅子图的间距
    plt.show()


if __name__ == '__main__':
    draw_123()
```

![draw_plot.png](https://AppleLin8.github.io/assets/img/blog/draw_plot.png)