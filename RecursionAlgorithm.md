[🏠HOME](README.md)

# 递归算法（Recursion Algorithm）

在数学与计算机科学中，是指在函数的定义中使用函数自身的方法。递归一词还较常用于描述以自相似方法重复事物的过程。例如，当两面镜子相互之间近似平行时，镜中嵌套的图像是以无限递归的形式出现的。

## 理解递归

### 自然语言例子

+ 从前有座山，山里有座庙，庙里有个老和尚，正在给小和尚讲故事呢！故事是什么呢？“从前有座山，山里有座庙，庙里有个老和尚，正在给小和尚讲故事呢！故事是什么呢？‘从前有座山，山里有座庙，庙里有个老和尚，正在给小和尚讲故事呢！故事是什么呢？……’”

### 计算机语言例子

+ 阶乘（factorial）

表达式: `n! = n * (n-1) * (n-2) * ... * 1`

```python
def factorial(n):
    return 1 if n==1 else n*factorial(n-1)
```

+ 斐波那契数列（Fibonacci sequence）

表达式: `f(n) = (n-1) + (n-2)`

第n项（**n≥0**）为其前面两项之和，值依次是 `0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...`

```python
def fibonacci(n):
    if n==0 or n==1:
        return n
    elif n > 1:
        return fibonacci(n-1) + fibonacci(n-2)
```

当n较大时，由于大量重复运算，运算效率会降低。可采用`functools.lru_catch`充分利用缓存的运算结果。

```python
from functools import lru_catch

@lru_catch
def fibonacci(n):
    if n==0 or n==1:
        return n
    elif n > 1:
        return fibonacci(n-1) + fibonacci(n-2)
```