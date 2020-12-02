---
title: python main
layout: post
categories: python
date:   2020-12-2 12:30:28 +0800
tags: python
excerpt: python if __name__ == "__main__"\:
---
--------------------
文章出自个人博客<https://applelin8.github.io/2020/12/2/python-main>，转载请申明

------------------
# content <span id="home">
* [__main__](#1)


----------------------------

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

