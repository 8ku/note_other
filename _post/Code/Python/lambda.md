# lambda

匿名函数，lambda 是为了减少单行函数的定义而存在的。

好处是不用定义函数，不用写return

lambda 左边为返回函数，右侧为表达式

`lambda [arg1][arg2....argn]] : expression`

举例：

```python
# 单参数函数
g = lambda x : x ** 2
print(g(3))
# 等于
def g(x):
    return x ** 2

#多参数函数
g = lambda x,y,z : (x + y) ** z
print(g(1,2,2))

```

