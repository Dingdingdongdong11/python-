# 2.3python语言基础
相对于《python编程从入门到实践》有一定的拔高，挑几个补充点
## 2.3.1.6 isinstance检查对象类型


```python
a = 5
b=2.5
```


```python
isinstance(a, int)
```


```python
isinstance(b, float)
```


```python
isinstance(a, (int, float))
```

## 2.1.3.7 属性和方法


```python
c = 'foo'
c.format
```

## 2.3.1.8 验证是否可迭代


```python
def isiterable(obj):
    try:
        iter(obj)
        return True
    except TypeError:  #类型错误不可遍历
        return False
```


```python
isiterable('a string')  #字符串可迭代，即可遍历
```


```python
isiterable([1,2,5])
```


```python
isiterable(5)
```

## 2.3.2.1 数值类型
整数和浮点型
整数可以储存任意大小的数字


```python
ival = 5211314
ival**10
```

浮点型float 每个浮点数都是双精度64位


```python
faval = 3.1415926
```

可以用科学计数法表示


```python
faval = 12345.67e-5
faval+1
```

e-7就是十的负七次方

整数除法，自动转型为浮点数


```python
3/2
```

如果想整数除完还是整数。利用//


```python
3//2
```

## 2.3.2.2 字符串
多行字符用三引号


```python
c = '''
一顿火锅
两顿烧烤
三杯可乐
四盆龙虾
'''
```

这个字符串包含了5行文本，换行符\n也是包含在其中

试着用count计算换行符


```python
c.count('\n')
```

下面说下这个反斜杠，\

    1.反斜杠作为转义符号
    
参考苦行僧95的博客园：

https://www.cnblogs.com/kuxingseng95/p/9462294.html

目前见过的 ' , \t, \n


```python
print('I \'am a good boy.')
```


```python
s='\n'
print(s)
```

可以看出反斜杠是有特殊作用的

那么杠一个普通的内容会怎样


```python
s='\a'
print(s)
```

无输出，非正常存在


```python
s='\ab'
print(s)
```

a不正常输出，b正常输出


```python
s='b\a'
print(s)
```

a仍然不正常


```python
s='\'
print(s)
```

报错


```python
s='\\'
print(s)
```

正常输出反斜杠


```python
s='\\\'
print(s)
```

报错，最后一个杠无转义内容


```python
s='\\\\'
print(s)
```

正常输出


```python
s='\\\a'
print(s)
```

a无法正常输出

杠数字的问题


```python
s='12\\24'
print(s)
```


```python
s='\24'
s
```

这里如果单独s有输出，其为x14，是16进制，即1*16+4 = 20

原来的\24省略了0即\024,其为8进制，即2*8+4 = 20， 两者相等

如果print(s)输出结果与\a相同


```python
s='12\\\24'
print(s)
```


```python
s
```

如果想要轻松打出\。可以使用r'

raw表示原生的


```python
s = r'人\生\不\易\\且\吃\且\珍\惜'
s #注意这里是查看s本身
```


```python
print(s)
```

# 2.3.2.3 字节与Unicode

encode 使文本变为bytes类型， decode进行解码重新变为str类型

可以直接用b''转换为bytes类型,但仅限于ASCII码，汉字不行


```python
b1 = b'破马张飞'
```


```python
b1 = b'po ma zhang fei'
b1
```


```python
type(b1)
```


```python
#下面进行解码
decoded = b1.decode('utf8')
decoded
```


```python
type(decoded)
```

## 2.3.2.5 类型转换
str bool int float 之间的转换


```python
s = '3.1415926'
fs = float(s)  #字符串类型转换为浮点数
```


```python
type(s)
```


```python
type(fs)
```


```python
fs
```

 int（）函数不能直接将字符串型转换为整型，必须先转换为float类型


```python
int(s)
```


```python
int(fs)
```


```python
bool(fs)
```

数字0的布尔值为False 但字符的布尔值为True


```python
bool(0)
```


```python
bool(s)
```

字符串是0为True，但空字符为False


```python
bool('0')
```


```python
bool('')
```

## 2.3.2.6 None
None可以作为一个常用的函数参数默认值


```python
def add_and_maybe_multiply(a, b, c=None):
    result = a+b
    if c is not None:
        result = result * c
    return result
```

None不仅是一个关键字，还是None Type类型的唯一实例


```python
type(None)
```

## 2.3.2.7 日期和时间
做数据， 时间是一个非常重要的因素

下面为整理结果

年月日 时分秒


```python
from datetime import datetime, date, time
dt = datetime(2011, 10, 29, 20, 30,21)
```


```python
dt.day
```


```python
dt.minute
```


```python
dt.date()
```


```python
dt.time()
```

strftime 方法将datetime转换为字符串

年月日 时分秒顺序可以任意调整, 间隔用什么符号分开也可以自定义，如/ -等


```python
dt.strftime('%Y-%m-%d  %H : %M')
```


```python
#字符串对象转换为datetime对象
datetime.strptime('20091031', '%Y%m%d')
```

替换时间中的某些值


```python
dt
```


```python
dt.replace(minute = 0, second = 0)
```

计算两个时间点之间间隔了多长时间


```python
dt1 = datetime(2019, 5, 8, 10, 12, 30)
dt2 = datetime(2024, 6, 7, 8, 28, 57)
delta = dt2-dt1
```


```python
delta  #delta为一种新的类型
```

如果知道今天，想知道过十天是哪天，怎么办


```python
dt2 + delta
```

# Datetime 格式化的详细说明
%Y 四位年份

%y 两位年份

%m 两位的月份[01, 12]

%d 两位的天数[01, 31]

%H 24小时制[00, 23]

%I 12小时制[01, 12]

%M 两位分钟[00, 59]

%S 秒值[00, 61]

%w 星期值[0, 6] 0是星期天

%U 一年中第几个星期[00, 53], 星期天是每周第一天，第一个星期天前的一周是第0个星期

%W 一年中第几个星期[00, 53], 星期一是每周第一天，第一个星期一前的一周是第0个星期

%z UTC时区偏置，格式为 +HHMM或 -HHMM；如果是简单时区则为空

%F %Y-%m-%d的简写（如2012-4-18）

%D %m/%d%y的简写（如04/1812)
