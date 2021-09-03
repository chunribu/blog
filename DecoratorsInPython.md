[🏠HOME](README.md)

# Python装饰器（Decorators in Python）

---

装饰器本身是函数，这是一种高阶函数，其返回值是一个新的函数（在输入函数的基础上增加了某些功能）。

比如在后面的例子，是一个打印函数运行时间的装饰器。在定义函数前`@calculate_time`，则在函数运行前查询系统时间，函数运行后再次查询系统时间，并打印时间差。

```python
import time
import math

def calculate_time(func):
    
    def wrapper(*args, **kwargs):
        begin = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print("Total time taken in : ", func.__name__, end - begin)
        return result
    return wrapper

@calculate_time
def factorial(num):
    return math.factorial(num)
    
# calling the function
factorial(10)
```
Out：
```
3628800

Total time taken in :  factorial 2.6226043701171875e-06
```

函数是对象，有__name__等属性，但经过decorator装饰之后的函数，实质上已经是另一个函数了，其__name__从原来的`factorial`变成了`wrapper`。为了使被装饰的函数看起来仅是增加了功能，Python内置的`functools.wraps`提供了简洁的写法。

```python
import time
from functools import wraps

def calculate_time(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        begin = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print("Total time taken in : ", func.__name__, end - begin)
        return result
    return wrapper
```

还有一些装饰器是带参数的，本质上，是对不带参数的装饰器的更高阶封装。下面的例子用来打印指定文本和函数的签名。

```python
from functools import wraps

def log(text):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator

@log('execute')
def now():
    print('2021-9-3')

now()
```
Out:
```
execute now():
2021-9-3
```
