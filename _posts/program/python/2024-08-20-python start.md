---
categories: [Program lang, Python]
tags: [python]
math: true
mermaid: true
render_with_liquid: true
img_path: 
description: Python 的入门笔记
pin: 
---

## 基本规范

### 常见问题
### pycharm debug的问题
第一行是注释时，需要debug标注两行才能正常执行

### 注释

```python
# 单行注释 
'''多行注释'''
```

#### PEP 8规范
* 单行注释 #后跟一个空格
* 行内注释 #后跟两个空格
* python代码最后一行是空行

### 变量类型
* 变量的数据类型，由变量中的存储数据决定
* 查看变量类型： type()  返回类型
* 字符类型 单双引号均可
* 布尔类型 首字母大写
* 标识符不能数字开头，由字母、_、数字组成
![](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/markdeanzhq.github.io/_posts/program/python/2024-08-20-start.md/134307125783080.png)

### 基本结构语句

#### if
```python
if condition1:
    ...
elif condition2:
    ...
else:
    ...
```
#### 三目运算符 
```python
data = a if a > b else b  
变量 = 表达式1 if 条件 else 表达式2
```

#### while
```python
while 判断条件:
    ...
    
```
#### for

## 基础函数
### 输入输出
#### 输出 - print
##### 格式符号
```python
print('str', 12) #  输出相隔一个空格 "str 12"
print(1 + 2) #  运算输出
print("I'm %s" % name)  #  格式化输出
print("I'm %s, %d years old." % (name, age))  #  多变量，格式化输出
print("%%")  #  输出%   
# python3.6支持 f-string
printf(f"I'm {name}, {age} years old.") #  前面的f 可以大写F
```
![](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/markdeanzhq.github.io/_posts/program/python/2024-08-20-start.md/445885789727606.png)

##### 默认输出
默认会添加一个换行，可以用 , end='' 自定义或去掉换行  
```python
print('hello', end='66')
print('world')
# 输出内容：hello66world
```


#### 输入 - input
返回数据<mark>都</mark>是字符串类型
```python
pwd = input('pwd:')
# 执行效果：输出界面"pwd:" 后，并等待输入
```


### 类型转换 - eval 等
  
去除引号，还原原来数据类型  
```python
eval('100') #  int
eval('123.23') #  float
eval('num') #  变量 num 只能作为右值
```

普通类型转换：  
* int(x [,base])      base 表示转换进制
* int('23', 8)  #  将23转换为八进制
![](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/markdeanzhq.github.io/_posts/program/python/2024-08-20-start.md/27753013416929.png)


### 运算符
仅列出与C不同的运算符类型

* // 整除
    * 复合赋值; //=
* ** 指数，幂运算 10的20次方：10**20
    * **=


#### 逻辑运算符
![](https://raw.githubusercontent.com/MarkDeanZHQ/ImageHost/main/markdeanzhq.github.io/_posts/program/python/2024-08-20-start.md/344163383821512.png)

### 功能函数
#### 随机函数
```python
import random
random.randint(a, b) #  生成a-b 随机整数
```

