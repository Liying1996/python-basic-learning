### ***python版本及解释器***
##### [版本]
1. python2.7
2. python3.7

##### [解释器]
1. Pycharm (交互)
2. Jupyter Notebook （交互）
3. Spider （交互）
2. Atom 
3. Sublime Text 
4. Vim
5. VS code
6. Notepad ++ 
6. ......

##### [注意]
1. 缩进： 一个tab or 四个空格
2. 严格区分大小写
3. 单行注释（#）
4. 多行注释（'''）
---
### ***数据结构***

##### [字符串 str]
单双引号； 必要时候可以转义
`print('I\'m \"OK\"!')`
`I'm "OK"!`
##### [整数 int]
  <br>

##### [浮点数 float]
即小数。
整数和浮点数在计算机内部存储的方式是不同的，整数运算永远是精确的（除法难道也是精确的？是的！），而浮点数运算则可能会有四舍五入的误差。

##### [布尔 bool]
True
False
##### [空值 None]
NoneType
##### [列表 list]
`L = [1,2,3,4,5]`
可修改 
O(n)
0-base
pop()
sorted()
remove()
......
##### [元组 tuple]
不可修改
`t = (1,2,3,4,5)`
只有1个元素的tuple定义时必须加一个逗号
`t = (1,)`

##### [集合 set]
`s = set()`
O(1)
集合中元素无重复值，无序，可以对list中的元素去重
s.add()
s.update()
s.remove()
s1.intersection(s2)
.......
##### [字典 dictionary]
可变，可存储任意类型
`dict = {'a': 1, 'b': 2, 'b': '3'}`
key必须为不可变类型，所以列表不可以为key
平均O(1) 复杂度低
del()
get()
.......
一般一个key对应一个value key值唯一；
一个key映射多个value:  `from collections import defaultdict` 

---
### ***条件判断和循环***
##### [条件]
if...elif...else

##### [循环]
for
while
break
pass
continue

**example**:
```
while True:
    a = int(input('please input a number: '))
    if a == 1:
        print('yes')
        break
    elif a >= 1:
        print('>')
    else:
        print('<')
```

---
### ***数值计算***
##### [加减乘除 +=*/]
注意python2和3的区别
##### [地板除 //]
舍去小数点后面的数字
##### [取模 %]
取出10以内的奇数
```
 for i in range(1,11):
    if i % 2 == 1:
        print(i)
        
[i for i in range(1,11) if i % 2 == 1]   
```

---
### ***函数***
1. 调用函数
2. 自定义函数 def...return...
3. 函数的参数；默认参数
4. 递归函数（汉诺塔问题；斐波那契数列）
   虽然逻辑清晰，但是运行速度慢，占用内存多
    实现上述两个问题
5. 高阶函数 
    ```
    def add(x, y, f):
        return f(x) + f(y)
    ```
    传入的参数是另一个函数
6. 返回函数 ***（注意闭包）***
    闭包概念：在一个内部函数中，对外部作用域的变量进行引用，(并且一般外部函数的返回值为内部函数)，那么内部函数就被认为是闭包。eg. 
    ```
    def outer(x):
        def inner(y):
            return x + y
        return inner
    ```
    闭包无法直接访问外部函数的局部变量; (**???**)
   作用域（全局变量；局部变量）
7. 装饰器
   [介绍1](https://www.zhihu.com/question/26930016)
   [介绍2](https://foofish.net/python-decorator.html)
8. 捕获异常
    try...except
9. 命令行
    ```
    import argparse
    parser = argparse.ArgumentParser()
    parser.add_argument("-t", help = "", required = True)
    args = parser.parse_args()
    print args.t
    ```
    ```
    # 1. 命令行， 必须参数 -n 名字; -a 年龄；返回xx今年xx岁；非必须参数 -s 身高 加一个xx高；
###### 封装到函数里并调用
```
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("-n", help = "", required = True)
parser.add_argument("-a", help = "", required = True)
parser.add_argument("-s", help = "", required = False)
args = parser.parse_args()
#if args.s:
#   print('{}今年{}岁{}height'.format(args.n,args.a,args.s))
#else:
#   print('{}今年{}岁'.format(args.n,args.a))
if args.s == None:
    print('{}今年{}岁'.format(args.n,args.a))
else:
    print('{}今年{}岁{}height'.format(args.n,args.a,args.s))
 ```  

***封装成函数***
```
import argparse
def args():
    parser = argparse.ArgumentParser()
    parser.add_argument("-n", help = "someone's name...", required = True)
    args = parser.parse_args()
    return args

def greet(name):
    return 'hello, {}!'.format(name)

def main():
    name = args().n
    return greet(name)

print(main())
```
```
# 1. 命令行， 必须参数 -n 名字; -a 年龄；返回xx今年xx岁；非必须参数 -s 身高 加一个xx高；
# 2. 封装到函数里并调用
import argparse
def args():
    parser = argparse.ArgumentParser()
    parser.add_argument("-n", help = "", required = True)
    parser.add_argument("-a", help = "", required = True)
    parser.add_argument("-s", help = "", required = False)
    args = parser.parse_args()
    return args
def inputinfo(name,age,height=None):
    if height==None:
        return '{}今年{}岁'.format(name,age)
    else:
        return '{}今年{}岁,{}高'.format(name,age,height)
def main():
    name = args().n
    age = args().a
    height = args().s
    return inputinfo(name,age,height)
print(main())
```
---
### ***类***
1. 继承
2. 多态

```
class Person:
    def __init__(self, name, age):
        self.age = age
        self.name = name
    def get_name(self):
        return self.name
    def get_info(self):
        return "{} is {} years old. ".format(self.name, self.age)

p = Person('gouzi', '24')
p.get_info()
```


```
# 写一个类Bird，定义两个参数， 鸟的名字和鸟的颜色，\
# 两个函数：一个叫eat，一个叫drink， 返回xx's color is xx, and it is eating/drinking...
class Bird:
    def __init__(self, name, color):
        self.name = name
        self.color = color
    def eat(self):
        return "{}'s color is {},and it is eating".format(self.name,self.color)
Bird('bird1', 'yellow').eat()

```
---
### IO
##### 文件读写

```
# 读取文件的方法
f = open('test.txt', 'r')   # 一下子全部读取 
# w 写入 r只读 rb 二进制只读 wb二进制写入 a追加
for line in f:
    .........
f.close()

# 最合适的：（不需要close with open自己会处理）
with open('test.txt', 'r') as f:
    for line in f:
        ......... 

# 写入文件
f = open('test2.txt', 'w')
f.write('....')
f.close()

# 或者
with open('test2.txt', 'w') as f:
    f.write('...')

```

##### 文件操作和目录
    ```
    # 查看当前目录的绝对路径:
    os.path.abspath('.')
    '/Users/xxx'
    # 在某个目录下创建一个新目录，首先把新目录的完整路径表示出来:
    os.path.join('/Users/xxx/', 'testdir')
    '/Users/xxx/testdir'
    # 创建一个目录:
    os.mkdir('/Users/xxx/testdir')
    # 删掉一个目录:
    os.rmdir('/Users/xxx/testdir')
    ```
---
### ***进程 & 线程***
1. 全局解释器锁 (GIL)
某个线程想要执行，必须先拿到GIL，相当于拿到了通行证；并且在一个python进程中，GIL只有一个。拿不到通行证的线程，就不允许进入CPU执行。

    ***python的多线程是否没用？***
    1、CPU密集型代码(各种循环处理、计数等等)，在这种情况下，ticks计数很快就会达到阈值，然后触发GIL的释放与再竞争（多个线程来回切换当然是需要消耗资源的），所以python下的多线程对CPU密集型代码并不友好。

    2、IO密集型代码(文件处理、网络爬虫等)，多线程能够有效提升效率(单线程下有IO操作会进行IO等待，造成不必要的时间浪费，而开启多线程能在线程A等待时，自动切换到线程B，可以不浪费CPU的资源，从而能提升程序执行效率)。所以python的多线程对IO密集型代码比较友好。

2. 多线程 multithreading
3. 多进程 multiprocessing

---
### ***正则表达式***
regular expression
[介绍](http://www.runoob.com/python/python-reg-expressions.html)
```
import re
re.search(pattern, string, flags=0)
re.match(pattern, string, flags=0) 
re.sub(pattern, repl, string, count=0, flags=0) # 替换
re.compile(pattern[, flags]) # 编译正则表达式
findall #返回所有匹配正确的
```

---
### 数据分析
1. pandas 
2. numpy
3. array
4. matplotlib
5. seaborn</br>
6.[scikit-learn](https://scikit-learn.org/stable/) 

---
### ***pythonic code***
1. 列表推导式(生成式)
```
 L = [i for i in range(10) if i % 2 == 0]
```
2. 匿名函数lambda
    `list(map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7, 8, 9]))`



3. 迭代用enumerate
```
    for i, value in enumerate(['A', 'B', 'C']):
        print(i, value)
```
4. 生成器(generator)
    `g = (x * x for x in range(10))`
    next()
    yield()
    ```
    def odd():
        print('step 1')
        yield 1
        print('step 2')
        yield(3)
        print('step 3')
        yield(5)
    ```
5. map & reduce
    `list(map(str, [1, 2, 3, 4, 5, 6, 7, 8, 9]))`

    ```
    from functools import reduce
    def fn(x, y):
        return x * 10 + y
    reduce(fn, [1, 3, 5, 7, 9])
    ```
6. filter
    ```
    def is_odd(n):
        return n % 2 == 1

    list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
    # 结果: [1, 5, 9, 15]
    ```
7. sorted
    `sorted([36, 5, -12, 9, -21], key=abs)`

8. zip

